<div align="center">

# TradingAgents with Poe Integration

**一个强大的多Agent交易框架，集成Poe平台API，支持GPT、Claude、Gemini等多个大模型**

[English](README.md) | [简体中文](README_zh.md)

[![GitHub Stars](https://img.shields.io/github/stars/Hewuliu/TradingAgents-Poe-api?style=flat-square)](https://github.com/Hewuliu/TradingAgents-Poe-api)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg?style=flat-square)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](./LICENSE)

</div>

---

> 📌 **重要声明**：本项目对原开源项目 [TradingAgents](https://github.com/TauricResearch/TradingAgents) 的代码库**没有做任何修改**，仅增加了对 Poe 平台 API 的支持，实现了与多个 LLM 提供商（GPT、Claude、Gemini 等）的无缝集成。

## 📌 项目简介

**TradingAgents** 是一个基于大语言模型（LLM）的多Agent金融交易框架，通过集成 **Poe平台API**，支持快速切换和使用GPT-4、Claude 3、Gemini等多个顶级大模型。

本项目基于开源框架 [TradingAgents](https://github.com/TauricResearch/TradingAgents) 开发，核心增强包括：

✨ **核心特性：**
- 🤖 **多大模型支持**：通过Poe平台统一接入GPT、Claude、Gemini等大模型
- 🔄 **灵活切换**：支持不同任务使用不同的LLM提供商，无需重新配置API密钥
- 📊 **多Agent协作**：包含基本面分析师、情感分析师、技术分析师等多个Agent
- 🎯 **实时交易决策**：综合多个Agent的分析进行智能交易决策
- 🔌 **易于集成**：提供CLI工具和Python包两种使用方式
- 🐳 **Docker支持**：一键启动容器化部署

## 🏗️ 系统架构

该框架采用多Agent架构，模拟真实交易公司的运作流程：

```
┌─────────────────────────────────────────────────────┐
│                 数据来源                             │
│  (Alpha Vantage, Yahoo Finance, 新闻源)             │
└────────────────────┬────────────────────────────────┘
                     │
        ┌────────────┴────────────┐
        │   分析师团队 (Agent)     │
        │  • 基本面分析师          │
        │  • 情感分析师            │
        │  • 新闻分析师            │
        │  • 技术分析师            │
        └────────────┬────────────┘
                     │
        ┌────────────┴────────────┐
        │   研究员团队 (Agent)     │
        │  • 看涨研究员            │
        │  • 看跌研究员            │
        │  • 管理研究员            │
        └────────────┬────────────┘
                     │
        ┌────────────┴────────────┐
        │   交易决策 (Agent)       │
        │  • 交易员                │
        │  • 风险管理              │
        │  • 组合经理              │
        └────────────┬────────────┘
                     │
        ┌────────────┴────────────┐
        │    交易执行              │
        │  (模拟交易所)            │
        └─────────────────────────┘
```

### 各Agent详解

#### 📈 **分析师团队**
- **基本面分析师**：分析公司财务报表、盈利能力、增长潜力
- **情感分析师**：通过社交媒体和公众情绪分析短期市场情绪
- **新闻分析师**：关注全球新闻和宏观经济指标的影响
- **技术分析师**：利用MACD、RSI等技术指标预测价格走势

#### 🔍 **研究员团队**
- **看涨研究员**：从积极角度评估市场机会
- **看跌研究员**：从风险角度评估潜在危险
- **管理研究员**：综合多方观点，平衡收益与风险

#### 💼 **交易执行层**
- **交易员**：根据分析综合判断，确定交易时机和规模
- **风险管理**：评估市场波动性、流动性等风险因素
- **组合经理**：最终审批交易方案，执行投资决策

> ⚠️ **免责声明**：本框架仅用于研究和教育目的。交易性能受多种因素影响，包括选择的大模型、温度参数、交易周期、数据质量等。**非投资建议，使用风险自负。**

## 🚀 快速开始

### 前置条件

- Python 3.10+
- Poe 账号（[poe.com](https://poe.com)）
- （可选）Docker 和 Docker Compose

### 方式一：本地安装

**1. 克隆仓库**
```bash
git clone https://github.com/Hewuliu/TradingAgents-Poe-api.git
cd TradingAgents
```

**2. 创建虚拟环境**
```bash
conda create -n tradingagents python=3.11
conda activate tradingagents
```

**3. 安装依赖**
```bash
pip install -r requirements.txt
```

**4. 配置 Poe API**

获取 Poe API 密钥并设置环境变量：
```bash
# Windows (PowerShell)
$env:POE_API_KEY="your_poe_api_key"
$env:ALPHA_VANTAGE_API_KEY="your_alpha_vantage_key"

# Linux/Mac
export POE_API_KEY="your_poe_api_key"
export ALPHA_VANTAGE_API_KEY="your_alpha_vantage_key"
```

或创建 `.env` 文件：
```env
POE_API_KEY=your_poe_api_key
ALPHA_VANTAGE_API_KEY=your_alpha_vantage_key
```

### 方式二：Docker 部署

**1. 配置环境文件**
```bash
cp .env.example .env
# 编辑 .env，添加你的 POE_API_KEY 和 ALPHA_VANTAGE_API_KEY
```

**2. 启动容器**
```bash
docker compose up -d
```

### 💻 CLI 使用

启动交互式命令行界面：
```bash
python -m cli.main
```

或（如果已安装包）：
```bash
tradingagents
```

**CLI 功能：**
- 🔍 选择要分析的股票代码
- 📅 指定分析日期
- 🤖 选择大模型（通过Poe平台）
  - GPT-4 / GPT-5
  - Claude 3 Opus / Sonnet / Haiku
  - Gemini Pro / Ultra
  - 其他Poe支持的模型
- 📊 配置分析深度和参数
- 📈 实时查看分析进度和交易决策

## 📚 Python API 使用

### 基础使用

在 Python 代码中导入并使用 TradingAgents：

```python
from tradingagents.graph.trading_graph import TradingAgentsGraph
from tradingagents.default_config import DEFAULT_CONFIG

# 初始化交易Agent
ta = TradingAgentsGraph(debug=True, config=DEFAULT_CONFIG.copy())

# 执行分析和交易决策
_, decision = ta.propagate("AAPL", "2026-04-01")
print(decision)
```

### 自定义配置

通过修改配置来使用不同的大模型和参数：

```python
from tradingagents.graph.trading_graph import TradingAgentsGraph
from tradingagents.default_config import DEFAULT_CONFIG

config = DEFAULT_CONFIG.copy()

# Poe 平台配置
config["llm_provider"] = "poe"              # 使用 Poe 平台
config["deep_think_llm"] = "claude-3-opus"  # 复杂推理使用 Claude 3 Opus
config["quick_think_llm"] = "gpt-4-turbo"   # 快速任务使用 GPT-4
config["max_debate_rounds"] = 3             # Agent 辩论轮数

# 其他可选配置
config["research_depth"] = "deep"           # 分析深度: shallow/medium/deep
config["temperature"] = 0.7                 # 模型温度
config["enable_cache"] = True               # 启用缓存

ta = TradingAgentsGraph(debug=True, config=config)
_, decision = ta.propagate("NVDA", "2026-04-01")
```

### Poe 支持的模型

通过 Poe 平台，你可以使用以下大模型：

| 提供商 | 模型 | 推荐用途 |
|--------|------|---------|
| **OpenAI** | GPT-4, GPT-5 | 通用分析、复杂推理 |
| **Anthropic** | Claude 3 (Opus/Sonnet/Haiku) | 长文本处理、深度分析 |
| **Google** | Gemini Pro/Ultra | 多模态处理、快速响应 |
| **其他** | 更多模型 | 根据 Poe 更新 |

详见 [tradingagents/default_config.py](tradingagents/default_config.py) 获取所有配置选项。

### 项目结构

```
tradingagents/
├── agents/              # Agent 实现
│   ├── analysts/       # 分析师 Agents
│   ├── researchers/    # 研究员 Agents
│   ├── trader/         # 交易员 Agent
│   └── risk_mgmt/      # 风险管理 Agent
├── dataflows/          # 数据流和数据源
│   ├── alpha_vantage*.py
│   ├── y_finance.py
│   └── yfinance_news.py
├── graph/              # LangGraph 工作流
│   ├── trading_graph.py
│   ├── signal_processing.py
│   └── propagation.py
├── llm_clients/        # LLM 客户端（包括 Poe）
│   ├── base_client.py
│   └── poe_client.py   # ✨ Poe 平台整合
└── default_config.py   # 默认配置
```

## 🤝 贡献指南

欢迎提交 Issue 和 Pull Request！本项目接受以下类型的贡献：

- 🐛 Bug 修复
- ✨ 新功能开发
- 📚 文档改进
- 🔧 依赖更新
- 🧪 测试用例

### 提交流程

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 📖 常见问题

### Q: 如何获取 Poe API 密钥？

**A:** 访问 [poe.com](https://poe.com)，注册账号后在设置中获取 API 密钥。

### Q: 支持哪些股票市场？

**A:** 通过 Alpha Vantage 和 Yahoo Finance，支持美股（NYSE、NASDAQ）、港股、A股等全球主要市场。

### Q: 如何自定义 Agent 行为？

**A:** 编辑 `tradingagents/agents/` 下的相应 Agent 类，或在配置中调整参数。

### Q: 可以用真实资金交易吗？

**A:** 当前框架仅支持模拟交易。集成真实交易所需要额外的风险评估和合规处理。

## 📄 许可证

本项目采用 MIT License - 详见 [LICENSE](LICENSE) 文件

## 🙏 致谢

本项目基于 [TradingAgents](https://github.com/TauricResearch/TradingAgents) 开源框架开发，感谢原项目的贡献者。

通过 Poe 平台集成，使得多模型支持更加便利和灵活。

---

<div align="center">

**⭐ 如果本项目对你有帮助，请点击 Star！**

Made with ❤️ by Contributors

</div>
