# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a playground repository for experimenting with DeepCode (deepcode-hku), an AI agent framework that uses MCP (Model Context Protocol) servers for enhanced capabilities like web search, file operations, and code execution.

## Setup and Installation

```bash
# Install Python dependencies
pip install deepcode-hku

# Or use uv (faster)
uv sync

# Install Node.js dependencies (for MCP servers)
pnpm install
```

### Configuration Files

- **mcp_agent.config.yaml**: Main configuration for DeepCode agent
  - Configures MCP servers (brave search, filesystem, code-implementation, etc.)
  - Sets LLM provider (line 106): "anthropic", "google", or "openai"
  - Configures document segmentation settings
  - Sets logging levels and output paths

- **mcp_agent.secrets.yaml**: API keys and secrets (gitignored)
  - Contains API keys for LLM providers (OpenAI, Anthropic, Google)
  - Search API keys (Brave, Bocha)
  - Never commit this file

## MCP Server Architecture

DeepCode uses multiple MCP servers for different capabilities:

1. **Search Servers**:
   - `brave`: Web search via Brave Search API (default)
   - `bocha-mcp`: Alternative search provider
   - Configure default with `default_search_server` in config

2. **Code & File Servers**:
   - `filesystem`: File system operations in current directory
   - `code-implementation`: Paper code reproduction with execution
   - `code-reference-indexer`: Intelligent code reference search
   - `command-executor`: Execute system commands

3. **Utility Servers**:
   - `fetch`: HTTP fetch operations
   - `file-downloader`: PDF and file downloads
   - `github-downloader`: Git repository operations
   - `document-segmentation`: Smart document chunking for large files

## Platform-Specific MCP Configuration

The MCP servers use different commands on different platforms:

- **macOS/Linux**: Uses `npx` for Node.js-based servers
- **Windows**: Uses `node` with absolute paths (commented out in config)

When modifying MCP server configs, ensure platform-appropriate commands are used.

## LLM Provider Configuration

DeepCode supports multiple LLM providers with automatic fallback:

- Set `llm_provider` in mcp_agent.config.yaml (line 106)
- Configure provider-specific models:
  - OpenAI: `default_model` supports OpenRouter format (e.g., "anthropic/claude-sonnet-4.5")
  - Google: Uses Gemini models (e.g., "gemini-3-pro-preview")
  - Anthropic: Uses Claude models (e.g., "claude-sonnet-4.5")

## Document Segmentation

For large documents (>50,000 chars by default):
- Enable with `document_segmentation.enabled: true` in config
- Adjust threshold with `size_threshold_chars`
- Uses intelligent chunking to optimize token usage

## Execution Engine

- Uses `asyncio` execution engine by default
- Handles concurrent MCP server operations
- Configured via `execution_engine` in config

## Development Workflow

```bash
# Run the main script
python main.py

# Or with uv
uv run main.py
```

## Key Configuration Decisions

When working with this codebase:

1. **LLM Provider Selection**: Check which provider's API keys are configured before running tasks
2. **Search API**: Ensure Brave or Bocha API keys are set for web search functionality
3. **MCP Server Paths**: Python-based MCP servers reference `tools/*.py` files - these are part of the deepcode-hku package installation
4. **Environment Variables**: All MCP servers can use `PYTHONPATH: .` for local development
