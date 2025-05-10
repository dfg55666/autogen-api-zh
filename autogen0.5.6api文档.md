AutoGen 0.5.6 中文开发文档
本文档旨在为开发者提供一份详尽的 AutoGen 0.5.6 版本中文开发指南。基于官方代码库 https://github.com/microsoft/autogen 及相关文档，深入剖析其 API 设计、核心组件、函数参数及实际应用范例，助力开发者快速掌握并高效运用 AutoGen 0.5.6 构建强大的多智能体应用。
1. AutoGen 0.5.6 概述
AutoGen 作为一个强大的开源框架，致力于简化和加速基于大型语言模型（LLM）的多智能体应用的开发过程。它使开发者能够构建可以自主协作或与人类用户协同工作的复杂AI系统。
1.1 AutoGen 简介
AutoGen 是一个旨在通过组合多个智能体（Agent）以对话方式协同完成任务，从而构建 LLM 应用的开源框架。这些智能体具有高度的可定制性、可对话性，并且能够在多种模式下运行，灵活运用 LLM、人工输入和外部工具。AutoGen 的核心价值在于其提供了一套通用的基础设施，使得开发者能够便捷地为不同应用场景创建具有特定行为和对话模式的智能体系统，无论是通过自然语言还是代码进行定义。
AutoGen 不仅仅局限于构建完全自主的AI系统，其设计同样重视人类在循环中的作用。智能体可以“与人类协同工作”，或在其决策过程中整合“人工输入”。这种对人机协作的内置支持，极大地扩展了 AutoGen 的适用范围。对于那些完全自动化尚不可行或不理想的复杂任务，人类的判断力、创造力或干预能力变得至关重要。AutoGen 的这种灵活性，允许开发者根据具体需求，构建从需要最少人工监督到人类深度参与的各种智能体应用。
1.2 核心理念与架构
AutoGen 的设计哲学基于两大核心理念：“可对话智能体”（Conversable Agents）和“对话式编程”（Conversation Programming）。
●可对话智能体 (Conversable Agents)：AutoGen 中的智能体是具有特定角色的实体，它们能够发送和接收消息，从而发起或参与对话。每个智能体都维护着基于其收发消息的内部上下文。这些智能体是高度可定制的，其能力可以由大型语言模型（LLM）、人工输入或外部工具（或它们的组合）提供支持。开发者可以通过配置或扩展内置功能，轻松创建具有不同职责和能力的智能体。
●对话式编程 (Conversation Programming)：这一编程范式简化并统一了复杂 LLM 应用的开发过程，将其视为多智能体之间的对话。它主要包含两个步骤：(1) 定义一组具有特定能力和角色的可对话智能体；(2) 通过以对话为中心的计算和控制来编排智能体间的交互行为。这种方法使得复杂工作流的定义和理解更为直观。
为了满足不同开发者的需求，AutoGen 采用了分层且可扩展的架构设计。这种架构使得开发者可以根据项目的复杂度和对控制粒度的要求，在不同抽象层次上使用该框架：
1.核心 API (Core API)：实现了消息传递、事件驱动的智能体以及本地和分布式运行时，提供了极高的灵活性和强大的功能。它甚至支持.NET 和 Python 之间的跨语言互操作。这一层主要面向需要深度定制和细粒度控制的研究人员或高级开发者。
2.AgentChat API：在核心 API 之上构建，提供了一个更简洁但更具主张性的 API，专为快速原型设计而优化。此 API 更接近早期版本（如 v0.2）用户所熟悉的模式，并原生支持常见的的多智能体交互模式，例如双智能体聊天或群聊。它适用于希望快速迭代和构建对话式应用的开发者。
3.扩展 API (Extensions API)：允许第一方和第三方扩展持续丰富框架的功能。它支持 LLM 客户端（如 OpenAI、Azure OpenAI）的具体实现，以及代码执行等增强能力。通过扩展 API，社区可以贡献新的集成和功能，而无需修改核心框架。
这种分层设计确保了 AutoGen 既能提供底层操作的强大能力，又能提供高层抽象的便捷性，从而服务于广泛的用户群体和应用场景。
1.3 AutoGen 0.5.6 的主要特性与改进
AutoGen 0.5.6 版本（发布于2025年5月2日，基于提交 880a225cb2046284b612b7499bb21b957c0ca583）在前序版本的基础上，引入了一系列重要的新特性和改进，显著增强了工作流控制的灵活性和智能体的个体能力：
●基于图的执行功能 (GraphFlow)：此版本引入了 GraphFlow 和 DiGraphBuilder，允许开发者使用有向图来定义和执行复杂的、非线性的多智能体工作流。这是一个重大的进步，使得智能体之间的交互可以超越简单的顺序或轮询模式，实现如扇出扇入等更高级的协作模式。
●SelectorGroupChat 增强：SelectorGroupChat 现在支持在内部选择提示（select_prompt）时使用流式输出，这对于需要逐步推理或生成较长内容的场景非常有用。
●CodeExecutorAgent 自我调试：为 CodeExecutorAgent 添加了自我调试循环。这意味着当代码执行出错时，该智能体可以尝试自行修正错误并重试，提高了代码执行的健壮性。
●结构化消息 (StructuredMessage)：引入了 StructuredMessage 类型，并使用类层次结构来组织 AgentChat 的消息类型。StructuredMessage 允许在智能体之间传递结构化的数据（例如 Pydantic 模型），而不仅仅是文本，这对于需要精确数据交换和工具调用的场景至关重要，使得智能体间的通信更加可靠和易于机器解析。
●新增扩展：此版本添加了如 autogen-oaiapi 和 autogen-contextplus 等扩展。其中，autogen-contextplus 提供了高级的模型上下文实现，能够自动总结和截断智能体使用的模型上下文，有助于管理长对话历史并优化成本。
这些更新共同提升了 AutoGen 在构建复杂、可控且功能强大的多智能体应用方面的能力，为开发者提供了更丰富的工具集。
2. 安装与配置
在开始使用 AutoGen 0.5.6 之前，请确保您的开发环境满足基本要求，并按照以下步骤完成安装和基本配置。
2.1 环境要求
●Python 版本：AutoGen 0.5.6 要求 Python 版本为 3.10 或更高。
●Docker (推荐)：对于需要执行由 LLM 生成的代码的场景（例如使用 CodeExecutorAgent 或 DockerCommandLineCodeExecutor），强烈建议安装并运行 Docker。这提供了一个沙箱环境，以确保代码执行的安全性。
2.2 安装 AutoGen 0.5.6
AutoGen 的安装过程体现了其模块化的架构设计。开发者可以根据需要选择安装核心组件、AgentChat 功能包或特定的扩展。
主要的包及其安装命令如下：
●核心库 (autogen-core)：包含 AutoGen 的基础接口和智能体运行时实现。
Bash
pip install autogen-core==0.5.6

( 确认 autogen-core 0.5.6 版本)
●AgentChat 库 (autogen-agentchat)：提供了构建对话式智能体和多智能体协作（如群聊）的上层 API。
Bash
pip install autogen-agentchat==0.5.6

( 确认 autogen-agentchat 0.5.6 版本)
●扩展库 (autogen-ext)：包含与外部服务（如 OpenAI 模型、Azure 服务等）的集成。可以按需安装特定功能的扩展。例如，安装 AgentChat 并集成 OpenAI 客户端：
Bash
pip install "autogen-agentchat[openai]"

或者，如果需要同时安装多个扩展，可以使用逗号分隔：
Bash
pip install "autogen-ext[openai,azure,websurfer]"

( 展示了 autogen-ext[feature] 的安装模式)
●AutoGen Studio (可选)：如果您希望通过图形用户界面（GUI）进行无代码原型设计，可以安装 AutoGen Studio：
Bash
pip install autogenstudio
autogenstudio ui --port 8080 --appdir./myapp

()
这种模块化的安装方式允许开发者根据项目需求选择最合适的组件组合，避免引入不必要的依赖，从而实现更轻量级的部署。
2.3 基本配置
大多数 AutoGen 应用都需要与大型语言模型（LLM）进行交互，这通常需要配置 API 密钥。
●环境变量配置：推荐将 API 密钥等敏感信息存储在环境变量中。AutoGen 的模型客户端通常会自动从标准环境变量（如 OPENAI_API_KEY, AZURE_OPENAI_API_KEY, AZURE_OPENAI_ENDPOINT）中读取这些信息。
●直接在代码中配置：在初始化模型客户端时，也可以直接传入 API 密钥和其他配置参数。例如，配置 OpenAIChatCompletionClient：
Python
from autogen_ext.models.openai import OpenAIChatCompletionClient

