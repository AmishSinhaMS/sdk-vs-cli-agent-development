# SDK vs CLI: What's Preferred for Agent‑Native Development?

*A developer's guide to choosing the right approach for building and operating AI agents — April 2026*

---

## Introduction

Something fundamental has shifted in how developers interact with AI. We've moved beyond prompting models for text completions. In 2026, AI agents — systems that can plan, execute multi-step tasks, use tools, and operate autonomously — are becoming a core part of the development stack.

This shift introduces a question that didn't exist two years ago:

> **When I need an agent, should I build one with an SDK, or use one through a CLI?**

The answer isn't "one or the other." These approaches serve different purposes, target different stages of the development lifecycle, and complement each other in ways that aren't immediately obvious.

This post breaks down both approaches — what they are, when to use each, how they intersect through the Model Context Protocol (MCP), and how the most productive teams combine them into a compound workflow.

---

## The Problem Space

Agent-native development means building software where AI agents are first-class participants — not just generating text, but executing actions, managing state, coordinating with other agents, and operating with varying degrees of autonomy.

This creates two distinct needs:

1. **Building agent products** — services that run in production, serve users, and scale. Think customer support bots, document processing pipelines, or voice agents.

2. **Using agents as tools** — leveraging an AI agent in your terminal to do your own work faster. Think infrastructure provisioning, report building, codebase exploration, or data engineering.

These are fundamentally different activities, and they call for different tooling.

---

## What Each Approach Actually Does

### SDK: You Write the Agent

With an SDK, you author the agent's logic in code. You define the models, tools, orchestration patterns, and deployment infrastructure. The result is a deployable service.

```python
# Microsoft Foundry Agent Service — Python SDK
from azure.ai.projects import AIProjectClient

client = AIProjectClient.from_connection_string(conn_str)
agent = client.agents.create_agent(
    model="gpt-4o",
    name="sales-analyst",
    instructions="Analyze sales data and generate actionable reports.",
    tools=[
        {"type": "code_interpreter"},
        {"type": "file_search"}
    ]
)
thread = client.agents.create_thread()
client.agents.create_message(
    thread_id=thread.id,
    role="user",
    content="What were our top products by revenue last quarter?"
)
run = client.agents.create_and_process_run(
    thread_id=thread.id,
    agent_id=agent.id
)
```

You control every layer: model selection, tool definitions, memory management, error handling, and deployment topology. The output is a production service.

### CLI: You Use the Agent

With a CLI agent, you describe a goal in natural language, and the agent plans and executes the work:

```
$ copilot
> Create a lakehouse called "SalesLH" in my Fabric workspace,
  upload these 4 CSV files, load them as delta tables, then
  build a semantic model with relationships and publish a report.
```

The agent decomposes this into API calls, file operations, and verification steps. It handles authentication, error recovery, and progress tracking. You review and approve at key checkpoints.

The output isn't code you wrote — it's completed infrastructure, published artifacts, and working systems.

---

## Side-by-Side Comparison

| Dimension | SDK | CLI Agent |
|-----------|-----|-----------|
| **Your role** | Agent developer | Agent user |
| **Output** | Deployable service or API | Completed tasks and artifacts |
| **Runtime** | Cloud infrastructure (Azure, AWS, etc.) | Your terminal session |
| **Target users** | Your customers / end users | You, the developer |
| **Scalability** | Horizontal — serves millions | Single user, single session |
| **Customization** | Unlimited — you write the logic | Plugin and skill ecosystems |
| **Learning curve** | High (code + infra + MLOps) | Low (natural language) |
| **Production readiness** | Designed for production | Designed for developer productivity |
| **Tool calling** | You define tools programmatically | Pre-built tools + MCP servers |
| **Multi-model support** | You implement model routing | Built-in model switching |
| **Observability** | You instrument (App Insights, traces) | Session logs and checkpoints |
| **Cost model** | Compute + token consumption | Subscription-based |

---

## When to Use an SDK

Use an SDK when you are **building an agent that other people will use** — a product, a service, or an automated pipeline that runs in production.

### Scenarios that call for an SDK

| Scenario | Why SDK |
|----------|---------|
| Customer support chatbot with escalation logic | Needs deployment, SLAs, conversation memory |
| Multi-agent RAG pipeline with retrieval + synthesis | Requires orchestration, tool chaining, state management |
| Voice agent for a contact center | Real-time streaming, telephony integration, latency SLAs |
| Document processing at scale (10K+ items/day) | Batch orchestration, error handling, monitoring |
| AI copilot embedded in your SaaS application | Must run inside your product's infrastructure |

### The SDK landscape (April 2026)

