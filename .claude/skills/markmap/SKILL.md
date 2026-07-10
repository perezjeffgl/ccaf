---
name: markmap
description: Generate an interactive HTML mind map and export PNG/SVG images from a .mm.md Markmap file. Runs the markmap CLI, validates output, and writes files into the docs/ directory.
when_to_use: Use when the user asks to generate, render, or export a mind map from a *.mm.md file, or passes a markmap filename as an argument.
argument-hint: "file.mm.md"
paths:
  - "**/*.mm.md"
---

# Markmap Skill

Convert a `.mm.md` Markmap file into an interactive HTML mind map and export it as PNG and SVG images.

> ref: https://markmap.js.org/

## How to invoke

```
/markmap <file.mm.md>
```

Example: `/markmap mindmaps/introduction-to-agent-skills.mm.md`

Derive `<basename>` from the input filename (strip path and `.mm.md`, e.g. `introduction-to-agent-skills`). All output goes to `docs/`.

---

## Step 1 — Generate offline HTML

`markmap-cli` only produces HTML (no direct image export). Use `--offline` to inline all CDN assets so the headless browser can render without network access:

```bash
mkdir -p assets
npx markmap-cli --no-open --offline --output docs/<basename>.html <file.mm.md> 2>&1
```

### Validate HTML

```bash
head -1 docs/<basename>.html
ls -lh docs/<basename>.html
```

- Valid: first line is `<!doctype html>` and file is non-zero (expect ~350 KB with `--offline`).
- If empty or not `<!doctype html>`, show the captured output and stop.

---

## Step 2 — Export PNG and SVG with puppeteer

`markmap-cli` embeds the SVG as `<svg id="mindmap">` but it is empty at parse time — D3 populates it at runtime. A headless browser is required to render it.

**puppeteer v25.3.0** is already cached at `~/.npm/_npx/`. Use it without installing anything.

### Find the puppeteer npx cache directory

```bash
PUPPETEER_BASE=$(ls -d ~/.npm/_npx/*/node_modules/puppeteer 2>/dev/null | head -1 | xargs dirname | xargs dirname)
```

### Write the export script into that directory and run it

```bash
SCRIPT="$PUPPETEER_BASE/markmap-export.mjs"
cat > "$SCRIPT" << 'EOF'
import puppeteer from 'puppeteer';
import { writeFileSync } from 'fs';
import { pathToFileURL } from 'url';

const [htmlPath, outPng, outSvg] = process.argv.slice(2);
const browser = await puppeteer.launch({ headless: true });
const page = await browser.newPage();
await page.setViewport({ width: 1920, height: 1080 });
await page.goto(pathToFileURL(htmlPath).href, { waitUntil: 'networkidle0' });
await page.waitForSelector('svg#mindmap > g', { timeout: 10000 });
if (outPng) await page.screenshot({ path: outPng, fullPage: false });
if (outSvg) {
  const svgHtml = await page.$eval('svg#mindmap', el => el.outerHTML);
  writeFileSync(outSvg, svgHtml);
}
await browser.close();
EOF

node "$SCRIPT" \
  docs/<basename>.html \
  docs/<basename>.png \
  docs/<basename>.svg 2>&1

rm -f "$SCRIPT"
```

> The script must live inside the npx cache directory so Node's ESM resolver can find the `puppeteer` package.

### Validate exports

```bash
file docs/<basename>.png
head -c 40 docs/<basename>.svg
ls -lh docs/<basename>.{png,svg}
```

- Valid PNG: `file` reports `PNG image data, 1920 x 1080`.
- Valid SVG: starts with `<svg id="mindmap"`.
- On failure, show the full captured error output.

---

## Authoring / editing .mm.md files

If the source file needs fixes before rendering:

1. Use headings and/or nested bullet lists for hierarchy.
2. Keep heading levels monotonic (avoid skipping levels).
3. Keep each node concise; split long nodes into children.
4. Preserve links and inline emphasis (`**bold**`, `_italic_`, `` `code` ``).
5. Fix malformed YAML frontmatter while preserving intent.

### Frontmatter reference

```yaml
---
title: <Title>
markmap:
  initialExpandLevel: 2
  maxWidth: 0
  colorFreezeLevel: 2
  duration: 500
  spacingHorizontal: 80
  spacingVertical: 5
  lineWidth: 2
  zoom: true
  pan: true
---
```

---

## After generating

Report all three output paths and sizes:
- `docs/<basename>.html` — interactive mind map (~350 KB offline)
- `docs/<basename>.png` — raster screenshot at 1920×1080
- `docs/<basename>.svg` — extracted vector SVG

If the CLI or puppeteer is missing, suggest `npm install -g markmap-cli` or `npm install -g puppeteer`.
