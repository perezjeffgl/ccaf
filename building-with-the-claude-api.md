# Building with the Claude API

A comprehensive course covering the full spectrum of working with Anthropic models using the Claude API.

## Main Sections

- **API Fundamentals** — Authentication, setup, and basic API calls
- **Model Capabilities** — Understanding different Claude models and their use cases
- **Prompt Engineering** — Crafting effective prompts and context management
- **Advanced Features** — Vision, tool use, batch processing, and streaming
- **Error Handling & Reliability** — Rate limiting, retries, and error management
- **Building Production Applications** — Scaling, monitoring, and deploying Claude API applications

## Course Link

- **Anthropic Learning Path**: https://anthropic.skilljar.com/claude-with-the-anthropic-api

---

[← Back to Courses Overview](COURSES.md)

===================introduction-to-model-context-protocol
* mcp
  * advantage: save time on implementation(schema+functions) 
  * transport agnostic: standart IO

===================claude-with-the-anthropic-api
* models
  * sonnet
  * haiku
  * opus
* temperature [0...1]
  * how likely each token is to be selected
  * low
    * more deterministic(select the highest probability)
  * high
    * more random output(distribute probability more evenly)
    * varied and creative
* response time (output + input) size
  * streaming = send initial quick response
  * chunk of responses
* structured data
  * 
