<div align="center">

# TradingAgents with Poe Integration

**A powerful multi-Agent trading framework integrating Poe platform API, supporting GPT, Claude, Gemini and more LLMs**

[English](README.md) | [简体中文](README_zh.md)

[![GitHub Stars](https://img.shields.io/github/stars/Hewuliu/TradingAgents-Poe-api?style=flat-square)](https://github.com/Hewuliu/TradingAgents-Poe-api)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg?style=flat-square)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](./LICENSE)

</div>

---

> 📌 **Important Notice**: This project makes **NO modifications** to the original [TradingAgents](https://github.com/TauricResearch/TradingAgents) codebase. It only adds support for the Poe platform API, enabling seamless integration with multiple LLM providers (GPT, Claude, Gemini, etc.).

## 📌 Overview

**TradingAgents** is a multi-Agent financial trading framework powered by Large Language Models (LLMs). By integrating the **Poe platform API**, it supports seamless switching between and usage of top-tier models like GPT-4, Claude 3, and Gemini.

This project is built upon the open-source framework [TradingAgents](https://github.com/TauricResearch/TradingAgents), with the following enhancement:

✨ **Core Features:**
- 🤖 **Multi-LLM Support**: Unified access to GPT, Claude, Gemini and more through Poe platform
- 🔄 **Flexible Switching**: Use different LLM providers for different tasks without reconfiguring API keys
- 📊 **Multi-Agent Collaboration**: Includes fundamental analysts, sentiment analysts, technical analysts and more
- 🎯 **Real-time Trading Decisions**: Synthesize multi-agent analysis for intelligent trading decisions
- 🔌 **Easy Integration**: Provides both CLI tool and Python package interfaces
- 🐳 **Docker Support**: One-click containerized deployment

## 🏗️ System Architecture

The framework employs a multi-Agent architecture, simulating real-world trading firm operations:

```
┌─────────────────────────────────────────────────────┐
│                 Data Sources                         │
│  (Alpha Vantage, Yahoo Finance, News feeds)         │
└────────────────────┬────────────────────────────────┘
                     │
        ┌────────────┴────────────┐
        │   Analyst Team (Agents) │
        │  • Fundamentals         │
        │  • Sentiment            │
        │  • News                 │
        │  • Technical            │
        └────────────┬────────────┘
                     │
        ┌────────────┴────────────┐
        │  Research Team (Agents) │
        │  • Bull Researcher      │
        │  • Bear Researcher      │
        │  • Manager              │
        └────────────┬────────────┘
                     │
        ┌────────────┴────────────┐
        │  Trading Decision (Agents)
        │  • Trader               │
        │  • Risk Management      │
        │  • Portfolio Manager    │
        └────────────┬────────────┘
                     │
        ┌────────────┴────────────┐
        │    Trade Execution      │
        │  (Simulated Exchange)   │
        └─────────────────────────┘
```

### Agent Details

#### 📈 **Analyst Team**
- **Fundamentals Analyst**: Analyzes financial statements, profitability, and growth potential
- **Sentiment Analyst**: Evaluates market sentiment through social media and public data
- **News Analyst**: Monitors global news and macroeconomic indicators
- **Technical Analyst**: Utilizes technical indicators (MACD, RSI, etc.) to forecast price movements

#### 🔍 **Research Team**
- **Bull Researcher**: Assesses market opportunities from a positive perspective
- **Bear Researcher**: Evaluates potential risks from a critical perspective
- **Manager**: Synthesizes diverse viewpoints and balances gains against risks

#### 💼 **Trading Execution Layer**
- **Trader**: Makes informed decisions and determines trade timing and magnitude
- **Risk Management**: Assesses market volatility, liquidity, and other risk factors
- **Portfolio Manager**: Final approval/rejection of trading proposals and execution

> ⚠️ **Disclaimer**: This framework is for research and educational purposes only. Trading performance varies based on multiple factors including chosen LLM models, temperature parameters, trading periods, data quality, and more. **This is not financial, investment, or trading advice. Use at your own risk.**

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- Poe account ([poe.com](https://poe.com))
- (Optional) Docker and Docker Compose

### Method 1: Local Installation

**1. Clone the repository**
```bash
git clone https://github.com/Hewuliu/TradingAgents-Poe-api.git
cd TradingAgents
```

**2. Create a virtual environment**
```bash
conda create -n tradingagents python=3.11
conda activate tradingagents
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Configure Poe API**

Get your Poe API key and set environment variables:
```bash
# Windows (PowerShell)
$env:POE_API_KEY="your_poe_api_key"
$env:ALPHA_VANTAGE_API_KEY="your_alpha_vantage_key"

# Linux/Mac
export POE_API_KEY="your_poe_api_key"
export ALPHA_VANTAGE_API_KEY="your_alpha_vantage_key"
```

Or create a `.env` file:
```env
POE_API_KEY=your_poe_api_key
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_key
```

### Method 2: Docker Deployment

**1. Configure environment file**
```bash
cp .env.example .env
# Edit .env and add your POE_API_KEY and ALPHA_VANTAGE_API_KEY
```

**2. Start the container**
```bash
docker compose up -d
```

### 💻 CLI Usage

Launch the interactive command-line interface:
```bash
python -m cli.main
```

Or if installed as a package:
```bash
tradingagents
```

**CLI Features:**
- 🔍 Select stock ticker symbols for analysis
- 📅 Specify analysis date
- 🤖 Choose your LLM (via Poe platform)
  - GPT-4 / GPT-5
  - Claude 3 Opus / Sonnet / Haiku
  - Gemini Pro / Ultra
  - Other Poe-supported models
- 📊 Configure analysis depth and parameters
- 📈 Real-time progress tracking and trading decisions

## 📚 Python API Usage

### Basic Usage

Import and use TradingAgents in your Python code:

```python
from tradingagents.graph.trading_graph import TradingAgentsGraph
from tradingagents.default_config import DEFAULT_CONFIG

# Initialize trading agents
ta = TradingAgentsGraph(debug=True, config=DEFAULT_CONFIG.copy())

# Execute analysis and trading decision
_, decision = ta.propagate("AAPL", "2026-04-01")
print(decision)
```

### Custom Configuration

Modify configuration to use different LLMs and parameters:

```python
from tradingagents.graph.trading_graph import TradingAgentsGraph
from tradingagents.default_config import DEFAULT_CONFIG

config = DEFAULT_CONFIG.copy()

# Poe platform configuration
config["llm_provider"] = "poe"              # Use Poe platform
config["deep_think_llm"] = "claude-3-opus"  # Claude 3 Opus for complex reasoning
config["quick_think_llm"] = "gpt-4-turbo"   # GPT-4 for quick tasks
config["max_debate_rounds"] = 3             # Number of agent debate rounds

# Other optional configurations
config["research_depth"] = "deep"           # Analysis depth: shallow/medium/deep
config["temperature"] = 0.7                 # Model temperature
config["enable_cache"] = True               # Enable caching

ta = TradingAgentsGraph(debug=True, config=config)
_, decision = ta.propagate("NVDA", "2026-04-01")
```

### Supported Models via Poe

Available models through Poe platform:

| Provider | Models | Recommended Use |
|----------|--------|-----------------|
| **OpenAI** | GPT-4, GPT-5 | General analysis, complex reasoning |
| **Anthropic** | Claude 3 (Opus/Sonnet/Haiku) | Long-text processing, deep analysis |
| **Google** | Gemini Pro/Ultra | Multimodal processing, fast responses |
| **Others** | More models | Subject to Poe updates |

See [tradingagents/default_config.py](tradingagents/default_config.py) for all configuration options.

### Project Structure

```
tradingagents/
├── agents/              # Agent implementations
│   ├── analysts/       # Analyst Agents
│   ├── researchers/    # Researcher Agents
│   ├── trader/         # Trader Agent
│   └── risk_mgmt/      # Risk Management Agent
├── dataflows/          # Data flows and sources
│   ├── alpha_vantage*.py
│   ├── y_finance.py
│   └── yfinance_news.py
├── graph/              # LangGraph workflows
│   ├── trading_graph.py
│   ├── signal_processing.py
│   └── propagation.py
├── llm_clients/        # LLM clients (including Poe)
│   ├── base_client.py
│   └── poe_client.py   # ✨ Poe platform integration
└── default_config.py   # Default configuration
```

## 🤝 Contributing

We welcome Issues and Pull Requests! This project accepts contributions of:

- 🐛 Bug fixes
- ✨ New features
- 📚 Documentation improvements
- 🔧 Dependency updates
- 🧪 Test cases

### Submission Process

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📖 FAQ

### Q: How do I get a Poe API key?

**A:** Visit [poe.com](https://poe.com), create an account, and generate your API key in settings.

### Q: Which stock markets are supported?

**A:** Through Alpha Vantage and Yahoo Finance, the framework supports major global markets including US stocks (NYSE, NASDAQ), Hong Kong stocks, and Chinese A-shares.

### Q: How can I customize Agent behavior?

**A:** Edit the corresponding Agent classes in `tradingagents/agents/` or adjust parameters in the configuration.

### Q: Can I use real money for trading?

**A:** Currently, the framework only supports simulated trading. Integrating real trading requires additional risk assessment and compliance handling.

## 📄 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details

## 🙏 Acknowledgments

This project is built upon the open-source [TradingAgents](https://github.com/TauricResearch/TradingAgents) framework. Special thanks to the original contributors.

The Poe platform integration enables flexible, convenient support for multiple LLM providers.

---

<div align="center">

**⭐ If this project helps you, please give it a Star!**

Made with ❤️ by Contributors

</div>