client = OpenAIChatCompletionClient(
    model="gpt-4o",  # 或其他模型
    api_key="YOUR_OPENAI_API_KEY"
    # organization="YOUR_ORG_ID", # 可选
    # base_url="YOUR_CUSTOM_API_ENDPOINT" # 可选，用于代理或兼容OpenAI API的服务
)

( 示例了 API 密钥的直接传递)
确保正确配置 LLM 客户端是运行 AutoGen 应用的前提。具体的配置方式和所需参数会因所使用的 LLM 服务提供商而异。
3. AutoGen Core (autogen_core) 深入解析
autogen_core 模块是 AutoGen 框架的基石，它定义了智能体、运行时、消息传递、代码执行、模型交互、工具使用和记忆等核心抽象和基础实现。理解 autogen_core 对于深度定制和扩展 AutoGen 至关重要。
3.1 Agent 与 AgentRuntime (智能体与智能体运行时)
在 AutoGen Core 中，智能体 (Agent) 的行为逻辑与其运行和通信机制 (AgentRuntime) 是解耦的。这种设计带来了高度的模块化和灵活性。
●Agent 协议 (Interface)：autogen_core.Agent 是一个协议类 (Python Protocol)，它定义了一个智能体必须实现的基本接口。任何遵循此协议的对象都可以被视为一个核心智能体，并由 AgentRuntime 管理。关键方法包括处理消息、保存和加载状态等 1。
●BaseAgent 基类：autogen_core.BaseAgent 是 Agent 协议的一个抽象基类实现，为创建具体的智能体提供了一个起点。它处理了一些通用的智能体功能，如ID管理和元数据 1。开发者通常通过继承 BaseAgent 并实现其抽象方法（如 on_message_impl）来创建自定义的核心智能体。
表 1: autogen_core.BaseAgent __init__ 参数

参数名称 (Parameter Name)	类型 (Type)	默认值 (Default Value)	描述 (Description)
description	str	无 (N/A)	智能体的角色或用途描述 1。



**表 2: `autogen_core.Agent` 协议关键方法**


方法 (Method)	描述 (Description)
metadata (property)	返回智能体的元数据。
id (property)	返回智能体的唯一ID。
async on_message(message: Any, ctx: MessageContext) -> Any	智能体的消息处理器，由运行时调用以处理传入消息。
async save_state() -> Mapping[str, Any]	保存智能体的当前状态，返回的状态必须可序列化为JSON。
async load_state(state: Mapping[str, Any]) -> None	从给定的状态映射中加载智能体的状态。
async close() -> None	当智能体运行时关闭时调用，用于执行任何必要的清理操作。
●AgentRuntime (智能体运行时)：autogen_core.AgentRuntime 负责管理智能体的生命周期（创建、注册）和消息的路由与传递。它提供了一个通信基础设施，使得智能体可以专注于其自身的逻辑。SingleThreadedAgentRuntime 是一个本地嵌入式的单线程运行时实现 1。更高级的运行时，如 GrpcWorkerAgentRuntime（通常在 autogen_ext 中提供），可以支持分布式智能体系统。
这种将智能体逻辑与运行时机制分离的设计，不仅增强了模块化程度，使得智能体逻辑更容易独立测试，同时也为未来支持不同类型的运行时环境（例如，从本地单线程切换到分布式多进程/多机器环境）提供了可能性，而无需修改智能体本身的核心代码。
3.2 CodeExecutor (代码执行器)
代码执行是许多 LLM 应用中的关键环节，尤其是在智能体需要生成并运行代码来解决问题或与外部系统交互时。autogen_core.code_executor 模块定义了代码执行器的相关抽象 1。
●CodeExecutor 协议/基类：虽然 autogen_core 本身可能不直接提供一个名为 CodeExecutor 的具体基类（具体实现通常在 autogen_ext 中），但它定义了代码执行器应遵循的接口和核心概念，如执行代码块 (CodeBlock) 并返回结果 (CodeResult) 2。
●具体实现 (通常在 autogen_ext 中)：
○DockerCommandLineCodeExecutor: 这是推荐的代码执行方式，它在 Docker 容器中执行代码，提供了沙箱环境以增强安全性 3。它支持执行 Python 和 shell 脚本。代码块首先被保存到工作目录中的文件，然后在容器内执行这些文件。
○LocalCommandLineCodeExecutor: 允许在本地环境直接执行代码。虽然便捷，但由于 LLM 生成的代码可能存在安全风险，因此不推荐在生产环境或处理不可信代码时使用。
AutoGen 框架对代码执行的安全性给予了高度重视。通过 DockerCommandLineCodeExecutor 提供的容器化执行环境 3，开发者可以有效地隔离 LLM 生成的代码，降低潜在风险。该执行器提供了丰富的配置选项，允许开发者精细控制 Docker 环境，包括使用的镜像、超时设置、工作目录、资源清理等，这对于构建既能利用 LLM 代码生成能力又需确保系统安全的应用至关重要。
表 3: autogen_ext.code_executors.docker.DockerCommandLineCodeExecutor __init__ 主要参数

参数名称 (Parameter Name)	类型 (Type)	默认值 (Default Value)	描述 (Description)
image	str	'python:3-slim'	用于代码执行的 Docker 镜像。
container_name	Optional[str]	None	创建的 Docker 容器的名称；若为 None，则自动生成。
timeout	int	60	代码执行的超时时间（秒）。
work_dir	Union[Path, str]	临时目录	代码执行的工作目录；若为 None，则使用临时目录。
auto_remove	bool	True	若为 True，则在容器停止时自动移除 Docker 容器。
stop_container	bool	True	若为 True，则在调用 stop() 方法、上下文管理器退出或 Python 进程退出时自动停止容器。
delete_tmp_files	bool	False	若为 True，则在执行后删除临时文件。
extra_volumes	Optional]]	None	额外挂载到容器的卷（超越 work_dir）。
init_command	Optional[str]	None	在每次 shell 操作执行前运行的 shell 命令。
DockerCommandLineCodeExecutor 的关键方法包括 async execute_code_blocks(...) 用于执行代码，以及 async start() 和 async stop() 用于管理容器生命周期 3。
3.3 ChatCompletionClient (模型客户端)
与大型语言模型 (LLM) 的交互是 AutoGen 智能体的核心能力之一。autogen_core.models 模块定义了与这些模型通信的客户端抽象 1。
●ChatCompletionClient 协议：这是一个抽象基类（协议），定义了与聊天补全模型交互的标准接口 4。任何具体的模型客户端实现（例如 OpenAI 客户端、Azure OpenAI 客户端）都应遵循此协议。这使得上层智能体代码可以在一定程度上与具体的 LLM 服务解耦。
表 4: autogen_core.models.ChatCompletionClient 协议关键方法/属性

