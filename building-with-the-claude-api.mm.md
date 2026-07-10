---
title: api
---

# API
Building with the Claude API
A comprehensive course covering the full spectrum of working with Anthropic models using the Claude API.

**Anthropic Learning Path**: https://anthropic.skilljar.com/claude-with-the-anthropic-api

## Models
Understanding different Claude models and their use cases
  * opus
    - expensive but best for complex tasks
    - best for code generation and reasoning
  * sonnet
    - best for general-purpose tasks
    - balance of intelligence, cost, and speed
  * haiku
    - fastest and most cost-effective
    - best for simple tasks and high-volume applications

## Authentication,Setup,API calls

## Prompt Engineering
Crafting effective prompts and context management
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

## Tools
Allowing models to interact with external APIs and databases for enhanced capabilities

* goal
  - Allow model to access and interact
    * external data sources
    * external services
* usage
  - External APIs or databases
  - Back and forth interaction pattern
  - Loop conversation until task is complete
  - Add details about tools and their integration with the Claude API
  - tools: [ref_to_schema]
  - multi turn interactions with tools
    - stop_reason: tool_use
* functions
  - calls to perform tasks
  - calls to retrieve information
  - best practices
    * Well-named functions
    * Clear input and output specifications
    * Error handling and validation
* schema
  - structure of data for tools and functions
  - JSON rules for defining schemas
  - Ensure compatibility with the Claude API's expected formats
  - ToolParam(schema)
  - Append to message content for tool calls as assistant messages
* ToolUseBlock results
  - tool_use_id
  - content
  - is_error
* build-in tools
  * buildin
  * only write schema
  * tools
    - TextEditor
    - WebSearch
      - search web for
      - max_uses:, allowed_domains:
      - citations

## Streaming
Real-time response handling and optimization techniques

* Event types
  - InputJsonEvent key properties
    - partial_json
    - snapshot
* FGTC: Fine grained tool calling
  - fine_grained=True
  - send groups of chunks
  - disable JSON validation
* Chunks
  - type == input_json
  - chunk: {abstract, meta, content}
    - abstract: high-level description of the tool call
    - meta: metadata about the tool call (e.g., tool name, parameters)
    - content: detailed information or results from the tool call

## RAG
Retrieval-Augmented Generation (RAG) techniques for enhanced responses and Agentic search for information retrieval and decision-making
- problem
  - large documents
  - options
    - send all document to prompt(hard limit)
    - break into chunks and send relevant chunks
      - different methods to select relevant chunks
        - embedding similarity search
        - keyword matching
        - vector databases
- RAG
  - retrieve relevant information from external sources
  - chunkin strategies
    - size-based
      * include overlap between chunks to maintain context
    - semantic-based
      * divide by headers or sections
    - structure-based
      * divide by groups of related information
      * requires understanding of document structure
    - sentence-based
      * divide by sentences or paragraphs
      * may require more complex processing to maintain coherence
      * include optimal overlap to maintain context
- Text Embeddings
  - convert text into vector/numerical representations
  - number = score
  - used for similarity search in RAG
  - embedding models available through the Claude API
    - text-embedding-3-small
    - text-embedding-3-large
  - normalization of embeddings
    - ensure consistent scale and distribution of embedding vectors
    - improve performance of similarity search
  - numbers  [-1..1] stored in vector databases
    * vectorDB.add(embedding, chunk)
    * calculate cosine similarity between query embedding and stored embeddings to find relevant information
    * calculate cosine distance between vectors to determine relevance
  - search systems
    * lexical search(classic keyword-based)
      - keyword matching
      - simple and fast
      - may miss relevant information due to synonyms or variations in language
      - BM25Index 
        - considers term frequency
        - considers inverse document frequency
        - can be used in combination with embedding similarity
    * semantic search(embedding similarity)
      - embedding similarity search
      - more sophisticated and can capture meaning and context
      - may be slower
      - require more computational resources
      - VectorIndex
         - efficient data structure for storing and searching embeddings
  - retriever
    * merge results
    * RRF (Reciprocal Rank Fusion)
      - combine results from multiple search methods
        * lexical
        * semantic
      - rank results based on relevance scores from both methods
  - provider
    - VoyageAI
      * install via pip: `pip install voyageai`
      * VOYAGEAI_API_KEY environment variable
      * generate_embedding(text, model, input_type)

## Features
- extended thinking
  - reasoning(also known as)
  - thinking=True
  - thinking_budget=1000
  - redacted thinking block
    - magic string used as part of the prompt to indicate where the thinking block is located
- vision
  - image captioning support
  - object recognition
  - visual question answering
- pdf
  - extract text and images from PDFs
  - use extracted information for RAG and other tasks
- citations
  - provide sources for retrieved information
  - create clear trail from response back to original sources
  - enhance credibility and transparency of responses
  - include in response content or as metadata
- prompt caching
  - store and reuse prompts for efficiency
  - reduce latency for common queries
  - manage cache with expiration and invalidation strategies
  - turn on
    * cache_control: `content: [{type: "ephemeral"}]`
    * add breakpoint in the prompt to indicate where to cache
  - todo cache
    - list of tools
    - system prompt(content must be at least 1024 tokens long)
- Files API(tool)
  - FileMetadata(file_id, type, ...)
  - ContainerUploadBlock(file_id, content, ...)
    - `{ "type": "container_upload", "file_id": "123", "content": "file content" }`
  - run isolated container
  - upload and manage files for use in prompts and tool calls
  - support for various file types (e.g., text, CSV, JSON)
  - integration with RAG for retrieving information from uploaded files
  - type=code_execution_file
    * download_file()
## CC Apps
- Computer Use
- Agents
- Claude Code
  - features
    - Discover
    - Design
    - Build
    - Deploy
    - Support & Scale
  - Common Workflows
    - Plan/Implement workflow
      - feed context
      - plan solution
      - implement solution
    - TDD workflow
      - feed context
      - think some test cases
      - implement tests
      - write code to pass tests
  - Connecting to external services
    - via MCP
      - add custom functionality by connecting servers that provides
        - tools
        - resources
        - integrations
## Workflow & Agents
- when to use
  - workflow: you can picture exact steps to solve a problem
  - agent: you are not sure what task or parameters to use
  - Benefits
- workflow patterns
  - Evaluator-Optimizer
    - input
    - producer
    - grader
    - output
  - Parallelization
    - send multiple requests to the model in parallel
  - Chaining
    - break complex tasks into smaller subsequent tasks
    - split work into focused steps
  - Routing
    - use initial call to categorize the ask
    - forward to specialized pipeline(workflow, prompt, set of tools, etc)
    - when to use
      - apps with diverse types of request
      - we can clearly define categories
      - specialized processing outweighs the cost of routing
## Environment inspection
- Benefits
  - better progress tracking
  - error handling
  - quality assurance
  - adaptaive behavior
- implementation
  - reading file contents before modification
  - taking screenshots after UI interactions
  - checking API responses for expected data
  - validating generated content against requirements
[← Back to Courses Overview](COURSES.md)