## MCP
Model Context Protocol (MCP) for managing and optimizing model interactions. Master MCP's three core primitives—tools, resources, and prompts—to connect Claude with external services.

Anthropic Learning Path: https://anthropic.skilljar.com/introduction-to-model-context-protocol 

- advantage
  - save time on implementation(schema+functions) 
  - transport agnostic: standard IO
- goal
  - provide standardized way to manage context and state
  - mcp use schemas + functions
- author
  - anyone can write a MCP provider
- different from API calls
  - API calls are for specific tasks and interactions with the model
  - MCP is for managing the overall context and state of interactions with the model
- client
  - library or framework that implements the MCP protocol
  - provides tools and functions for managing context and state of interactions with the model
  - handles communication with the model
  - ensures compliance with the MCP protocol
  - core methods
    - list_tools
    - call_tool
- server
  - implementation of the MCP protocol
  - managing context and state of interactions with the model
  - can be built on top of existing APIs or services
  - responsible for executing tools and functions defined in the MCP schema
  - Tools
    - model-controlled
  - Resources
    - app-controlled
    - @mcp.resource decorator
      - defines a resource that can be used by the model
    - types
      - direct resource
      - template resources
    - MIME types
  - Prompts
    - user-controlled
    - @mcp.prompt decorator
      - defines a prompt that can be used by the model
    - list_prompts
    - get_prompt
    - arguments
- FastMCP: python library for building MCP servers(SDK)
  - annotate functions with @mcp_function decorator
  - define schemas for tools and functions using JSON schema
- Inspector
  - web-based tool for inspecting and debugging MCP interactions
  - python virtual env



[← Back to Courses Overview](COURSES.md)