成员 (Member)	类型 (Type)	描述 (Description)
`async create(*messages: Sequence[LLMMessage], tools: Sequence =, json_output: bool	type	None = None, extra_create_args: Mapping[str, Any] = {}, cancellation_token: CancellationToken
`async create_stream(*messages: Sequence[LLMMessage], tools: Sequence =, json_output: bool	type	None = None, extra_create_args: Mapping[str, Any] = {}, cancellation_token: CancellationToken
count_tokens(*messages: Sequence[LLMMessage], tools: Sequence =) -> int	int	计算给定消息序列和工具列表所占用的令牌数量。
capabilities (property)	ModelCapabilities	返回一个 ModelCapabilities 对象，描述该模型客户端所连接的模型支持的特性（例如，是否支持函数调用、JSON 输出、视觉能力等）。
model_info (property)	ModelInfo	返回一个 ModelInfo 对象，包含模型的详细信息，如模型族系（例如 GPT-4, Gemini）、上下文窗口大小等。
total_usage() (property)	RequestUsage	返回自客户端初始化以来模型的总使用量。
async close() -> None	无返回值	关闭客户端并释放其可能持有的任何资源。
●具体实现 (通常在 autogen_ext 中)：AutoGen 通过 autogen_ext 模块提供了对多种流行 LLM 服务的具体客户端实现，例如：
○OpenAIChatCompletionClient (用于 OpenAI API)
○AzureOpenAIChatCompletionClient (用于 Azure OpenAI 服务)
○AnthropicChatCompletionClient (用于 Anthropic Claude 模型)
○OllamaChatCompletionClient (用于本地运行的 Ollama 模型)
AutoGen 的模型客户端系统设计得非常灵活且功能丰富。通过统一的 ChatCompletionClient 协议，开发者可以相对轻松地在不同的 LLM 后端之间切换。此外，框架还内置了对高级功能的支持，如流式响应（通过 create_stream 方法，可用于实时显示模型输出）4、结构化输出（允许模型直接返回符合 Pydantic 模型定义的 JSON 对象），以及响应缓存（通过 autogen_ext.cache_store 中的 ChatCompletionCache、DiskCacheStore、RedisStore 等，可显著减少重复调用的成本和延迟）。这些特性共同构成了一个成熟的 LLM 集成方案。
3.4 Tool 与 FunctionTool (工具与函数工具)
为了让智能体能够执行超越纯文本生成的任务（例如，查询数据库、调用外部 API、执行计算），AutoGen 提供了强大的工具使用机制。autogen_core.tools 模块定义了工具相关的核心抽象 1。
●Tool 协议：定义了工具的基本接口，任何希望被智能体调用的功能单元都应遵循此协议 5。
●BaseTool 抽象基类：是 Tool 协议的一个实现，提供了创建工具的通用结构。它通常需要定义工具的名称、描述、输入参数模式 (args_type) 和返回值类型 (return_type) 5。
●FunctionTool 类：这是一个非常实用的类，可以将任何 Python 函数（同步或异步）包装成一个 AutoGen 工具 5。开发者只需提供函数本身、一个描述（供 LLM 理解何时以及如何使用该工具）以及可选的名称。FunctionTool 会自动从函数的类型注解中推断输入参数的模式。
表 5: autogen_core.tools.FunctionTool __init__ 参数

参数名称 (Parameter Name)	类型 (Type)	默认值 (Default Value)	描述 (Description)
func	Callable]	无 (N/A)	要包装并作为工具公开的 Python 函数。该函数必须对其所有参数和返回类型进行类型注解。
description	str	无 (N/A)	函数用途的描述，详细说明其功能、预期输入以及何时应被调用。此描述对于 LLM 理解和正确使用该工具至关重要。
name	`str	None`	None
global_imports	`Sequence[str	ImportFromModule	Alias]`
strict	bool	False	如果设置为 True，工具的 JSON Schema 将只包含函数签名中明确定义的参数，不允许使用默认值。当与处于结构化输出模式的模型一起使用时，此参数可能需要设置为 True。
FunctionTool 的设计极大地简化了将现有 Python 代码集成为智能体可用工具的过程。开发者无需编写复杂的适配器或解析逻辑，只需专注于实现核心功能并通过清晰的描述将其暴露给 LLM。这种 LLM 的推理能力与 Python 代码的精确执行能力的结合，是 AutoGen 实现复杂任务的关键。
3.5 Memory (记忆组件)
为了使智能体能够在多次交互中保持上下文连贯性、从过去的经验中学习或积累信息，autogen_core.memory 模块提供了记忆组件的基础 1。
●Memory 协议/基类：定义了记忆存储和检索的基本接口。
●ListMemory：一个简单的基于列表的内存实现，按顺序存储消息或记忆内容 2。
这些核心记忆组件为构建有状态的智能体提供了基础。虽然 autogen_core 中的实现可能相对简单（如 ListMemory），但 AutoGen 的可扩展设计允许通过 autogen_ext 模块引入更高级的记忆管理方案。例如，autogen-contextplus 扩展提供了能够自动总结对话历史、截断上下文以适应模型限制等高级功能。这种分层方法——核心提供基础，扩展提供专业化能力——与 AutoGen 的整体框架设计理念保持一致，允许开发者根据应用需求选择或构建合适的记忆系统。
3.6 核心异常 (autogen_core.exceptions)
autogen_core.exceptions 模块定义了框架核心组件可能抛出的特定异常类型，帮助开发者进行更精确的错误处理 1。常见的核心异常包括：
●CantHandleException：当智能体或组件声明无法处理某个特定消息或请求时抛出。
●MessageDroppedException：当消息在传递过程中因某种原因被丢弃时抛出。
●NotAccessibleError：当尝试访问不可达的资源或组件时抛出。
●UndeliverableException：当消息无法传递给指定接收者时抛出。
理解这些核心异常有助于开发者构建更健壮的错误处理逻辑。
3.7 核心日志 (autogen_core.logging)
AutoGen 使用标准的 Python logging 模块进行日志记录，这对于调试智能体行为、追踪消息流和监控 LLM 调用至关重要。
●日志记录器名称：核心事件通常使用名为 autogen_core.EVENT_LOGGER_NAME 的记录器。
●关键事件类型：
○LLMCallEvent：记录有关对 LLM 进行调用的信息，包括输入、输出和潜在的成本。
○MessageEvent：记录与消息传递相关的事件，如消息发送和接收。
○MessageDroppedEvent：当消息被丢弃时记录此事件。
○AgentConstructionExceptionEvent：智能体构建过程中发生异常时记录。
开发者可以通过配置 Python 的 logging 模块来控制 AutoGen 日志的级别和输出目的地，从而有效地进行应用监控和故障排查。
4. AgentChat API (autogen_agentchat) 深入解析
autogen_agentchat API 构建于 autogen_core 之上，提供了一套更高级、更专注于对话场景的抽象，使得构建和管理聊天智能体及其交互变得更加便捷。它封装了许多底层细节，让开发者可以快速搭建常见的的多智能体对话模式。
4.1 BaseChatAgent (基础聊天智能体)
autogen_agentchat.agents.BaseChatAgent 是 AgentChat API 中所有聊天智能体的基类 6。它为具体的聊天智能体（如 AssistantAgent 和 UserProxyAgent）提供了共同的接口和基础功能。
表 6: autogen_agentchat.agents.BaseChatAgent __init__ 参数

参数名称 (Parameter Name)	类型 (Type)	默认值 (Default Value)	描述 (Description)
name	str	无 (N/A)	智能体的名称。此名称用于在团队或多智能体系统中唯一标识该智能体。
description	str	无 (N/A)	对智能体能力、角色或预期行为的描述。此描述可被其他智能体或团队协作机制（如 SelectorGroupChat 中的选择器）用来决定何时与该智能体交互。
BaseChatAgent 的关键方法定义了聊天智能体的核心交互生命周期 6：
●async on_messages(messages: Sequence, cancellation_token: CancellationToken) -> Response：处理传入的消息序列并返回一个响应。这是一个核心方法，子类需要实现具体的处理逻辑。
●async on_messages_stream(messages: Sequence, cancellation_token: CancellationToken) -> AsyncGenerator[...]：以流式方式处理传入消息并产生事件/响应。
●async run(task:... ) -> TaskResult：运行智能体以完成给定任务，并返回最终结果。
●async run_stream(task:... ) -> AsyncGenerator[...]：以流式方式运行智能体处理任务，逐步产生中间消息和最终结果。
●async on_reset(cancellationToken: CancellationToken)：将智能体重置到其初始状态。
●produced_message_types() -> Sequence] (属性)：声明该智能体在其响应中会产生的消息类型。
简单的初始化参数（name 和 description）突出了任何聊天智能体所需的核心身份信息，其中 description 对于其他智能体或选择机制理解其角色尤为重要。
4.2 AssistantAgent (助手智能体)
autogen_agentchat.agents.AssistantAgent 是 AgentChat 中最常用和功能最丰富的智能体之一。它通常由 LLM 驱动，能够进行自然语言对话、调用工具（函数）、执行代码，并根据需要进行反思 6。
AssistantAgent 的设计使其成为一个多面手，能够适应各种复杂任务。其丰富的初始化参数反映了这种多功能性，允许开发者精细调整其行为，包括其连接的 LLM 后端、可用的工具集、系统提示（用于设定其“个性”或角色）、工具使用后的反思行为、输出内容的格式（如结构化输出）以及是否启用流式响应等 6。
表 7: autogen_agentchat.agents.AssistantAgent __init__ 主要参数

