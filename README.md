# [VideoDB Director Agent](https://github.com/Coral-Protocol/Coral-VideoDbDirector-Agent)

VideoDB Director Agent is a specialized agent for managing video streaming, text messaging, and coordinating communication between agents within the Coral Protocol ecosystem. It provides comprehensive video processing capabilities and seamless agent-to-agent communication through the VideoDB MCP tools.

## Responsibility
VideoDB Director Agent acts as the primary interface for video processing and agent coordination within multi-agent workflows. It handles video streaming operations, text message management, and facilitates communication between different agents in the Coral Protocol network, enabling seamless integration of video services into automated multi-agent systems.

## Details
- **Framework**: LangChain
- **Tools used**: VideoDB MCP Tools, Coral MCP Tools
- **AI model**: GPT-4.1-mini, supports configurable LLM providers
- **Date added**: January 2025
- **License**: MIT

## Setup the Agent

### 1. Clone & Install Dependencies

<details>  

```bash
# In a new terminal clone the repository:
git clone https://github.com/Coral-Protocol/Coral-VideoDbDirector-Agent.git

# Navigate to the project directory:
cd Coral-VideoDbDirector-Agent

# Install `uv`:
pip install uv

# Install dependencies from `pyproject.toml` using `uv`:
uv sync
```

</details>

### 2. Configure Environment Variables

Get the required credentials:
- [OpenAI API Key](https://platform.openai.com/api-keys) or other LLM provider
- [VideoDB API Key](https://videodb.io/) for video processing services

<details>

```bash
# Create .env file in project root
cp -r env.example .env
```

Required environment variables:
- `OPENAI_API_KEY`: Your LLM provider API key
- `coral_base_url`: Coral server SSE endpoint URL
- `VIDEODB_API_KEY`: VideoDB platform API key for video processing

Optional environment variables:
- `MODEL_NAME`: LLM model name (default: "gpt-4o")
- `MODEL_PROVIDER`: LLM provider (default: "openai")

</details>

## Run the Agent

You can run in either of the below modes to get your system running.  

- The Executable Model is part of the Coral Protocol Orchestrator which works with [Coral Studio UI](https://github.com/Coral-Protocol/coral-studio).  
- The Dev Mode allows the Coral Server and all agents to be separately running on each terminal without UI support.  

### 1. Executable Mode

Checkout: [How to Build a Multi-Agent System with Awesome Open Source Agents using Coral Protocol](https://github.com/Coral-Protocol/existing-agent-sessions-tutorial-private-temp) and update the file: `coral-server/src/main/resources/application.yaml` with the details below, then run the [Coral Server](https://github.com/Coral-Protocol/coral-server) and [Coral Studio UI](https://github.com/Coral-Protocol/coral-studio). You do not need to set up the `.env` in the project directory for running in this mode; it will be captured through the variables below.

<details>

For Linux or MAC:

```bash
# PROJECT_DIR="/PATH/TO/YOUR/PROJECT"

applications:
  - id: "app"
    name: "VideoDB Director Application"
    description: "Video processing and agent coordination agent for streaming and messaging operations"
    privacyKeys:
      - "default-key"
      - "public"
      - "priv"

registry:
  videodb-director-agent:
    options:
      - name: "OPENAI_API_KEY"
        type: "string"
        description: "API key for the LLM service"
      - name: "VIDEODB_API_KEY"
        type: "string"
        description: "VideoDB platform API key"
    runtime:
      type: "executable"
      command: ["bash", "-c", "${PROJECT_DIR}/run_agent.sh main.py"]
      environment:
        - name: "OPENAI_API_KEY"
          from: "OPENAI_API_KEY"
        - name: "VIDEODB_API_KEY"
          from: "VIDEODB_API_KEY"
        - name: "MODEL_NAME"
          value: "gpt-4.1-mini"
        - name: "MODEL_PROVIDER"
          value: "openai"
        - name: "MODEL_TOKEN"
          value: "4000"
        - name: "MODEL_TEMPERATURE"
          value: "0.3"

```

For Windows, create a powershell command (run_agent.ps1) and run:

```bash
command: ["powershell","-ExecutionPolicy", "Bypass", "-File", "${PROJECT_DIR}/run_agent.ps1","main.py"]
```

</details>

### 2. Dev Mode

Ensure that the [Coral Server](https://github.com/Coral-Protocol/coral-server) is running on your system and run below command in a separate terminal.

<details>

```bash
# Run the agent using `uv`:
uv run main.py
```
</details>

## Capabilities

The VideoDB Director Agent provides comprehensive video processing and agent coordination capabilities:

### Video Processing
- Stream video content through VideoDB platform
- Process video files and manage video metadata
- Handle video format conversions and optimizations
- Manage video storage and retrieval operations

### Video Streaming Management
- Manage video streaming sessions
- Handle streaming quality and bandwidth optimization
- Support multiple streaming protocols
- Monitor streaming performance and metrics


## Example

<details>

```bash
# Input from orchestrating agent:
"Watch the <Youtube URL> video and give a summary about it in bullet points"

# VideoDB Director Agent Response:
✅ Successfully initiated video streaming for 'presentation.mp4'
📋 Streaming Details:
   - URL: https://stream.videodb.io/presentation-12345
   - Status: Active
   - Quality: HD (1080p)
   
📤 Message sent to user agent with streaming information.
Streaming session is ready for viewing.

```
</details>

## Creator Details
- **Name**: Mustafa Khan
- **Affiliation**: Coral Protocol
- **Contact**: [Discord](https://discord.com/invite/Xjm892dtt3)
