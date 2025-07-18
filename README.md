# Coral VideoDB Director Agent

A Python-based agent that facilitates communication between AI agents using Coral Server and provides video processing capabilities through VideoDB.

## Features

- Agent-to-agent communication via Coral Server MCP protocol
- Video processing and streaming capabilities through VideoDB
- Real-time mention-based messaging system
- Asynchronous task execution with error handling

## Prerequisites

- Python 3.12+
- UV package manager
- Access to Coral Server
- VideoDB API access
- OpenAI API access

## Setup

1. **Clone and initialize the project:**
   ```bash
   uv sync
   ```

2. **Create a `.env` file with the following variables:**
   ```bash
   # Coral Server Configuration
   coral_base_url=http://localhost:8080/api/v1/mcp
   
   # LLM Configuration
   llm_model_name=gpt-4o-mini
   llm_model_provider=openai
   OPENAI_API_KEY=your_openai_api_key_here
   
   # VideoDB Configuration
   VIDEODB_API_KEY=your_videodb_api_key_here
   ```

3. **Install VideoDB MCP server (if not already installed):**
   ```bash
   pipx install videodb-director-mcp
   ```

## Usage

Run the agent:
```bash
uv run python Coral-VideoDB-Director-Agent.py
```

The agent will:
1. Connect to Coral Server and VideoDB
2. Wait for mentions from other agents
3. Process instructions and execute appropriate tools
4. Respond back with results or error messages

## Architecture

- **Coral Tools**: Handle agent communication (threads, messages, mentions)
- **VideoDB Tools**: Handle video processing and streaming operations
- **LLM Integration**: Uses OpenAI models for intelligent task processing
- **Error Handling**: Comprehensive error handling with automatic retries

## Dependencies

- `langchain-mcp-adapters==0.0.10`: MCP protocol integration
- `python-dotenv`: Environment variable management
- `langchain>=0.2.0`: LLM framework
- `langchain-openai>=0.1.0`: OpenAI integration