参数名称 (Parameter Name)	类型 (Type)	默认值 (Default Value)	描述 (Description)
name	str	无 (N/A)	智能体的名称。
model_client	ChatCompletionClient	无 (N/A)	用于与 LLM 交互的模型客户端实例。
tools	`List, Callable[[...], Any], Callable[[...], Awaitable[Any]]]]	None`	None
workbench	`Workbench	None`	None
system_message	`str	None`	'You are a helpful AI assistant. Solve tasks using your tools. Reply with TERMINATE when the task has been completed.'
reflect_on_tool_use	`bool	None`	None (若设置了 output_content_type 则默认为 True，否则为 False)
output_content_type	`type	None`	None
model_client_stream	bool	False	若为 True，则 model_client 将以流式模式进行调用，允许逐步接收 LLM 的响应。
memory	`Sequence[Memory]	None`	None
handoffs	`List[Handoff	str]	None`
AssistantAgent 的关键方法继承自 BaseChatAgent，包括 on_messages, on_messages_stream, on_reset，并增加了状态保存与加载的方法 async save_state() 和 async load_state() 6。
4.3 UserProxyAgent (用户代理智能体)
autogen_agentchat.agents.UserProxyAgent 在 AutoGen 中扮演着连接人类用户与智能体系统的桥梁角色。它主要用于征求人类输入，或者代表用户执行代码及调用函数 6。
UserProxyAgent 的设计体现了 AutoGen 对人机协作的重视。其核心参数 input_func 允许开发者自定义获取用户输入的方式 6。考虑到现实世界中人类响应可能存在延迟，AutoGen 文档建议结合终止条件（如 HandoffTermination）来优雅地管理这种交互，允许智能体系统在等待用户输入时暂停，并在获得输入后恢复，而不是无限期阻塞 6。这种对实际人机交互场景的细致考虑，是构建实用型人机协同应用的关键。
表 8: autogen_agentchat.agents.UserProxyAgent __init__ 参数

参数名称 (Parameter Name)	类型 (Type)	默认值 (Default Value)	描述 (Description)
name	str	无 (N/A)	智能体的名称。
description	str	'A human user'	对该用户代理智能体的描述。
input_func	`Callable[[str], str]	Callable, Awaitable[str]]	None`
UserProxyAgent 同样继承了 BaseChatAgent 的核心方法。
4.4 消息类型 (autogen_agentchat.messages)
消息是智能体之间通信的载体。autogen_agentchat.messages 模块定义了 AgentChat 中使用的各种消息类型，它们构成了智能体对话的基础 7。AgentChat 的消息系统正朝着更丰富的语义和更强的结构化方向发展，以支持日益复杂的智能体交互。
早期的智能体通信可能主要依赖于简单的文本消息。然而，为了实现更复杂的任务和更可靠的工具交互，结构化数据交换变得至关重要。MultiModalMessage 已经允许在消息中包含图像等多媒体内容 7。而 StructuredMessage 的引入 则更进一步，它允许使用 Pydantic 模型作为消息内容，从而实现了基于模式（schema）强制的数据交换。这种演进支持了更复杂、更可靠的智能体交互逻辑。
表 9: autogen_agentchat.messages 中的主要消息类型

类名 (Class Name)	主要内容字段 (Key Content Fields) & 类型	简要描述 (Brief Description)
BaseMessage	source: str, metadata: Dict[str, str], models_usage: Optional	所有消息类型的基类，包含来源、元数据和模型使用量等通用信息 7。
BaseChatMessage	(继承自 BaseMessage)	聊天消息的基类 7。
TextMessage	content: str	包含纯文本内容的消息 7。
MultiModalMessage	content: List[Union[str, autogen_core.Image]]	多模态消息，其内容可以是文本字符串和/或 autogen_core.Image 对象的列表 7。
StructuredMessage	content: BaseModel (Pydantic 模型)	结构化消息，其内容是一个 Pydantic 模型实例，用于在智能体之间可靠地交换复杂数据。
ToolCallRequestEvent	tool_calls: List	表示一个或多个工具调用请求的事件消息。
ToolCallExecutionEvent	tool_call: ToolCall, result: Any (通常是字符串或结构化数据)	表示工具调用已执行及其结果的事件消息。
HandoffMessage	target: str, context: Optional]	表示将对话控制权移交给另一个智能体的消息。
StopMessage	(通常无特定内容字段，其类型本身即为信号)	指示对话或任务应终止的消息。
AgentEvent	(多种特定事件，如 CodeExecutionEvent, CodeGenerationEvent, ThoughtEvent)	表示智能体内部发生的特定事件的消息，用于观察和调试。
理解这些消息类型及其结构，对于开发者正确解析收到的消息、构造恰当的回复以及设计智能体间的复杂交互至关重要。
4.5 群聊与协作 (autogen_agentchat.teams)
AutoGen 的 AgentChat API 提供了强大的团队（Team）和群聊（Group Chat）管理功能，允许开发者组织多个智能体协同工作，解决更复杂的问题 8。
autogen_agentchat.teams 模块中的类负责协调参与群聊的智能体之间的对话流程、发言顺序和终止条件。0.5.6 版本在群聊和协作方面引入了重要的 GraphFlow 功能，标志着 AutoGen 从主要支持对话流向支持更通用的、基于智能体的计算图的演进。这种演进使得开发者能够定义和执行具有复杂依赖关系和条件分支的多智能体工作流，极大地扩展了 AutoGen 的应用潜力。
以下是一些关键的群聊与协作类：
●BaseGroupChat：作为群聊团队的基类，定义了群聊管理的基本框架。通常与一个 BaseGroupChatManager (一个 SequentialRoutedAgent 的子类) 配合使用 8。
○__init__ 主要参数：participants (参与智能体列表), group_chat_manager_name, group_chat_manager_class, termination_condition, max_turns 8。
●RoundRobinGroupChat：实现了一种简单的轮询发言机制，群聊中的智能体按顺序轮流发言 8。
○__init__ 主要参数：participants, termination_condition, max_turns 8。
●SelectorGroupChat：提供更动态的发言人选择机制。它可以配置为使用 LLM 根据对话历史和预设提示来选择下一位发言者，或者使用开发者提供的自定义函数进行选择 8。0.5.6 版本对此功能进行了增强，例如支持在内部选择提示时使用流式输出。
表 10: autogen_agentchat.teams.SelectorGroupChat __init__ 主要参数

参数名称 (Parameter Name)	类型 (Type)	默认值 (Default Value)	描述 (Description)
participants	List[ChatAgent]	无 (N/A)	参与群聊的 ChatAgent 实例列表。必须至少包含两个名称唯一的智能体。
model_client	ChatCompletionClient	无 (N/A)	用于选择下一位发言者的 ChatCompletion 模型客户端。
selector_prompt	str	预定义的提示模板	用于指导 LLM 选择下一位发言者的提示模板。可用的占位符包括 '{roles}', '{participants}', '{history}'。
allow_repeated_speaker	bool	False	是否允许前一位发言者再次成为下一轮的候选发言人。
max_selector_attempts	int	3	从模型获取有效发言人选择的最大尝试次数。
selector_func	`Callable], str	None]	AsyncCallable`
candidate_func	`Callable], List[str]]	AsyncCallable`	None
emit_team_events	bool	False	是否通过 run_stream() 方法发出团队级别的事件（如 SelectSpeakerEvent）。
model_client_streaming	bool	False	是否为 model_client 启用流式模式，对需要逐步推理的模型有益。
●GraphFlow 和 DiGraphBuilder：这是 0.5.6 版本引入的重量级功能。DiGraphBuilder 用于构建有向图，其中节点通常代表智能体，边代表智能体之间的转换条件或消息流向。GraphFlow 则负责执行这个定义好的图工作流。这使得开发者可以精确控制复杂的多智能体协作逻辑，例如实现条件分支、并行执行（扇出）、结果汇总（扇入）等高级模式。
○DiGraphBuilder 的常用方法包括 add_node(agent_name) 添加智能体节点，以及 add_edge(source_node_name, target_node_name, condition_func) 添加带有转换条件的边。
●Swarm：一种更高级的团队协作模式，通常用于构建能够动态组合和协调大量智能体以解决复杂问题的系统 8。
这些群聊和协作机制为构建从简单的自动化客服到复杂的分布式研究模拟等各种多智能体应用提供了坚实的基础。
4.6 终止条件 (autogen_agentchat.conditions)
在多智能体对话中，有效地控制对话的启停至关重要，以避免无限循环、资源浪费或偏离主题。autogen_agentchat.conditions 模块提供了一系列预定义的终止条件类，以及组合这些条件的机制 9。
终止条件是可调用的对象，它们接收自上次调用以来的消息序列（增量序列），并判断对话是否应终止。如果应终止，则返回一个 StopMessage；否则返回 None。这些条件是状态化的，但在每次运行（通过 run() 或 run_stream()）结束后会自动重置。一个强大的特性是可以使用逻辑与 (&) 和逻辑或 (|) 操作符来组合多个终止条件，从而创建复杂的终止逻辑 9。
这种灵活且可组合的对话控制机制，允许开发者根据具体应用场景精确定义对话的边界和结束时机，例如“在10轮对话后结束，或者当用户说‘停止’时结束，并且某个关键工具已被成功调用”。
表 11: autogen_agentchat.conditions 中的常用终止条件

