# [VideoDB Director Agent](https://github.com/Coral-Protocol/Coral-VideoDbDirector-Agent)

VideoDB Director Agent is a specialized AI agent that processes, analyzes, and extracts insights from video content using advanced AI capabilities. It can watch videos, translate video content, generate summaries, extract key moments, answer questions about video content, and provide detailed analysis through natural language interactions within the Coral Protocol ecosystem.

## Responsibility
VideoDB Director Agent serves as an intelligent video content analyzer and processor that can understand, interpret, and respond to queries about video content. It handles video watching, transcription, summarization, question answering, and content analysis tasks. The agent processes video URLs (YouTube, local files, etc.), extracts meaningful information, and provides comprehensive insights through natural language responses, making video content accessible and searchable through conversational AI interactions.

## Details
- **Framework**: LangChain
- **Tools used**: VideoDB MCP Tools, Coral MCP Tools
- **AI model**: GPT-4.1-mini, supports configurable LLM providers
- **Date added**: July 2025
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
- `VIDEODB_API_KEY`: VideoDB platform API key for video processing

Optional environment variables:
- `MODEL_NAME`: LLM model name (default: "gpt-4o")
- `MODEL_PROVIDER`: LLM provider (default: "openai")
- `MODEL_TOKEN`: Max tokens (default: "4000")
- `MODEL_TEMPERATURE`: Model temperature (default: "0.3")

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

The VideoDB Director Agent provides comprehensive video content analysis and processing capabilities:

### Video Content Analysis
- Watch and process videos from YouTube URLs, local files, and other sources
- Transcribe speech and audio content from videos
- Generate comprehensive summaries of video content
- Extract key moments and important segments from videos
- Answer specific questions about video content and context

### AI-Powered Video Understanding
- Analyze video content using advanced AI models
- Provide detailed insights and explanations about video topics
- Generate bullet-point summaries and structured content analysis
- Identify and describe key themes, topics, and concepts in videos
- Process long-form video content with intelligent summarization

### Intelligent Content Extraction
- Identify and summarize key points from video presentations
- Extract important quotes and statements from video content
- Generate structured summaries with main topics and subtopics
- Provide detailed analysis of video content with context and explanations

## Example

<details>

```bash
# Input from orchestrating agent:
"Watch the <Youtube URL> video and give a summary about it in bullet points"

# VideoDB Director Agent Response:
✅ Successfully processed video: "Introduction to AI and Machine Learning"
📋 Video Analysis Summary:
   - Duration: 45 minutes
   - Main Topic: Artificial Intelligence Fundamentals
   
📝 Key Points:
   • AI is a branch of computer science focused on creating intelligent machines
   • Machine learning is a subset of AI that enables systems to learn from data
   • Three main types of ML: supervised, unsupervised, and reinforcement learning
   • Deep learning uses neural networks to process complex patterns
   • Current applications include image recognition, natural language processing, and autonomous vehicles
   
🎯 Key Insights:
   - The video emphasizes the practical applications of AI in modern technology
   - Discusses the evolution from rule-based systems to data-driven approaches
   - Highlights the importance of ethical considerations in AI development
   
📤 Analysis complete and ready for further processing or agent collaboration.

```
</details>

## Creator Details
- **Name**: Mustafa Khan
- **Affiliation**: Coral Protocol
- **Contact**: [Discord](https://discord.com/invite/Xjm892dtt3)