| Framework | Maintainer | Primary Language | Key Strength |
|-----------|-----------|-----------------|-------------|
| [Microsoft Foundry Agent Service](https://learn.microsoft.com/azure/ai-services/agents/) | Microsoft | Python, C# | Managed hosting, enterprise connections, MCP support |
| [Semantic Kernel](https://github.com/microsoft/semantic-kernel) | Microsoft | .NET, Python, Java | Enterprise orchestration with planners and plugins |
| [AutoGen](https://github.com/microsoft/autogen) | Microsoft | Python | Multi-agent conversation patterns |
| [LangGraph](https://github.com/langchain-ai/langgraph) | LangChain | Python, JavaScript | Stateful agent graphs with persistence |
| [OpenAI Agents SDK](https://github.com/openai/openai-agents-python) | OpenAI | Python | Native Responses API, lightweight |

Each framework has trade-offs in abstraction level, deployment flexibility, and ecosystem maturity. The choice depends on your team's language preference, cloud provider, and orchestration complexity.

---

## When to Use a CLI Agent

Use a CLI agent when you are **using AI to accelerate your own work** — and the work involves commands, APIs, files, and infrastructure that an agent can operate directly.

### Scenarios that call for a CLI agent

| Scenario | Why CLI |
|----------|---------|
| Provision cloud resources (Fabric, Azure, Databricks) | REST API orchestration handled by the agent |
| Build a Power BI report from a semantic model | Layout, data binding, and publishing via commands |
| Explore an unfamiliar codebase | Agent searches, reads, and summarizes across files |
| Debug a failing CI/CD pipeline | Agent reads logs, traces errors, suggests fixes |
| Daily briefing from M365 data (calendar, emails) | Personal productivity, no deployment needed |
| Prototype agent logic before building with SDK | Fast iteration in natural language |

### The CLI agent landscape (April 2026)

| Tool | Maintainer | Default Model | Extensibility |
|------|-----------|---------------|---------------|
| [GitHub Copilot CLI](https://docs.github.com/copilot/concepts/agents/about-copilot-cli) | GitHub | Claude Sonnet 4.5 | Plugin marketplace, MCP, 30+ Fabric skills |
| [Claude Code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview) | Anthropic | Claude Sonnet 4 | MCP servers, custom commands |

Both support sub-agents (parallel task execution), background tasks, and the Model Context Protocol for extensibility. GitHub Copilot CLI adds a plugin marketplace with domain-specific skills for Microsoft Fabric, Power BI, Databricks, and more.

---

## The Compound Pattern: Using Both Together

The most effective teams don't choose between SDK and CLI — they use CLI agents to accelerate the SDK development process itself.

```
┌──────────────────────────────────────────────────────────────┐
│  Phase 1: Explore & Prototype (CLI)                          │
│                                                              │
│  • Explore data sources and APIs in natural language          │
│  • Prototype agent logic without writing boilerplate          │
│  • Test tool integrations interactively                      │
│  • Validate approach before committing to code                │
└─────────────────────────┬────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────────┐
│  Phase 2: Build & Test (CLI + SDK)                           │
│                                                              │
│  • CLI scaffolds the SDK project (files, config, prompts)    │
│  • Developer writes core agent logic in SDK                  │
│  • CLI runs tests, linters, and integration checks           │
│  • CLI manages git workflow (commits, PRs, reviews)          │
└─────────────────────────┬────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────────┐
│  Phase 3: Deploy & Scale (SDK)                               │
│                                                              │
│  • Agent runs in Microsoft Foundry / Container Apps           │
│  • Serves users via API, Teams bot, or embedded UI           │
│  • Scales horizontally with managed infrastructure           │
│  • Monitored via Foundry observability and App Insights      │
└─────────────────────────┬────────────────────────────────────┘
                          │
                          ▼
┌──────────────────────────────────────────────────────────────┐
│  Phase 4: Operate & Iterate (CLI + SDK)                      │
│                                                              │
│  • CLI queries production metrics and logs                   │
│  • CLI helps debug issues and generate fixes                 │
│  • SDK agent is updated and redeployed                       │
│  • Cycle continues                                           │
└──────────────────────────────────────────────────────────────┘
```

### Concrete example

A developer building a sales analytics agent:

1. **CLI** — Uses Copilot CLI to explore a Fabric lakehouse, understand the data model, and prototype DAX queries
2. **CLI** — Generates the Semantic Kernel project scaffold with tool definitions and system prompts
3. **SDK** — Implements the agent logic in Python, connecting to Azure AI Search and the Fabric semantic model
4. **CLI** — Deploys the agent to Azure Container Apps using infrastructure-as-code generated by the agent
5. **SDK** — The deployed agent serves sales teams in a Teams bot, answering revenue questions in natural language
6. **CLI** — When users report slow responses, uses the CLI to trace queries, profile performance, and push a fix

---

## Decision Framework

When deciding between SDK and CLI for a specific task, ask two questions:

### Question 1: Who is the user?

| If the user is... | Use... |
|---|---|
| **You** (the developer) | CLI |
| **Someone else** (customer, colleague, end user) | SDK |

### Question 2: Does it need to run unattended?

| If it runs... | Use... |
|---|---|
| **Once or on-demand** (interactive) | CLI |
| **Continuously in production** (automated) | SDK |

### Combined decision matrix

| | Runs once / on-demand | Runs continuously |
|---|---|---|
| **For me** | ✅ **CLI** | CLI (scheduled) or lightweight SDK |
| **For others** | SDK (API) or CLI (scripted) | ✅ **SDK** |

---

## MCP: The Bridge Between Both Worlds

The [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) deserves special attention because it's the shared extensibility layer across both approaches.

MCP defines a standard interface for tools that AI agents can call. An MCP server is a tool provider — it exposes capabilities (read a database, call an API, manage a resource) through a protocol that any MCP-compatible agent can consume.

**Why this matters:**

- **Build once, use everywhere.** A custom MCP server for your internal APIs works with both SDK agents (Microsoft Foundry supports MCP natively) and CLI agents (Copilot CLI and Claude Code both support MCP).
- **Decouples tools from agents.** Your tool logic doesn't depend on a specific framework. Switch from Semantic Kernel to LangGraph? Your MCP servers still work.
- **Community ecosystem.** The growing library of open-source MCP servers means less custom tool code for common integrations.

If you're investing in agent tooling, MCP is the abstraction layer worth building on.

---

## The Agent-Native Maturity Model

Teams typically evolve through these stages:

| Stage | Description | Primary Tool |
|-------|-------------|-------------|
| **1. Prompting** | Using ChatGPT/Copilot Chat for one-off questions | Browser / IDE chat |
| **2. CLI Agents** | Using terminal agents for multi-step developer tasks | Copilot CLI, Claude Code |
| **3. SDK Prototypes** | Building simple agents with frameworks | Semantic Kernel, LangGraph |
| **4. Production Agents** | Deploying scaled agent services | Microsoft Foundry, managed infra |
| **5. Agent Platforms** | Multi-agent systems with governance and observability | Foundry + MCP + enterprise policies |

Most teams in 2026 are between stages 2 and 3. The compound pattern (CLI + SDK) is the fastest path from 2 to 4.

---

## Conclusion

SDK and CLI are not competing approaches — they are complementary tools for different stages of the agent development lifecycle.

**Use a CLI agent when:**
- You need to get work done in your terminal
- You're prototyping, exploring, or operating infrastructure
- The "user" of the agent is you

**Use an SDK when:**
- You're building an agent product for others
- The agent needs to run autonomously in production
- You need horizontal scaling, monitoring, and governance

**Use both when:**
- You're a developer building production agents (which is most of us)
- CLI accelerates your development workflow
- SDK powers your production deployments

The developers who are most productive in the agentic era are not choosing one over the other. They are fluent in both, and they use MCP as the shared tool layer that connects them.

Start with the CLI. Graduate to the SDK. Keep both in your workflow.

---

## Further Reading

| Resource | Link |
|----------|------|
| Microsoft Foundry Agent Service | [learn.microsoft.com/azure/ai-services/agents](https://learn.microsoft.com/azure/ai-services/agents/) |
| Semantic Kernel | [github.com/microsoft/semantic-kernel](https://github.com/microsoft/semantic-kernel) |
| AutoGen | [github.com/microsoft/autogen](https://github.com/microsoft/autogen) |
| GitHub Copilot CLI | [docs.github.com/copilot](https://docs.github.com/copilot/concepts/agents/about-copilot-cli) |
| Claude Code | [docs.anthropic.com/claude-code](https://docs.anthropic.com/en/docs/agents-and-tools/claude-code/overview) |
| Model Context Protocol | [modelcontextprotocol.io](https://modelcontextprotocol.io/) |
| Skills for Fabric (CLI Plugin) | [github.com/microsoft/skills-for-fabric](https://github.com/microsoft/skills-for-fabric) |
| Microsoft Foundry Agent Samples | [github.com/Azure-Samples/ai-foundry-agents-samples](https://github.com/Azure-Samples/ai-foundry-agents-samples) |
| Microsoft AI Decision Framework | [github.com/microsoft/Microsoft-AI-Decision-Framework](https://github.com/microsoft/Microsoft-AI-Decision-Framework) |

---

*All guides are written from personal experience and may need adjustments for your specific environment.*

*Last updated: April 2026*
