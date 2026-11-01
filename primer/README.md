# CommerceFlow · 模型与 Agent 基础示例

本目录演示模型调用、对话记忆、工具执行和工作流编排。每个示例可单独运行，来源见 [项目来源说明](../SOURCES.md)。

## 装环境

项目本身 `uv sync` 装过的，什么都不用再装，在仓库根目录下 `uv run python primer/s1_hello.py` 就能跑。

没装项目、只想跑这几个例子的，Python 3.10 以上，装这几个包（分别用于直接 API 调用和框架示例）：

```bash
pip install openai python-dotenv langchain langchain-openai langgraph
```

LangChain 认 1.x 系列，项目里锁的也是它。

配置跟项目共用仓库根目录的 `.env`，只用到三行，脚本会往上级目录找。只跑这几个例子的，在仓库根目录或 `primer/` 下建一个 `.env` 写这三行也行：

```bash
CHAT_BASE_URL=https://api.deepseek.com/v1
CHAT_API_KEY=sk-你的密钥
CHAT_MODEL=deepseek-v4-flash
```

## 文件

| 文件 | 功能分组 | 演示什么 |
|---|---|---|
| `shop.py` | 共用 | 连模型的客户端，查订单、查物流两个假数据函数 |
| `s1_hello.py` | 模型与记忆 | 在代码里跟大模型说一句话，看回答和 token 账单 |
| `s2_memory.py` | 模型与记忆 | 两次各问各的它记不住，把聊天记录一起发过去就记住了 |
| `s3_tools.py` | 工具与工作流 | 给它一份工具清单，看它回来的 `tool_calls`，执行后把结果还给它 |
| `s4_agent.py` | 工具与工作流 | 工具调用包进循环，它自己先查订单再查物流 |
| `s5_workflow.py` | 工具与工作流 | 同一个问题换成 Workflow，查询顺序由代码写死 |
| `s6_langchain_hello.py` | 框架集成 | 换成 `ChatOpenAI` 说一句话，对照 s1 |
| `s7_prompt_chain.py` | 框架集成 | 提示词模板加 `\|` 串成链 |
| `s8_tool_decorator.py` | 框架集成 | `@tool` 装饰器，打印它自动生成的参数 schema |
| `s9_langchain_agent.py` | 框架集成 | `create_agent` 二十行跑通两步工具链，加 `checkpointer` 就有记忆 |

订单和物流是写死在 `shop.py` 里的假数据，不连数据库。主应用的知识库与会话数据由 MySQL 持久化，订单与物流仍使用模拟数据。
