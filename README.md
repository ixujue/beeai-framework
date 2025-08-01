<div align="center">

<h1>BeeAI Framework</h1>

**Build production-ready multi-agent systems in <a href="https://github.com/i-am-bee/beeai-framework/tree/main/python">Python</a> or <a href="https://github.com/i-am-bee/beeai-framework/tree/main/typescript">TypeScript</a>.**

[![Python library](https://img.shields.io/badge/Python-306998?style=plastic&logo=python&logoColor=white)](https://github.com/i-am-bee/beeai-framework/tree/main/python)
[![Typescript library](https://img.shields.io/badge/TypeScript-2f7bb6?style=plastic&logo=typescript&logoColor=white)](https://github.com/i-am-bee/beeai-framework/tree/main/typescript)
[![Apache 2.0](https://img.shields.io/badge/Apache%202.0-License-EA7826?style=plastic&logo=apache&logoColor=white)](https://github.com/i-am-bee/beeai-framework?tab=Apache-2.0-1-ov-file#readme)
[![Follow on Bluesky](https://img.shields.io/badge/Follow%20on%20Bluesky-0285FF?style=plastic&logo=bluesky&logoColor=white)](https://bsky.app/profile/beeaiagents.bsky.social)
[![Join our Discord](https://img.shields.io/badge/Join%20our%20Discord-7289DA?style=plastic&logo=discord&logoColor=white)](https://discord.com/invite/NradeA6ZNF)
[![LF AI & Data](https://img.shields.io/badge/LF%20AI%20%26%20Data-0072C6?style=plastic&logo=linuxfoundation&logoColor=white)](https://lfaidata.foundation/projects/)

</div>

## Latest updates

| Date       | Language      | Update Description                                                                 
|------------|---------------|-------------------------------------------------------------------------------------|
| 2025/06/03 | Python        | Release experimental [Requirement Agent](https://framework.beeai.dev/experimental/requirement-agent).           |
| 2025/05/15 | Python        | New protocol integrations: [ACP](https://framework.beeai.dev/integrations/acp) and [MCP](https://framework.beeai.dev/integrations/mcp).           |
| 2025/02/19 | Python        | Launched Python library alpha. See [getting started guide](https://github.com/i-am-bee/beeai-framework/tree/main#installation).               |
| 2025/02/07 | TypeScript    | Introduced [Backend](https://framework.beeai.dev/modules/backend) module to simplify working with AI services (chat, embedding). |
| 2025/01/28 | TypeScript    | Added support for DeepSeek R1, check out the [Competitive Analysis Workflow example](https://github.com/i-am-bee/beeai-framework/tree/main/typescript/examples/workflows/competitive-analysis). |
| 2025/01/09 | TypeScript    | Introduced [Workflows](https://framework.beeai.dev/modules/workflows), a way of building multi-agent systems. Added support for [Model Context Protocol](https://framework.beeai.dev/modules/tools#mcp-tool). |
| 2024/12/09 | TypeScript    | Added support for LLaMa 3.3. See [multi-agent workflow example using watsonx](https://github.com/i-am-bee/beeai-framework/tree/main/typescript/examples/workflows/multiAgents.ts) or explore [other available providers](https://framework.beeai.dev/modules/backend#supported-providers).        |
| 2024/11/21 | TypeScript    | Added an experimental [Streamlit agent](https://github.com/i-am-bee/beeai-framework/tree/main/typescript/examples/agents/experimental/streamlit.ts). |

For a full changelog, see our [releases page](https://github.com/i-am-bee/beeai-framework/releases).

---

## What is BeeAI Framework?

BeeAI Framework is a comprehensive toolkit for building intelligent, autonomous agents and multi-agent systems. It provides everything you need to create agents that can reason, take actions, and collaborate to solve complex problems.

> [!TIP]
> Get started quickly with the [beeai-framework-py-starter](https://github.com/i-am-bee/beeai-framework-py-starter) [Python] or [beeai-framework-ts-starter](https://github.com/i-am-bee/beeai-framework-ts-starter) [TypeScript] template.

## Key Features

| Feature | Description |
|---------|-------------|
| 🤖 [**Agents**](https://framework.beeai.dev/modules/agents) | Create intelligent agents that can reason, act, and adapt |
| 🔄 [**Workflows**](https://framework.beeai.dev/modules/workflows) | Orchestrate multi-agent systems with complex execution flows |
| 🔌 [**Backend**](https://framework.beeai.dev/modules/backend) | Connect to any LLM provider with unified interfaces |
| 🔧 [**Tools**](https://framework.beeai.dev/modules/tools) | Extend agents with web search, weather, code execution, and more |
| 🔍 [**RAG**](https://framework.beeai.dev/modules/rag) | Build retrieval-augmented generation systems with vector stores and document processing |
| 📝 [**Templates**](https://framework.beeai.dev/modules/templates) | Build dynamic prompts with enhanced Mustache syntax |
| 🧠 [**Memory**](https://framework.beeai.dev/modules/memory) | Manage conversation history with flexible memory strategies |
| 📊 **Observability** | Monitor agent behavior with [events](), [logging](), and robust [error handling]() |
| 🚀 [**Serve**](https://framework.beeai.dev/modules/serve) | Host agents in servers with support for multiple protocols such as [A2A](https://framework.beeai.dev/integrations/a2a) and [MCP](https://framework.beeai.dev/integrations/mcp) |
| 💾 [**Cache**](https://framework.beeai.dev/modules/cache) | Optimize performance and reduce costs with intelligent caching |
| 💿 [**Serialization**](https://framework.beeai.dev/modules/serialization) | Save and load agent state for persistence across sessions |

## Quickstart

### Installation

To install the Python library:
```shell
pip install beeai-framework
```

To install the TypeScript library:
```shell
npm install beeai-framework
```

## Multi-Agent Workflow Example

```py
import asyncio
from beeai_framework.backend.chat import ChatModel
from beeai_framework.tools.search.wikipedia import WikipediaTool
from beeai_framework.tools.weather.openmeteo import OpenMeteoTool
from beeai_framework.workflows.agent import AgentWorkflow, AgentWorkflowInput

async def main() -> None:
    llm = ChatModel.from_name("ollama:granite3.3:8b")
    workflow = AgentWorkflow(name="Smart assistant")

    workflow.add_agent(
        name="Researcher",
        role="A diligent researcher.",
        instructions="You look up and provide information about a specific topic.",
        tools=[WikipediaTool()],
        llm=llm,
    )

    workflow.add_agent(
        name="WeatherForecaster",
        role="A weather reporter.",
        instructions="You provide detailed weather reports.",
        tools=[OpenMeteoTool()],
        llm=llm,
    )

    workflow.add_agent(
        name="DataSynthesizer",
        role="A meticulous and creative data synthesizer",
        instructions="You can combine disparate information into a final coherent summary.",
        llm=llm,
    )

    location = "Saint-Tropez"

    response = await workflow.run(
        inputs=[
            AgentWorkflowInput(
                prompt=f"Provide a short history of {location}.",
            ),
            AgentWorkflowInput(
                prompt=f"Provide a comprehensive weather summary for {location} today.",
                expected_output="Essential weather details such as chance of rain, temperature and wind. Only report information that is available.",
            ),
            AgentWorkflowInput(
                prompt=f"Summarize the historical and weather data for {location}.",
                expected_output=f"A paragraph that describes the history of {location}, followed by the current weather conditions.",
            ),
        ]
    ).on(
        "success",
        lambda data, event: print(
            f"\n-> Step '{data.step}' has been completed with the following outcome.\n\n{data.state.final_answer}"
        ),
    )

    print("==== Final Answer ====")
    print(response.result.final_answer)


if __name__ == "__main__":
    asyncio.run(main())
```

_Source: [python/examples/workflows/multi_agents_simple.py](https://github.com/i-am-bee/beeai-framework/tree/main/python/examples/workflows/multi_agents.py)_

> [!TIP]
> TypeScript version of this example can be found [here](https://github.com/i-am-bee/beeai-framework/tree/main/typescript/examples/workflows/multiAgents.ts).

### Running the example

> [!Note]
>
> To run this example, be sure that you have installed [ollama](https://ollama.com) with the [granite3.3:8b](https://ollama.com/library/granite3.3:8b) model downloaded.

To run projects, use:

```shell
python [project_name].py
```

Explore more in our examples for [Python](https://github.com/i-am-bee/beeai-framework/tree/main/python/examples/README.md) and [TypeScript](https://github.com/i-am-bee/beeai-framework/tree/main/typescript/examples/README.md).

---

## Contribution guidelines

BeeAI framework is open-source and we ❤️ contributions.<br>

To help build BeeAI, take a look at our:
- [Python contribution guidelines](https://github.com/i-am-bee/beeai-framework/tree/main/python/CONTRIBUTING.md)
- [TypeScript contribution guidelines](https://github.com/i-am-bee/beeai-framework/tree/main/typescript/CONTRIBUTING.md)

## Bugs

We use GitHub Issues to manage bugs. Before filing a new issue, please check to make sure it hasn't already been logged. 🙏

## Code of conduct

This project and everyone participating in it are governed by the [Code of Conduct](https://github.com/i-am-bee/beeai-framework/tree/main./CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please read the [full text](https://github.com/i-am-bee/beeai-framework/tree/main./CODE_OF_CONDUCT.md) so that you know which actions may or may not be tolerated.

## Legal notice

All content in these repositories including code has been provided by IBM under the associated open source software license and IBM is under no obligation to provide enhancements, updates, or support. IBM developers produced this code as an open source project (not as an IBM product), and IBM makes no assertions as to the level of quality nor security, and will not be maintaining this code going forward.

## Maintainers

For information about maintainers, see [MAINTAINERS.md](https://github.com/i-am-bee/beeai-framework/blob/main/MAINTAINERS.md).

## Contributors

Special thanks to our contributors for helping us improve BeeAI framework.

<a href="https://github.com/i-am-bee/beeai-framework/graphs/contributors">
  <img alt="Contributors list" src="https://contrib.rocks/image?repo=i-am-bee/beeai-framework" />
</a>

---

Developed by contributors to the BeeAI project, this initiative is part of the [Linux Foundation AI & Data program](https://lfaidata.foundation/projects/). Its development follows open, collaborative, and community-driven practices.
