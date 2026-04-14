<p align="center">
  <h1 align="center">SDK vs CLI: What's Preferred for Agent‑Native Development?</h1>
</p>

<p align="center">
  <em>A developer's guide to choosing the right approach for building and operating AI agents in 2026</em>
</p>

<p align="center">
  <a href="blog/sdk-vs-cli-agent-development.md"><img src="https://img.shields.io/badge/📖_Read_the_Blog_Post-blue?style=for-the-badge" alt="Read Blog"></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/AI_Agents-2026-purple?style=flat-square" alt="AI Agents 2026">
  <img src="https://img.shields.io/badge/Microsoft_Foundry-0078D4?style=flat-square&logo=microsoft" alt="Microsoft Foundry">
  <img src="https://img.shields.io/badge/GitHub_Copilot_CLI-000?style=flat-square&logo=github" alt="GitHub Copilot CLI">
  <img src="https://img.shields.io/badge/Semantic_Kernel-512BD4?style=flat-square" alt="Semantic Kernel">
  <img src="https://img.shields.io/badge/MCP_Protocol-00A67E?style=flat-square" alt="MCP">
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="License">
</p>

---

## 🤔 The Question

The agentic AI era has introduced a fundamental choice for developers:

> **Should I build agents with an SDK, operate through a CLI agent, or both?**

This repository contains a deep-dive technical blog post that breaks down the trade-offs, use cases, and architectural implications of each approach — and shows how the most productive teams combine both.

---

## 📖 What's Inside

| File | Description |
|------|-------------|
| [`blog/sdk-vs-cli-agent-development.md`](blog/sdk-vs-cli-agent-development.md) | The full blog post — ~3,000 words, structured for developers |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | How to contribute feedback, corrections, or additional perspectives |
| [`LICENSE`](LICENSE) | MIT License |

---

## 🎯 Who Is This For?

- **Platform engineers** evaluating agent infrastructure strategies
- **Application developers** building AI-powered products with Microsoft Foundry, Semantic Kernel, or LangGraph
- **Data engineers & analysts** using CLI agents (Copilot CLI, Claude Code) for Fabric, Power BI, and data workflows
- **Engineering leaders** making build-vs-buy decisions for agent capabilities
- **Anyone curious** about where agentic AI development is heading

---

## 💡 Key Takeaways

```
┌─────────────────────────────────────────────────┐
│                                                 │
│   SDK  = Build agents for others                │
│   CLI  = Use agents for yourself                │
│   Both = Ship faster, operate smarter           │
│                                                 │
└─────────────────────────────────────────────────┘
```

| Approach | Best For | Example Tools |
|----------|----------|---------------|
| **SDK** | Production agent services (chatbots, pipelines, voice agents) | Microsoft Foundry, Semantic Kernel, LangGraph, AutoGen |
| **CLI** | Developer productivity (infra setup, code gen, data engineering) | GitHub Copilot CLI, Claude Code |
| **MCP** | Bridge between both — reusable tool layer | Model Context Protocol servers |

---

## 🗂️ Blog Post Outline

1. **Introduction** — Why this question matters now
2. **What Each Approach Actually Does** — SDK vs CLI with code examples
3. **Side-by-Side Comparison** — 12 dimensions compared
4. **When to Use an SDK** — Production scenarios and framework landscape
5. **When to Use a CLI Agent** — Developer workflow scenarios
6. **The Compound Pattern** — Using both together (the winning strategy)
7. **Decision Framework** — Two questions to decide
8. **MCP as the Bridge** — Why it matters for extensibility
9. **The Agent-Native Maturity Model** — Where teams evolve over time
10. **Conclusion** — Practical recommendations

**👉 [Read the full post →](blog/sdk-vs-cli-agent-development.md)**

---

## 🌐 The Landscape (April 2026)

### SDK Frameworks

| Framework | Maintainer | Language | Focus |
|-----------|-----------|----------|-------|
| [Microsoft Foundry Agent Service](https://learn.microsoft.com/azure/ai-services/agents/) | Microsoft | Python, C# | Managed agent hosting with MCP |
| [Semantic Kernel](https://github.com/microsoft/semantic-kernel) | Microsoft | .NET, Python, Java | Enterprise agent orchestration |
| [AutoGen](https://github.com/microsoft/autogen) | Microsoft | Python | Multi-agent conversation patterns |
| [LangGraph](https://github.com/langchain-ai/langgraph) | LangChain | Python, JS | Stateful agent graphs |
| [OpenAI Agents SDK](https://github.com/openai/openai-agents-python) | OpenAI | Python | Responses API native |

### CLI Agents

| Tool | Maintainer | Default Model | Extensibility |
|------|-----------|---------------|---------------|
| [GitHub Copilot CLI](https://docs.github.com/copilot/concepts/agents/about-copilot-cli) | GitHub | Claude Sonnet 4.5 | Plugin marketplace + MCP |
| [Claude Code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview) | Anthropic | Claude Sonnet 4 | MCP servers |

### CLI Plugin Ecosystems

| Plugin | Focus | Skills |
|--------|-------|--------|
| [skills-for-fabric](https://github.com/microsoft/skills-for-fabric) | Microsoft Fabric | 30+ skills |
| [power-bi-agentic-development](https://github.com/data-goblin/power-bi-agentic-development) | Power BI | 6 plugins |
| [databricks-agent-skills](https://github.com/databricks/databricks-agent-skills) | Databricks | 7 skills |

---

## 🤝 Contributing

This is a living document. The agent landscape moves fast — contributions, corrections, and alternative perspectives are welcome.

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for guidelines.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

<p align="center">
  <em>All guides are written from personal experience and may need adjustments for your specific environment.</em>
</p>