类名 (Class Name)	__init__ 主要参数 (Key __init__ Parameter(s))	用途 (Purpose)
MaxMessageTermination	max_messages: int	在群聊中总消息数（包括智能体和任务消息）达到指定上限时终止。
TextMentionTermination	text_to_mention: str, sources: Optional[List[str]] = None (指定消息来源)	当指定来源的消息中包含特定文本字符串（例如 "TERMINATE", "APPROVED"）时终止。
TokenUsageTermination	threshold: int, metric: str (如 'total_tokens', 'prompt_tokens')	当 LLM 调用的令牌使用量（提示或补全）达到指定阈值时终止。需要智能体在消息中报告令牌使用情况。
TimeoutTermination	timeout: float (秒)	在指定的持续时间（以秒为单位）过后终止对话。
HandoffTermination	target_agent_name: str (或 target_agent_type: type)	当有智能体请求将控制权移交给特定目标智能体（通过名称或类型指定）时终止。常用于 Swarm 模式或需要外部干预的场景。
SourceMatchTermination	source_agent_name: str (或 source_agent_type: type)	当特定来源的智能体（通过名称或类型指定）响应后终止。
ExternalTermination	(通常通过外部调用其 trigger() 方法)	允许从对话运行外部以编程方式触发终止，例如通过 UI 按钮。
StopMessageTermination	无	当任何智能体在其响应中产生一个 StopMessage 类型的消息时终止。
TextMessageTermination	无	当任何智能体在其响应中产生一个 TextMessage 类型的消息时终止。
FunctionCallTermination	function_name: str	当一个 ToolCallExecutionEvent 消息产生，并且其包含的 FunctionExecutionResult 的名称与指定函数名匹配时终止。用于在特定函数调用成功后结束对话。
FunctionalTermination	condition_func: Callable], bool]	当提供的自定义函数（接收消息序列作为输入）返回 True 时终止。这为创建高度定制化的终止逻辑提供了极大灵活性。
4.7 AgentChat 工具 (autogen_agentchat.tools)
虽然 autogen_core.tools 提供了通用的工具定义（如 FunctionTool），autogen_agentchat.tools 模块可能包含一些特定于 AgentChat 上下文的工具或工具适配器。
●AgentTool：可能用于将一个完整的 ChatAgent 封装成一个可以被其他智能体（尤其是 AssistantAgent）调用的工具。这支持了“嵌套智能体”或“智能体作为工具”的模式，允许构建层次化的智能体结构。
●TeamTool：类似地，可能用于将一个智能体团队（如 RoundRobinGroupChat）封装成一个工具。
这些特定于 AgentChat 的工具抽象，使得更高级别的组合和委托成为可能，进一步增强了多智能体系统的构建能力。
4.8 用户界面 (autogen_agentchat.ui)
为了方便在开发和调试过程中与 AgentChat 应用进行交互，autogen_agentchat.ui 模块提供了一些简单的用户界面组件。
●Console()：一个实用程序类，可以将 AgentChat 的消息流（通常是 AsyncGenerator）打印到控制台，使得开发者可以实时观察智能体之间的对话和事件。
●UserInputManager：可能是一个辅助类，用于管理和处理来自用户的输入，与 UserProxyAgent 配合使用。
这些 UI 组件主要用于开发和演示目的，对于生产级应用，开发者可能需要构建更复杂的用户界面。
4.9 状态管理 (autogen_agentchat.state)
对于复杂的、长时间运行的多智能体交互，状态管理至关重要。autogen_agentchat.state 模块定义了用于捕获和恢复 AgentChat 组件（如智能体和团队）状态的类。
●AssistantAgentState：用于保存和加载 AssistantAgent 的状态。
●BaseGroupChatManagerState：群聊管理器状态的基类。
●TeamState：用于保存和加载整个智能体团队的状态。
●其他特定智能体或团队管理器的状态类，如 RoundRobinManagerState, SelectorManagerState 等。
通过这些状态管理类，开发者可以实现对话的持久化，使得在中断后能够从上次停止的地方继续，或者在不同会话间迁移智能体的状态。
5. AutoGen Extensions (autogen_ext) 详解
autogen_ext 模块是 AutoGen 生态系统的重要组成部分，它提供了一系列与外部服务、库或特定功能集成的具体实现。这些扩展极大地丰富了 AutoGen 的能力，使得开发者可以快速集成常用的 LLM 服务、代码执行环境、工具和数据存储等，而无需从头构建这些集成。
autogen_ext 的设计体现了 AutoGen 的可扩展性理念：核心框架提供稳定的抽象接口，而扩展则负责与不断变化和多样化的外部世界对接。这种方式使得 AutoGen 能够保持核心的简洁性，同时通过社区和官方的努力，不断扩展其支持的服务和功能范围。
autogen_ext 中的组件通常遵循 autogen_core 或 autogen_agentchat 中定义的协议或基类。以下是一些关键的扩展类别及其示例：
5.1 模型客户端扩展 (autogen_ext.models)
此类别包含了对各种大型语言模型服务提供商 API 的具体客户端实现。这些客户端都实现了 autogen_core.models.ChatCompletionClient 协议。
●OpenAIChatCompletionClient (autogen_ext.models.openai)：用于与 OpenAI 的 GPT 系列模型（如 gpt-4o, gpt-3.5-turbo）进行交互。
○__init__ 主要参数：model (模型名称), api_key, organization (可选), base_url (可选，用于代理或兼容 API)。
●AzureOpenAIChatCompletionClient (autogen_ext.models.azure)：用于与 Microsoft Azure OpenAI 服务部署的模型进行交互。
○__init__ 主要参数：model, azure_endpoint, api_key (或使用 Azure AD 认证), api_version。
●AnthropicChatCompletionClient (autogen_ext.models.anthropic)：用于与 Anthropic 的 Claude 系列模型进行交互。
●OllamaChatCompletionClient (autogen_ext.models.ollama)：用于与通过 Ollama 本地运行的开源模型进行交互。
●其他还可能包括对 Gemini, LlamaCpp 等模型的支持 10。
5.2 代码执行器扩展 (autogen_ext.code_executors)
提供了具体的代码执行环境实现，它们通常继承自 autogen_core.code_executor.CodeExecutor（或遵循其接口）。
●DockerCommandLineCodeExecutor (autogen_ext.code_executors.docker)：在 Docker 容器内通过命令行执行代码，是推荐的安全执行方式 3。详细参数已在 3.2 节中介绍。
●DockerJupyterCodeExecutor (autogen_ext.code_executors.jupyter)：在 Docker 容器内通过 Jupyter 内核执行代码，可以支持更丰富的交互和状态保持。
●LocalCommandLineCodeExecutor (autogen_ext.code_executors.local)：在本地机器的命令行环境中执行代码。便捷但存在安全风险，需谨慎使用。
5.3 工具扩展 (autogen_ext.tools)
提供了与特定外部服务或数据源集成的即用型工具。
●AzureAISearchTool (autogen_ext.tools.azure_ai_search)：允许智能体查询 Azure AI Search (认知搜索) 服务，从而访问和检索企业知识库或文档。
○__init__ 主要参数通常包括 Azure AI Search 服务的 endpoint, api_key, index_name 等。
●McpWorkbench (autogen_ext.tools.mcp)：用于与实现了模型上下文协议 (MCP) 的服务器进行交互的工具或工作台。
●可能还包括 LangChain 工具的适配器 (LangChainToolAdapter) 等。
5.4 缓存扩展 (autogen_ext.cache_store)
为了优化 LLM 调用的成本和延迟，autogen_ext 提供了缓存机制的实现。这些通常与 autogen_core.models.ChatCompletionCache 配合使用，后者包装了一个 ChatCompletionClient 实例，并在调用底层客户端之前检查缓存。
●DiskCacheStore (autogen_ext.cache_store.diskcache)：将 LLM 响应缓存到本地磁盘。适用于单机开发或测试环境。
○__init__ 主要参数：cache_path_root (缓存文件的根目录路径)。
●RedisStore (autogen_ext.cache_store.redis)：将 LLM 响应缓存到 Redis 服务器。适用于需要共享缓存的分布式应用或生产环境。
○__init__ 主要参数：redis_client (一个 redis.Redis 实例)。
LLM 调用可能成本高昂且耗时。通过这些缓存扩展，开发者可以显著提高重复查询的响应速度，并减少对 LLM API 的实际调用次数，从而在开发和生产环境中节省时间和金钱。
5.5 其他重要扩展
●运行时扩展 (autogen_ext.runtimes):
○GrpcWorkerAgentRuntime (autogen_ext.runtimes.grpc)：提供了一个基于 gRPC 的分布式智能体运行时，允许智能体在不同的进程或机器上运行和通信，是构建可伸缩多智能体系统的关键组件。
●教学与适应性扩展 (autogen_ext.teachability):
○Teachability (及其相关类如 Apprentice, Grader)：提供让智能体能够从交互中学习或被“教导”的机制，从而逐步改善其性能或适应特定任务。这表明 AutoGen 正朝着更具适应性和可进化性的智能体系统发展。
●认证扩展 (autogen_ext.auth):
○AzureTokenProvider：用于处理 Azure 服务的认证，例如获取 Azure OpenAI 服务的访问令牌 2。
autogen_ext 的存在极大地增强了 AutoGen 的实用性和开箱即用性。通过利用这些预构建的集成，开发者可以将更多精力投入到应用的核心业务逻辑和智能体协作设计上，而不是花费时间在与外部系统的底层连接上。随着社区的发展，可以预见 autogen_ext 的内容会越来越丰富。
6. 实用范例与代码片段
理解 AutoGen 的最佳方式之一是通过实际的代码示例。本节将提供一些基于 AutoGen 0.5.6 特性和 API 的实用范例，展示如何组合不同的组件来构建多智能体应用。官方文档和 GitHub 仓库（如 python/samples 或 examples 目录）通常包含更丰富的示例代码和 Jupyter Notebooks，这些是学习和探索 AutoGen 功能的宝贵资源。
6.1 构建双智能体对话 (AssistantAgent 与 UserProxyAgent)
这是一个基础示例，演示了如何设置一个助手智能体 (AI) 和一个用户代理智能体 (代表人类用户) 进行对话。

