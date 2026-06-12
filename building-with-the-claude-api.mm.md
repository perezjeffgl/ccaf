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

## Authentication

## Setup

## API calls

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
* Fine grained tool calling
  - fine_grained=True
  - specify which tool to call and when
  - control flow based on tool results
  - dynamic tool selection based on context
  - disable JSON validation for more flexible tool interactions







## Batch Processing

## Streaming
Real-time response handling and optimization techniques

* Event types
  * InputJsonEvent key properties
    - partial_json
    - snapshot
* Chunks
  * type == input_json
 

## Error Handling

* Rate Limiting
* Retries

## Building
Scaling, monitoring, and deploying Claude API applications

[← Back to Courses Overview](COURSES.md)