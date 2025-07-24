# NLIP with Agent Frameworks Demo

Demonstrates **Natural Language Interaction Protocol (NLIP)** integration with AI agent frameworks, showcasing inter-agent communication capabilities.

📹 **[Watch Demo Video](https://drive.google.com/file/d/1TgfTimKEdIOnGHDFqr67ipTRew2SxIw2/view?usp=sharing)** - See the demo in action!

📄 **Presentation Slides**: "(Potentially) Integrating NLIP with Agent Development Frameworks (July 23, '25).pdf"

## 🎯 What This Shows

1. **🔄 Inter-Agent Communication**: LangChain coordinator delegates to LlamaIndex worker via NLIP
2. **🏠 Standalone Integration**: Direct NLIP integration with individual frameworks

**Key Capabilities:**
- Cross-framework communication via NLIP protocol
- Task delegation between specialized agents

## 🏗️ Project Structure

```
nlip-with-agent-frameworks/
├── README.md                    # This file
├── pyproject.toml              # Dependencies and project config
├── requirements.txt         
├── .env                        # Environment variables 
├── demo/
│   ├── inter_agent/           # Inter-agent communication demo
│   │   ├── langchain_coordinator.py
│   │   ├── llamaindex_worker.py
│   │   └── README.md
│   ├── standalone/            # Standalone framework demos
│   │   ├── langchain_standalone.py
│   │   ├── llamaindex_standalone.py
│   │   └── README.md
│   └── shared/               # Shared utilities
│       ├── weather_tools.py
│       ├── nlip_client.py
│       └── __init__.py
```

## 🚀 Quick Start

**Prerequisites:** Python 3.10+, Poetry (recommended) or pip

**Setup:**
```bash
git clone <repository-url>
cd nlip-with-agent-frameworks

# Clone the nlip-server dependency into the project directory
git clone https://github.com/nlip-project/nlip_server.git

# Install project dependencies
poetry install  # or: pip install -r requirements.txt

# Configure API key
cp .env.example .env
# Edit .env with: OPENROUTER_API_KEY=your-key-from-https://openrouter.ai/
```

### Run Inter-Agent Demo

Open two terminals in the project directory:

**Terminal 1 - Start LlamaIndex Agent:**
```bash
poetry run uvicorn demo.inter_agent.llamaindex_worker:app --host 0.0.0.0 --port 8013 --reload
```

**Terminal 2 - Start LangChain Agent:**
```bash
poetry run uvicorn demo.inter_agent.langchain_coordinator:app --host 0.0.0.0 --port 8012 --reload
```

**Terminal 3 - NLIP client:**
```bash
curl -X POST http://localhost:8012/nlip/ \
  -H "Content-Type: application/json" \
  -d '{"format": "text", "subformat": "english", "content": "Weather alerts for California?"}'
```

### Run Standalone Demo
```bash
export OPENROUTER_API_KEY=your-key-from-https://openrouter.ai/
poetry run uvicorn demo.standalone.langchain_standalone:app --port 8014
# Or: poetry run uvicorn demo.standalone.llamaindex_standalone:app --port 8015
```

## 📊 Demo Scenarios

**Inter-Agent:** Client → LangChain → (NLIP) → LlamaIndex → Weather APIs  
**Standalone:** Client → NLIP Server → Weather APIs  


## 📋 Dependencies

This demo requires:
- **Python 3.10+** (required for NLIP SDK)
- **NLIP SDK & Server** (installed from PyPI: `nlip-sdk>=0.1.2`, `nlip-server`)
- **OpenRouter API Key** (for AI model access)