Python


import asyncio
from autogen_agentchat.agents import AssistantAgent, UserProxyAgent
from autogen_ext.models.openai import OpenAIChatCompletionClient
from autogen_agentchat.conditions import TextMentionTermination

async def main():
    # 1. 配置 LLM 客户端
    model_client = OpenAIChatCompletionClient(model="gpt-4o", api_key="YOUR_OPENAI_API_KEY")

    # 2. 创建助手智能体
    assistant = AssistantAgent(
        name="assistant",
        model_client=model_client,
        system_message="You are a helpful AI assistant."
    )

    # 3. 创建用户代理智能体
    user_proxy = UserProxyAgent(
        name="user_proxy",
        description="A human user.",
        # human_input_mode="ALWAYS", # 每次都请求人类输入
        # code_execution_config=False, # 禁用代码执行
    )

    # 4. 定义终止条件 (例如，当用户代理说 "exit" 时结束)
    termination_condition = TextMentionTermination(text_to_mention="exit", sources=[user_proxy.name])

    # 5. 发起对话 (这里使用 UserProxyAgent 的 run 方法简化，也可以用 Team)
    # 注意：在实际应用中，更推荐使用 Team (如 RoundRobinGroupChat) 来管理对话流
    # 此处为了简化，直接让 user_proxy 发起任务给 assistant
    # 更规范的做法是 user_proxy.initiate_chat(assistant, message="Your initial task for the assistant.")
    
    # 为了演示，我们假设一个简单的任务
    task = "What is AutoGen?"
    
    # 使用 UserProxyAgent 的 run 方法与 AssistantAgent 交互
    # 这会模拟用户向助手提问，并获取助手的回答
    # 在更复杂的场景中，应该使用 Team 来管理智能体间的对话
    
    # 初始化对话历史
    initial_messages = [
        {"role": "user", "content": task, "name": user_proxy.name} # 模拟用户发起
    ]

    # 运行助手智能体处理初始消息
    # 注意: AssistantAgent.run() 的 task 参数可以直接是字符串或消息列表
    # 为了更清晰地展示交互，我们这里手动构建消息并调用 on_messages
    # response = await assistant.on_messages(
    #     messages=[user_proxy.construct_message(content=task)], 
    #     cancellation_token=None
    # )
    # print(f"Assistant response: {response.chat_message.content}")

    # 更完整的交互通常通过 Team 进行，或者通过 UserProxyAgent.initiate_chat
    # 以下是一个 initiate_chat 的简化示例流程：
    print(f"User Proxy: {task}")
    current_speaker = user_proxy
    message_history = # 用于跟踪对话

    for _ in range(5): # 限制对话轮次
        if current_speaker == user_proxy:
            # 模拟用户发言或获取用户输入
            user_message_content = input("Your message (type 'exit' to end): ") if message_history else task
            if user_message_content.lower() == "exit":
                print("Exiting chat.")
                break
            
            user_message = current_speaker.construct_message(content=user_message_content)
            message_history.append(user_message)
            
            # 将消息发送给助手
            response = await assistant.on_messages(messages=message_history, cancellation_token=None)
            assistant_reply = response.chat_message
            message_history.append(assistant_reply)
            print(f"Assistant: {assistant_reply.content}")
            current_speaker = assistant # 轮到助手发言（虽然这里助手已经回复）
        else: # 实际上，在双向对话中，通常是用户说完，助手回复，然后等待用户再次输入
              # 这里简化了流程，实际应由 UserProxyAgent 处理用户输入逻辑
            print("Waiting for user input...")
            current_speaker = user_proxy
            
    await model_client.close()

if __name__ == "__main__":
    asyncio.run(main())

6.2 实现带工具的智能体 (使用 AssistantAgent 和 FunctionTool)
此示例展示了如何为 AssistantAgent 配备一个自定义工具（一个 Python 函数）。

Python


import asyncio
from autogen_agentchat.agents import AssistantAgent
from autogen_ext.models.openai import OpenAIChatCompletionClient
from autogen_core.tools import FunctionTool
from typing import Annotated # 用于类型注解

# 1. 定义一个 Python 函数作为工具
async def get_current_weather(location: Annotated) -> str:
    """Get the current weather in a given location."""
    # 这是一个模拟函数，实际应用中会调用天气 API
    if "tokyo" in location.lower():
        return "The weather in Tokyo is 15 degrees Celsius and cloudy."
    elif "paris" in location.lower():
        return "The weather in Paris is 18 degrees Celsius and sunny."
    else:
        return f"Sorry, I don't have weather information for {location}."

async def main():
    # 2. 配置 LLM 客户端
    model_client = OpenAIChatCompletionClient(model="gpt-4o", api_key="YOUR_OPENAI_API_KEY")

    # 3. 将函数包装成 FunctionTool
    weather_tool = FunctionTool.from_function(get_current_weather)

    # 4. 创建助手智能体，并注册工具
    assistant_with_tool = AssistantAgent(
        name="weather_assistant",
        model_client=model_client,
        system_message="You are a helpful AI assistant. You can use tools to answer questions. Reply with TERMINATE when the task is done.",
        tools=[weather_tool],
        reflect_on_tool_use=True, # 允许智能体在使用工具后进行反思
        model_client_stream=False # 可以设为 True 以启用流式输出
    )

    # 5. 运行智能体并提出需要使用工具的任务
    task_result = await assistant_with_tool.run(task="What's the weather like in Tokyo?")
    
    # 打印最终回复
    if task_result.messages and task_result.messages[-1].content:
        print(f"Final response from assistant: {task_result.messages[-1].content}")
    else:
        print(f"Assistant task result: {task_result.stop_reason}")

    await model_client.close()

if __name__ == "__main__":
    asyncio.run(main())

6.3 配置和运行群聊 (使用 RoundRobinGroupChat)
此示例演示如何设置一个包含多个智能体的轮询群聊。

Python


import asyncio
from autogen_agentchat.agents import AssistantAgent, UserProxyAgent
from autogen_agentchat.teams import RoundRobinGroupChat
from autogen_agentchat.conditions import MaxMessageTermination
from autogen_ext.models.openai import OpenAIChatCompletionClient

async def main():
    model_client = OpenAIChatCompletionClient(model="gpt-4o", api_key="YOUR_OPENAI_API_KEY")

    # 创建多个智能体
    planner = AssistantAgent(
        name="Planner",
        model_client=model_client,
        system_message="You are a planner. Your role is to create a step-by-step plan to solve a problem. Suggest the next step or person to act."
    )
    coder = AssistantAgent(
        name="Coder",
        model_client=model_client,
        system_message="You are a coder. You write Python code based on the plan. "
                       "Wrap your code in markdown code blocks (```python).",
        # 在实际应用中，Coder Agent 通常会与 CodeExecutorAgent 结合使用
    )
    user_proxy = UserProxyAgent(
        name="User",
        description="A human user providing tasks and feedback.",
        # human_input_mode="TERMINATE" # 在需要时请求人类输入
    )

    # 定义群聊参与者
    participants = [user_proxy, planner, coder]

    # 创建轮询群聊团队
    # 注意：RoundRobinGroupChat 期望 BaseChatAgent 实例
    team = RoundRobinGroupChat(
        participants=participants,
        termination_condition=MaxMessageTermination(max_messages=10) # 最多10条消息后终止
    )

    # 运行群聊任务
    # user_proxy 作为发起者，向团队提出任务
    # 在 RoundRobinGroupChat 中，初始消息通常由列表中的第一个智能体处理或作为任务广播
    # 为了让用户发起，可以将 user_proxy 放在 participants 列表首位，并由其提供初始任务
    initial_task = "Develop a Python script that prints numbers from 1 to 5."
    
    # 使用团队的 run 方法
    # task 可以是字符串，也可以是消息列表
    # 如果 task 是字符串，它会被包装成一个来自 "task" 源的消息
    # 为了让 user_proxy 发起，我们可以构造一个初始消息
    from autogen_agentchat.messages import TextMessage
    initial_message_for_team = TextMessage(source=user_proxy.name, content=initial_task)

    task_result = await team.run(task=[initial_message_for_team])

    print("\n--- Conversation Summary ---")
    for msg in task_result.messages:
        print(f"[{msg.source}]: {msg.content}")
    print(f"Termination reason: {task_result.stop_reason}")

    await model_client.close()

if __name__ == "__main__":
    asyncio.run(main())

6.4 安全执行代码 (使用 DockerCommandLineCodeExecutor)
此示例展示了如何结合 AssistantAgent（用于生成代码）和 CodeExecutorAgent（配置了 DockerCommandLineCodeExecutor）来安全地执行代码。

Python


import asyncio
import tempfile
from autogen_agentchat.agents import AssistantAgent, CodeExecutorAgent
from autogen_ext.models.openai import OpenAIChatCompletionClient
from autogen_ext.code_executors.docker import DockerCommandLineCodeExecutor
from autogen_agentchat.teams import RoundRobinGroupChat # 或者其他团队类型
from autogen_agentchat.conditions import MaxMessageTermination

async def main():
    model_client = OpenAIChatCompletionClient(model="gpt-4o", api_key="YOUR_OPENAI_API_KEY")

    # 1. 创建代码生成智能体
    code_writer = AssistantAgent(
        name="CodeWriter",
        model_client=model_client,
        system_message="You are a helpful AI assistant that writes Python code to solve tasks. "
                       "Wrap the code in markdown code blocks (```python). Reply with TERMINATE when the task is done."
    )

    # 2. 配置 Docker 代码执行器
    work_dir = tempfile.mkdtemp(prefix="autogen_work_")
    print(f"Using Docker work directory: {work_dir}")
    
    # 确保 Docker 服务正在运行
    try:
        docker_executor = DockerCommandLineCodeExecutor(
            work_dir=work_dir,
            timeout=60, # 执行超时时间
            image="python:3-slim" # 使用的 Docker 镜像
        )
    except Exception as e:
        print(f"Failed to initialize DockerCommandLineCodeExecutor: {e}")
        print("Please ensure Docker is installed and running.")
        return


    # 3. 创建代码执行智能体
    code_executor_agent = CodeExecutorAgent(
        name="CodeExecutor",
        code_executor=docker_executor,
        description="An agent that executes Python code blocks provided by other agents in a Docker container."
    )

    # 4. 创建一个简单的团队来协调 CodeWriter 和 CodeExecutor
    # 这里使用 UserProxyAgent 来发起任务
    from autogen_agentchat.agents import UserProxyAgent
    user_proxy = UserProxyAgent(name="User", description="Initiates tasks.")

    team = RoundRobinGroupChat(
        participants=[user_proxy, code_writer, code_executor_agent],
        termination_condition=MaxMessageTermination(max_messages=6) # 限制对话长度
    )
    
    # 5. 运行任务
    task = "Write a Python script to calculate the factorial of 5 and print the result. Then execute it."
    
    from autogen_agentchat.messages import TextMessage
    initial_message_for_team = TextMessage(source=user_proxy.name, content=task)

    task_result = await team.run(task=[initial_message_for_team])

    print("\n--- Conversation Summary ---")
    for msg in task_result.messages:
        # 打印非流式块的消息内容
        if hasattr(msg, 'content') and msg.content is not None:
             print(f"[{msg.source} ({type(msg).__name__})]: {msg.content}")
        elif type(msg).__name__ == "ToolCallExecutionEvent": # 特别处理工具执行结果
             print(f"[{msg.source} ({type(msg).__name__})]: Tool call '{msg.tool_call.function_name}' result: {msg.result}")

    print(f"Termination reason: {task_result.stop_reason}")

    # 清理 Docker 容器和工作目录（如果需要）
    # DockerCommandLineCodeExecutor 默认 auto_remove=True, stop_container=True
    # 手动停止（如果 stop_container=False 或需要提前停止）
    # await docker_executor.stop() # 通常由上下文管理器或 atexit 处理

    await model_client.close()
    # import shutil
    # shutil.rmtree(work_dir) # 清理临时工作目录

if __name__ == "__main__":
    asyncio.run(main())

6.5 使用 GraphFlow 定义复杂工作流
此示例演示如何使用 0.5.6 版本新增的 DiGraphBuilder 和 GraphFlow 来创建一个简单的扇出扇入 (fan-out-fan-in) 工作流。

Python


import asyncio
from autogen_agentchat.agents import AssistantAgent
from autogen_agentchat.teams import DiGraphBuilder, GraphFlow
from autogen_ext.models.openai import OpenAIChatCompletionClient
from autogen_agentchat.messages import TextMessage

async def main():
    model_client = OpenAIChatCompletionClient(model="gpt-4o", api_key="YOUR_OPENAI_API_KEY")

    # 1. 创建智能体
    initiator = AssistantAgent("Initiator", model_client=model_client, system_message="You are the initiator. Start the process.")
    researcher1 = AssistantAgent("Researcher1", model_client=model_client, system_message="You are Researcher 1. Research topic A.")
    researcher2 = AssistantAgent("Researcher2", model_client=model_client, system_message="You are Researcher 2. Research topic B.")
    summarizer = AssistantAgent("Summarizer", model_client=model_client, system_message="You are the summarizer. Combine inputs from researchers.")

    # 2. 使用 DiGraphBuilder 构建工作流图
    builder = DiGraphBuilder()

    # 添加节点 (智能体)
    builder.add_node(initiator)
    builder.add_node(researcher1)
    builder.add_node(researcher2)
    builder.add_node(summarizer)

    # 添加边 (定义流程)
    # Initiator -> Researcher1 AND Initiator -> Researcher2 (扇出)
    builder.add_edge(initiator, researcher1)
    builder.add_edge(initiator, researcher2)

    # Researcher1 -> Summarizer AND Researcher2 -> Summarizer (扇入)
    # GraphFlow 会等待所有入边节点的输出都准备好后，再传递给目标节点
    builder.add_edge(researcher1, summarizer)
    builder.add_edge(researcher2, summarizer)

    # 3. 创建 GraphFlow 团队
    # GraphFlow 期望 BaseChatAgent 实例
    graph_flow_team = GraphFlow(
        graph=builder.build(),
        participants=[initiator, researcher1, researcher2, summarizer]
        # termination_condition 可以根据需要设置
    )

    # 4. 运行 GraphFlow 任务
    initial_task_content = "Research pros and cons of renewable energy vs nuclear energy, then summarize."
    initial_message = TextMessage(source=initiator.name, content=initial_task_content) # 让 Initiator 发起

    # GraphFlow 的 run 方法期望一个消息列表作为 task
    task_result = await graph_flow_team.run(task=[initial_message])
    
    print("\n--- GraphFlow Conversation Summary ---")
    if task_result and task_result.messages:
        for msg in task_result.messages:
            if hasattr(msg, 'content') and msg.content is not None:
                print(f"[{msg.source} ({type(msg).__name__})]: {msg.content}")
            elif type(msg).__name__ == "ToolCallExecutionEvent":
                print(f"[{msg.source} ({type(msg).__name__})]: Tool call '{msg.tool_call.function_name}' result: {msg.result}")
        print(f"Termination reason: {task_result.stop_reason}")
    else:
        print("No messages in task result or task result is None.")


    await model_client.close()

if __name__ == "__main__":
    asyncio.run(main())

这些示例旨在提供一个起点。开发者应参考官方文档和更广泛的示例集，以充分利用 AutoGen 0.5.6 的各项功能。
7. API 参考快速索引
为了方便开发者快速查找特定 API 的详细信息，以下列出了 AutoGen 0.5.6 主要模块和类的参考路径（基于本文档的章节结构）：
●autogen_core (核心 API)
○Agent 协议与 BaseAgent：参见 3.1 节
○AgentRuntime (SingleThreadedAgentRuntime)：参见 3.1 节
○代码执行器 (CodeExecutor 概念, DockerCommandLineCodeExecutor)：参见 3.2 节及 5.2 节
○模型客户端 (ChatCompletionClient 协议)：参见 3.3 节
○工具 (Tool 协议, BaseTool, FunctionTool)：参见 3.4 节
○记忆组件 (Memory, ListMemory)：参见 3.5 节
○核心异常：参见 3.6 节
○核心日志：参见 3.7 节
●autogen_agentchat (AgentChat API)
○BaseChatAgent：参见 4.1 节
○AssistantAgent：参见 4.2 节
○UserProxyAgent：参见 4.3 节
○消息类型 (TextMessage, MultiModalMessage, StructuredMessage 等)：参见 4.4 节
○群聊与协作 (RoundRobinGroupChat, SelectorGroupChat, GraphFlow)：参见 4.5 节
○终止条件 (MaxMessageTermination, TextMentionTermination 等)：参见 4.6 节
○AgentChat 工具 (AgentTool, TeamTool)：参见 4.7 节
○用户界面 (Console, UserInputManager)：参见 4.8 节
○状态管理 (AssistantAgentState, TeamState 等)：参见 4.9 节
●autogen_ext (扩展 API)
○模型客户端扩展 (OpenAIChatCompletionClient, AzureOpenAIChatCompletionClient 等)：参见 5.1 节
○代码执行器扩展 (DockerCommandLineCodeExecutor, DockerJupyterCodeExecutor 等)：参见 5.2 节
○工具扩展 (AzureAISearchTool 等)：参见 5.3 节
○缓存扩展 (DiskCacheStore, RedisStore)：参见 5.4 节
○其他重要扩展 (GrpcWorkerAgentRuntime, Teachability 等)：参见 5.5 节
官方的 API 参考文档（通常位于 https://microsoft.github.io/autogen/0.5.6/reference/index.html 或类似路径）是获取最完整和最新 API 细节的权威来源。
8. 从旧版本迁移
如果开发者正在从 AutoGen 的旧版本（特别是 v0.2.x 系列）迁移到 v0.5.6，可能会遇到一些破坏性更改和 API 调整。AutoGen 的架构自 v0.2 以来经历了显著的重构，引入了更清晰的分层（Core, AgentChat, Extensions）和新的核心抽象。
官方 GitHub 仓库的 README 和文档通常会提供迁移指南的链接。例如，文档中提到：“如果您正在从 AutoGen v0.2 升级，请参阅迁移指南以获取有关如何更新代码和配置的详细说明。”。
主要的迁移关注点可能包括：
●包结构和导入路径的变化：由于引入了 autogen_core, autogen_agentchat, autogen_ext 等命名空间，许多类的导入路径可能已更改。
●智能体类的变化：旧版本中的 ConversableAgent 可能已被 autogen_agentchat.agents.BaseChatAgent 及其子类（如 AssistantAgent, UserProxyAgent）所取代或重构。其 __init__ 参数和核心方法（如消息处理、注册函数/工具）的签名和行为可能有所不同。
●配置 LLM 的方式：旧的 config_list 机制可能已被新的 ChatCompletionClient 抽象所取代。
●工具/函数注册：注册工具和函数给智能体的方式可能已更新，以适应新的 Tool 和 FunctionTool 抽象。
●群聊和工作流管理：旧的群聊管理方式可能已被新的 autogen_agentchat.teams 中的类（如 RoundRobinGroupChat, SelectorGroupChat, GraphFlow）所取代。
建议仔细阅读官方的迁移指南（如果针对 0.5.x 系列已发布）和 v0.5.x 系列的发布说明，以了解具体的 API 变更和推荐的迁移路径。同时，参考新版本的示例代码是理解 API 用法变化的有效方式。
9. 附录
9.1 常见问题解答 (FAQ)
AutoGen 官方 GitHub 仓库通常会维护一个 FAQ 文档 (FAQ.md)，解答开发者在学习和使用过程中可能遇到的常见问题。建议在遇到疑问时首先查阅该文档。
常见问题可能涉及：
●API 密钥配置问题。
●特定模型或服务的集成方法。
●代码执行环境的设置（尤其是 Docker）。
●常见错误的排查。
●框架设计理念的澄清。
9.2 参与贡献
AutoGen 是一个开源项目，欢迎社区的贡献。如果您有兴趣为 AutoGen 的发展做出贡献（无论是代码、文档、示例还是错误报告），请查阅项目根目录下的 CONTRIBUTING.md 文件。该文件通常会详细说明贡献流程、代码风格指南、行为准则以及如何提交拉取请求 (Pull Request)。
社区的积极参与是 AutoGen 不断完善和进步的重要动力。
本文档基于 AutoGen 0.5.6 版本编写，旨在提供全面而准确的开发参考。由于软件版本迭代迅速，建议开发者同时关注官方文档和 GitHub 仓库以获取最新信息。
Works cited
1.autogen_core — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_core.html
2.API Reference — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/index.html
3.autogen_ext.code_executors.docker — AutoGen, accessed May 9, 2025, https://microsoft.github.io/autogen/dev/reference/python/autogen_ext.code_executors.docker.html
4.autogen_core.models — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_core.models.html
5.autogen_core.tools — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_core.tools.html
6.autogen_agentchat.agents — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_agentchat.agents.html
7.autogen_agentchat.messages — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_agentchat.messages.html
8.autogen_agentchat.teams — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_agentchat.teams.html
9.Termination — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/tutorial/termination.html
10.API Reference — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/dev/reference/index.html