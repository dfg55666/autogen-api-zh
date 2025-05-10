AutoGen API 参考手册 (v0.5.6) - 中文版
引言 (Introduction)
AutoGen 框架概览 (Overview of the AutoGen Framework)
AutoGen 是一个为开发大型语言模型 (LLM) 应用而设计的框架，尤其擅长构建和管理多智能体对话系统 1。它通过提供可定制的智能体来简化复杂 LLM 工作流的编排、自动化和优化。这些智能体能够基于 LLM、人类输入和工具的组合进行对话和协作。AutoGen 的一个核心设计理念是其分层架构，主要包括核心层 (Core)、AgentChat 层和扩展层 (Extensions) 2。
●核心层 (AutoGen Core): 提供了事件驱动的编程框架，用于构建可扩展的多智能体 AI 系统。它支持异步消息传递、分布式智能体以及跨语言（目前主要是 Python 和.NET）的互操作性 2。这一层为高级用户和需要构建复杂、确定性或动态工作流的开发者提供了最大的灵活性和控制力。
●AgentChat API: 这是一个更高级别的 API，构建于核心层之上。它为快速原型设计提供了更简单、更具指导性的接口，尤其适合初学者或希望快速搭建对话式单智能体或多智能体应用的开发者 4。AgentChat 提供了具有预设行为的智能体和预定义的多智能体设计模式，例如双智能体聊天或群聊。
●扩展 API (AutoGen Extensions): 这是一个不断增长的组件库，包含由 AutoGen 项目维护的以及第三方贡献的对核心 API 和 AgentChat API 组件的具体实现。这些扩展涵盖了 LLM 客户端（如 OpenAI、Azure OpenAI）、代码执行器、工具以及其他增强功能 2。
AutoGen 生态系统还包括开发者工具，如 AutoGen Studio（一个用于无代码构建多智能体应用的图形用户界面）和 AutoGen Bench（一个用于评估智能体性能的基准测试套件）2。这种分层和可扩展的设计使得开发者可以根据需求在不同抽象级别上使用该框架。
AutoGen 的发展历程，例如从早期版本 (v0.2) 到当前的稳定版本 (v0.5.x)，体现了其向着更健壮、更易于扩展和用户友好的多智能体开发方向的演进 2。这种演进强调了更清晰的关注点分离（例如核心层与 AgentChat 层的划分）以及一个不断扩展的生态系统。因此，本 API 参考手册不仅旨在捕获框架的当前状态，也试图反映 AutoGen 所提供的模块化和渐进式复杂性的设计哲学。
本 API 参考手册的目的与范围 (Purpose and Scope of this API Reference Manual)
本手册旨在为 AutoGen Python API 的稳定版本 v0.5.6 提供一份全面、准确的中文参考 4。其主要目标读者是希望理解和利用 AutoGen 框架进行多智能体应用开发的中文软件开发者、AI 研究人员和工程师。
范围覆盖 AutoGen 的主要 Python 包，包括：
●autogen_agentchat: 用于构建对话式多智能体应用的高级 API。
●autogen_core: AutoGen 的基础核心层，提供事件驱动的智能体和运行时。
●autogen_ext: 包含对核心和 AgentChat 组件的具体实现和扩展，如模型客户端、工具和代码执行器。
本手册将详细描述这些包中的模块、类、函数、方法及其参数和返回值，力求与官方英文文档的结构和内容保持一致 8。明确版本信息 (v0.5.6) 对于确保技术细节的准确性至关重要。
AutoGen 框架为不同经验水平的用户提供了不同的切入点：AgentChat API 推荐给初学者和需要快速原型设计的用户，而核心 API 则面向需要更大灵活性和控制力的高级用户和工作流开发者 4。本 API 参考手册将努力兼顾这两类用户的需求，通过详尽且易于理解的方式呈现信息。
关于中文翻译的说明 (Note on Chinese Translation)
本手册中的所有技术术语、描述、参数说明、代码示例注释等均已翻译成简体中文。为了确保清晰度和准确性，特别是对于一些在行业内已有广泛认知或标准中文翻译尚在演变中的英文术语，我们会在其首次出现或在关键位置的中文翻译后附上相应的英文原文（通常在括号内）。例如，“智能体 (Agent)”。
这种处理方式旨在平衡纯中文环境的沉浸感与技术交流中对既有英文术语的熟悉度，以期为中文开发者提供最实用、最易懂的参考资料。
如何使用本手册 (How to Use This Manual)
本 API 参考手册按照 AutoGen 的包结构进行组织，主要分为 autogen_agentchat、autogen_core 和 autogen_ext 三大部分。每个部分下再细分为各个模块，模块内部则详细介绍相关的类、函数和常量。
●导航: 您可以通过侧边栏的目录结构快速定位到感兴趣的包、模块或具体 API 条目。
●API 条目: 每个类或函数的文档通常会包含以下信息：
○简要描述其功能和用途。
○参数列表：包括参数名称、类型、是否可选、默认值以及中文描述。
○返回值：描述返回值的类型和含义。
○方法（对于类）：列出其主要方法，并对每个方法进行类似的参数和返回值说明。
○属性（对于类）：列出其主要属性及其含义。
○代码示例（如果适用）：提供简短的代码片段以演示 API 的使用方法。
●表格: 对于关键的类，如各种智能体和团队配置，我们会提供参数表和方法表，以便快速查阅。
●术语表: 附录中包含一个术语表，列出了手册中使用的关键技术术语及其对应的英文和中文翻译，以帮助理解和保持一致性。
建议初学者从 autogen_agentchat 部分开始，了解如何使用预设的智能体和团队模式快速构建应用。有经验的开发者或希望进行深度定制的用户可以直接查阅 autogen_core 部分，以理解框架的底层机制。autogen_ext 部分则对所有用户都有价值，因为它提供了许多即用型的功能扩展。
I. AutoGen AgentChat API 参考 (autogen_agentchat)
autogen_agentchat 模块概述 (Module Overview)
autogen_agentchat 包是 AutoGen 框架中用于构建多智能体对话应用的高级 API 4。它构建于 autogen_core 之上，旨在为开发者提供一套直观、易用的工具，以便快速原型化和实现复杂的智能体交互。AgentChat 的核心理念是简化多智能体系统的开发，通过提供具有预设行为的智能体 (Agent) 和预定义的多智能体设计模式（例如团队 (Team)）来实现这一点 4。
对于初学者而言，AgentChat 是入门 AutoGen 的推荐起点。而对于需要更细粒度控制底层组件和事件驱动编程模型的高级用户，autogen_core 提供了更大的灵活性。
该模块本身也定义了一些关键的常量，主要用于日志记录 9：
●EVENT_LOGGER_NAME: 用于结构化消息日志记录器的名称，例如智能体之间的低级别消息。
●TRACE_LOGGER_NAME: 用于跟踪日志和内部消息的日志记录器名称。
这些日志记录器与 Python 内置的 logging 模块配合使用，帮助开发者调试和监控智能体应用的行为 10。
AgentChat 的主要功能通过其下的各个子模块提供，包括消息定义、智能体类型、团队协作模式、工具接口、基础类、终止条件、用户界面组件以及状态管理机制。
autogen_agentchat.messages (消息)
在 AgentChat 中，消息是智能体之间以及智能体与外部系统（如用户或其他应用）进行通信和信息交换的基础。这些消息不仅承载文本内容，还可以包含多模态数据、工具调用请求与结果、状态指示等多种信息。AgentChat 定义了一系列消息类型，它们都派生自基类，以支持多样化的交互需求 8。这些消息类型的设计反映了 AutoGen 处理复杂交互和超越简单文本数据的能力，从而满足高级 AI 应用的需求。
消息基类:
●BaseChatMessage: 这是所有用于智能体间通信消息的基类。它定义了消息来源 (source)、时间戳 (timestamp) 等通用属性。
●BaseAgentEvent: 这是所有智能体内部事件消息的基类。这类消息通常不直接在智能体间传递，而是用于记录或触发智能体内部的状态变化或行为。
主要消息类型:
●TextMessage(content: str, source: str): 最基本的消息类型，用于传递纯文本内容。
○content: 消息的文本字符串。
○source: 消息发送者的名称。
○例如，用户输入或智能体的文本回复 12。
●MultiModalMessage(content: List[Union[str, Image]], source: str): 用于传递包含多种模态内容的消息，如文本和图像的组合 13。
○content: 一个列表，其中元素可以是文本字符串或 autogen_core.Image 对象。
○source: 消息发送者的名称。
○这使得智能体能够处理和响应视觉信息，与现代 LLM 的多模态能力相匹配。
●StructuredMessage(content: BaseModel, source: str): 用于传递结构化数据。其 content 字段通常是一个 Pydantic BaseModel 的实例，允许智能体以预定义的、机器可解析的格式输出信息 12。
○这对于需要精确数据格式的应用场景（如 API 调用参数准备或数据库记录生成）至关重要。
●ToolCallRequestEvent(content: List[FunctionCall], source: str): 当智能体（通常是 AssistantAgent）决定调用一个或多个工具时，会生成此事件。
○content: 一个 FunctionCall 对象列表，每个对象包含工具名称、参数等信息。
○此事件清晰地记录了智能体的工具使用意图，便于调试和观察。
●ToolCallExecutionEvent(content: List, source: str): 在工具被执行后，此事件用于封装工具执行的结果。
○content: 一个 FunctionExecutionResult 对象列表，每个对象包含工具调用的结果（成功或失败，以及输出）。
●ToolCallSummaryMessage(content: str, source: str): 在工具调用及其执行后，此消息通常由智能体生成，用以总结工具调用的结果，并可能作为对其他智能体的回复。
●HandoffMessage(content: str, recipient: str, source: str): 在某些团队协作模式（如 Swarm）中，用于智能体将控制权或任务移交给另一个特定智能体 14。
○recipient: 接收移交的智能体的名称。
●StopMessage(content: Optional[str] = None, source: Optional[str] = None): 一种特殊消息，用于指示对话或任务应终止。
●UserInputRequestedEvent(source: str, prompt: Optional[str] = None): 当 UserProxyAgent 需要用户输入时，会生成此事件。
下表总结了部分关键消息类型的属性：
消息类型 (Message Type)	主要属性 (Key Attributes)	中文描述 (Chinese Description)
TextMessage	content: str, source: str	包含纯文本内容的消息。
MultiModalMessage	content: List[Union[str, Image]], source: str	包含文本和图像等多种模态内容的消息。
StructuredMessage	content: BaseModel, source: str	包含 Pydantic 模型定义的结构化内容的消息。
ToolCallRequestEvent	content: List[FunctionCall], source: str	表示智能体请求调用一个或多个工具的事件。
ToolCallExecutionEvent	content: List, source: str	包含工具执行结果的事件。
HandoffMessage	content: str, recipient: str, source: str	用于在智能体之间移交控制权或任务的消息。
StopMessage	content: Optional[str], source: Optional[str]	指示对话或任务终止的特殊消息。
UserInputRequestedEvent	source: str, prompt: Optional[str]	表示 UserProxyAgent 请求用户输入的事件。
理解这些不同的消息类型及其用途，对于设计和实现复杂的智能体交互至关重要。它们为 AgentChat 提供了处理多样化通信场景的强大能力。
autogen_agentchat.agents (代理)
autogen_agentchat.agents 模块提供了一系列预设的智能体类，这些智能体是构建多智能体应用的核心行动者。每个智能体都具有特定的行为模式和能力，可以独立工作或在团队中协作。AutoGen 设计理念中一个重要方面就是提供这些多样化的预构建智能体，作为开发复杂多智能体应用的基础模块，从而为常见智能体角色减少了样板代码的编写 12。
所有 AgentChat 智能体通常都继承自 BaseChatAgent，它定义了智能体的基本接口，如名称 (name)、描述 (description) 以及核心的消息处理方法 on_messages() 和流式处理方法 on_messages_stream() 12。
核心智能体类:
1.AssistantAgent (助手智能体)
○描述: 这是 AgentChat 中最核心和通用的智能体之一，通常由大型语言模型 (LLM) 驱动。它能够理解自然语言指令、生成回复、使用工具 (Tools) 或工作台 (Workbench) 来执行任务，并能对工具使用结果进行反思 (Reflection) 12。
○主要参数:
■name (str): 智能体的唯一名称。
■model_client (ChatCompletionClient): 用于与 LLM 进行交互的模型客户端实例。
■tools (Optional]]): 一个工具列表，智能体可以使用这些工具来执行特定操作，如代码执行、网页搜索等。工具可以是 BaseTool 的实例，也可以是同步或异步的 Python 函数 12。
■workbench (Optional[Workbench]): 一个工作台实例，用于管理一组共享状态和资源的工具。不能与 tools 参数同时使用 12。
■system_message (Optional[str]): 发送给 LLM 的系统消息，用于设定智能体的角色、行为指南或上下文。默认值为 "You are a helpful AI assistant. Solve tasks using your tools. Reply with TERMINATE when the task has been completed." 12。
■model_context (Optional[ChatCompletionContext]): 用于存储和检索发送给模型的消息的上下文。可以预加载初始消息，或使用如 BufferedChatCompletionContext 这样的实现来限制上下文长度 12。
■output_content_type (Optional]): 一个 Pydantic 模型类，用于定义智能体输出的结构。设置此参数后，智能体默认会返回 StructuredMessage 12。
■reflect_on_tool_use (Optional[bool]): 如果为 True，智能体在使用工具后会进行额外的模型推理以生成最终回复；否则，直接返回工具结果。默认为 True (如果设置了 output_content_type) 或 False 12。
■memory (Optional]): 一个或多个记忆存储实例，用于为智能体提供长期记忆或上下文检索能力 (RAG) 12。
■handoffs (Optional[List[Union[Handoff, str]]]): 配置智能体将控制权移交给其他智能体的规则 12。
○主要方法:
■on_messages(messages, cancellation_token): 处理传入消息序列并返回一个包含最终回复消息的 Response 对象。
■on_messages_stream(messages, cancellation_token): 以流式方式处理传入消息，异步生成中间事件/消息和最终的 Response。
■run(task, cancellation_token): 运行智能体处理给定任务，返回 TaskResult。
■run_stream(task, cancellation_token): 以流式方式运行智能体处理任务，异步生成事件/消息和最终的 TaskResult。
■save_state(): 保存智能体当前状态。
■load_state(state): 加载先前保存的智能体状态。
○应用场景: 任务执行、问答、内容生成、工具协调等。
AssistantAgent 参数	类型	中文描述
name	str	智能体的名称。
model_client	ChatCompletionClient	用于模型推理的客户端。
tools	List	智能体可使用的工具列表。
workbench	Workbench	管理一组工具的工作台。
system_message	str	发送给模型的系统提示。
output_content_type	Type	定义智能体输出结构的 Pydantic 模型。
reflect_on_tool_use	bool	是否在工具使用后进行反思。
model_context	ChatCompletionContext	管理发送给模型的聊天上下文。
memory	Sequence[Memory]	智能体的记忆存储。
handoffs	`List[Handoff \	str]`
2.UserProxyAgent (用户代理智能体)
○描述: 代表人类用户与AI智能体系统进行交互。它通过一个输入函数 (input_func) 来获取用户的响应 12。
○主要参数:
■name (str): 智能体的名称。
■input_func (Optional[Callable]): 一个函数，用于接收提示并返回用户的输入。可以是同步或异步的。
○主要方法:
■on_messages(messages, cancellation_token): 将上一条消息呈现给用户（通过 input_func），并将用户的回复作为 TextMessage 返回。
○应用场景: 在多智能体对话中引入人工输入、反馈和控制。
3.CodeExecutorAgent (代码执行器智能体)
○描述: (实验性功能) 能够根据用户指令生成和执行代码片段（Python 和 Shell）。它依赖于一个代码执行器 (CodeExecutor) 来实际运行代码 12。
○主要参数:
■name (str): 智能体的名称。
■code_executor (CodeExecutor): 负责运行代码的代码执行器实例 (例如 DockerCommandLineCodeExecutor)。
■model_client (Optional[ChatCompletionClient]): 用于生成代码和对执行结果进行反思的模型客户端。如果未提供，则仅执行输入消息中的代码块。
■max_retries_on_error (int): 代码执行失败时的最大重试次数。
○主要方法:
■on_messages(messages, cancellation_token): 处理传入消息，提取代码块，执行它们，并可能使用模型客户端生成代码或进行反思。
■execute_code_block(code_blocks, cancellation_token): 执行代码块列表。
○应用场景: 需要执行由 LLM 生成的代码的任务，如数据分析、脚本编写、自动化任务。这种关注点分离允许开发者组合具有明确定义角色的系统，从而提高模块化和可维护性。
4.SocietyOfMindAgent (心智社会智能体)
○描述: 这是一个元智能体，它利用一个内部的智能体团队 (Team) 来生成响应。它首先运行内部团队，然后使用自己的模型客户端根据团队的交互来形成最终的回复 12。
○主要参数:
■name (str): 智能体的名称。
■team (Team): 内部的智能体团队。
■model_client (ChatCompletionClient): 该智能体用于生成最终响应的模型客户端。
○应用场景: 将复杂任务分解给一个专门的子团队处理，然后由该智能体整合结果。
5.MessageFilterAgent (消息过滤器智能体)
○描述: (实验性功能) 这是一个包装智能体，它在将传入消息传递给内部智能体之前对其进行过滤。这对于在多智能体工作流中控制特定智能体可见的上下文非常有用 12。
○主要参数:
■name (str): 智能体的名称。
■wrapped_agent (BaseChatAgent): 内部智能体，过滤后的消息将传递给它。
■filter (MessageFilterConfig): 指定消息过滤方式的配置对象。
○应用场景: 在复杂的对话中，限制某些智能体接收到的信息量或信息类型，以提高效率或安全性。
这些预设的智能体为构建各种多智能体应用提供了坚实的基础。开发者可以根据具体需求选择和配置这些智能体，或者在理解其设计后，基于 BaseChatAgent 创建自定义智能体。
autogen_agentchat.teams (团队)
autogen_agentchat.teams 模块提供了用于组织和协调多个智能体协同工作的类和机制。在 AgentChat 中，“团队 (Team)”是一组智能体，它们共享一个共同的上下文，并根据预定义的模式进行交互以完成特定任务。AutoGen 在团队协作和工作流编排方面展现了其能力的成熟，从简单的对话循环发展到结构化的、目标导向的流程 14。
核心团队类和概念:
1.BaseGroupChat (基础群聊)
○描述: 这是创建群聊团队的基类。它提供了管理智能体团队的基本功能。通常，要实现特定的群聊团队，需要子类化 BaseGroupChat 并创建一个 BaseGroupChatManager 的子类来处理群聊逻辑 16。
○主要参数:
■participants (List[ChatAgent]): 团队中的智能体参与者列表。
■termination_condition (Optional): 指定群聊何时结束的终止条件。
■max_turns (Optional[int]): 群聊的最大轮次。
■emit_team_events (bool): 是否通过 run_stream 发出团队事件，默认为 False 16。
○主要方法: run(task, cancellation_token), run_stream(task, cancellation_token), reset(), save_state(), load_state()。
2.RoundRobinGroupChat (轮询群聊)
○描述: 一种简单的团队模式，参与者按预定顺序轮流发言。每个智能体的回复都会广播给团队中的所有其他智能体，确保上下文的一致性 16。
○应用场景: 适用于需要按固定顺序进行交互的简单协作任务。
3.SelectorGroupChat (选择器群聊)
○描述: 在这种团队模式中，每次消息后，会使用一个大型语言模型 (ChatCompletion模型) 来选择下一个发言的智能体 16。
○主要参数 (除继承自 BaseGroupChat 外):
■model_client (ChatCompletionClient): 用于选择下一个发言者的模型客户端。
■selector_prompt (str): 用于选择下一个发言者的提示模板。
■allow_repeated_speaker (bool): 是否允许重复选择上一个发言者。
○应用场景: 适用于需要根据对话动态选择最合适智能体发言的场景。
4.Swarm (蜂群)
○描述: Swarm 实现了一种团队模式，其中智能体可以根据自身能力将任务“移交 (handoff)”给其他智能体。这个概念借鉴自 OpenAI 的 Swarm 设计模式 14。核心思想是让智能体通过特殊的工具调用（生成 HandoffMessage）来委派任务，同时所有智能体共享相同的消息上下文。这使得智能体能够就任务规划做出局部决策，而不是依赖于像 SelectorGroupChat 那样的中央协调器 14。
○工作机制: 发言智能体的选择基于上下文中最新的 HandoffMessage。AssistantAgent 可以通过设置 handoffs 参数来指定它可以移交的对象。
○应用场景: 适用于需要去中心化、灵活任务分配和动态协作的复杂任务，如客户支持、内容生成等 14。
5.GraphFlow (图工作流)
○描述: 这是 AutoGen v0.5.6 中的一个重要新增功能，允许通过有向图 (Directed Graph) 定义多智能体工作流 15。GraphFlow 是 AgentChat API 中的一个新的团队类，可以看作是 SelectorGroupChat 的一个版本，但其选择器函数 (selector_func) 是一个有向图。它更为强大，因为该抽象还支持并发智能体 15。
○主要参数 (除继承自 BaseGroupChat 外):
■graph (DiGraph): 定义执行流程的有向图实例。
○核心组件:
■DiGraph (有向图): 定义了一个包含节点（智能体）和边（带有可选条件的执行路径）的图结构 16。
■DiGraphNode (有向图节点): 代表图中的一个智能体节点，包含其名称、出边和激活条件（'all' 或 'any'）16。
■DiGraphEdge (有向图边): 代表图中的一条有向边，包含目标节点名称和可选的执行条件 16。
■DiGraphBuilder (有向图构建器): 一个实用工具类，提供流畅的接口来构建 DiGraph 实例，简化了以编程方式构建复杂智能体交互图（包括顺序、并行、条件和循环流）的过程 15。
○应用场景: 需要精确控制智能体交互顺序、实现条件分支、并行执行或循环流程的复杂业务流程和研究场景。例如，可以构建扇出扇入 (fan-out-fan-in) 的工作流 15。
○GraphFlow 的引入标志着 AutoGen 在编排复杂多智能体交互方面能力的成熟，从基本的对话循环转向结构化、目标导向的过程。
GraphFlow 相关类	中文描述
GraphFlow	基于有向图执行群聊的团队。
DiGraph	定义节点（智能体）和边（执行路径）的有向图结构。
DiGraphBuilder	用于以编程方式流畅构建 DiGraph 实例的工具类。
DiGraphNode	代表 DiGraph 中的一个节点（智能体）。
DiGraphEdge	代表 DiGraph 中的一条有向边，可带有执行条件。
6.MagenticOneGroupChat (Magentic-One 群聊)
○描述: 一个使用 Magentic-One 架构来管理参与者之间对话流的团队。此团队中的协调器旨在高效完成任务 16。
○主要参数 (除继承自 BaseGroupChat 外):
■model_client (ChatCompletionClient): 用于生成响应的模型客户端。
○应用场景: 适用于需要遵循 Magentic-One 模式进行高效任务处理的场景。
这些团队类为开发者提供了多种选择来组织智能体，从简单的轮询到基于 LLM 的动态选择，再到高度结构化的图工作流和去中心化的蜂群模式。这种多样性使得 AutoGen 能够适应广泛的应用需求。
autogen_agentchat.tools (工具)
autogen_agentchat.tools 模块提供了将智能体或团队本身封装为工具的能力，这使得可以构建层级化或模块化的智能体系统。这种元能力是 AutoGen 设计中的一个强大特性，允许更高级别的智能体将子任务委托给专门的智能体或智能体团队。
●AgentTool(agent: BaseChatAgent, name: Optional[str] = None, description: Optional[str] = None)
○描述: 此类允许将一个 BaseChatAgent 实例包装成一个工具，使其可以被另一个 AssistantAgent 调用。当此工具被调用时，实际上是向被包装的智能体发起一次运行 (run)。
○参数:
■agent (BaseChatAgent): 要被包装成工具的智能体实例。
■name (Optional[str]): 工具的名称。如果未提供，则使用智能体的名称。
■description (Optional[str]): 工具的描述。如果未提供，则使用智能体的描述。
○工作方式: 调用此工具时，输入的参数会作为任务传递给被包装的智能体。被包装智能体的最终回复将作为工具的输出。
○应用场景: 创建一个“专家”智能体（如专门进行特定类型数据分析的智能体），然后将其作为工具提供给一个“协调员”智能体，协调员可以将相关任务分配给这个专家工具。
●TeamTool(team: Team, name: Optional[str] = None, description: Optional[str] = None)
○描述: 类似于 AgentTool，此类允许将一个完整的 Team 实例包装成一个工具。
○参数:
■team (Team): 要被包装成工具的团队实例。
■name (Optional[str]): 工具的名称。如果未提供，则使用团队的名称。
■description (Optional[str]): 工具的描述。如果未提供，则使用团队的描述。
○工作方式: 调用此工具时，输入的参数会作为任务传递给被包装的团队。团队执行任务后的最终结果（通常是 TaskResult 中的某个部分）将作为工具的输出。
○应用场景: 将一个复杂的多智能体协作流程（由一个团队实现）抽象为一个单一的工具，供更高层次的智能体或流程调用。例如，一个“研究报告生成团队”可以被包装成一个工具，供一个“项目经理智能体”调用。
通过 AgentTool 和 TeamTool，开发者可以构建出具有更高模块化程度和更清晰责任划分的复杂智能体系统。这符合 AutoGen 促进可重用和可组合智能体组件的设计哲学。
autogen_agentchat.base (基础类)
autogen_agentchat.base 模块定义了 AgentChat 框架的核心抽象和基础构建块。这些类和协议为智能体、团队、消息响应、任务执行和终止条件等关键概念提供了统一的接口和结构。理解这些基础类对于深入使用 AgentChat、进行定制或扩展至关重要。
主要基础类和协议:
●ChatAgent(ABC):
○描述: 所有 AgentChat 智能体的抽象基类。它定义了智能体必须实现的核心接口，特别是与消息处理相关的方法 12。
○主要抽象方法:
■on_messages(self, messages: Sequence, cancellation_token: CancellationToken) -> Response: 处理传入的消息序列并返回一个 Response 对象。这是智能体核心逻辑的入口点。
■on_reset(self, cancellation_token: CancellationToken) -> None: 重置智能体到其初始状态。
○其他重要方法: run(), run_stream(), save_state(), load_state()。
●Handoff:
○描述: 用于配置智能体如何将控制权或任务移交给其他智能体的数据类。通常与 Swarm 团队或 AssistantAgent 的 handoffs 参数一起使用 12。
○主要属性: 可能包括目标智能体名称、移交时的消息内容或条件等。
●Response:
○描述: on_messages 方法的返回类型。它封装了智能体对输入消息的响应。
○主要属性:
■chat_message (Optional): 智能体的最终回复消息，将发送给其他智能体或用户。
■inner_messages (Sequence]): 一个消息和事件的序列，代表智能体生成最终回复的“思考过程”或内部动作，例如工具调用请求和执行结果。
■is_successful (bool): 指示响应是否成功。
●TaskResult:
○描述: run 和 run_stream 方法（以及团队的相应方法）的最终返回类型。它总结了任务执行的结果。
○主要属性:
■messages (Sequence]): 任务执行期间产生的所有消息和事件的完整历史记录。
■stop_reason (Optional[Any]): 任务终止的原因，通常与 TerminationCondition 相关。
■is_successful (bool): 指示任务是否成功完成。
●TaskRunner(Protocol):
○描述: 定义了能够运行任务的对象的协议，智能体和团队都实现了这个协议。
○主要方法: run(), run_stream()。
●Team(TaskRunner, Component, ABC):
○描述: 所有团队类的抽象基类。团队本身也是一个 TaskRunner 和一个 Component。
○主要抽象方法: 除了继承自 TaskRunner 和 Component 的方法外，团队类通常需要实现特定的参与者管理和对话流程控制逻辑。
●TerminationCondition(ABC):
○描述: 用于定义对话或任务何时应该终止的条件的抽象基类 16。
○主要方法: __call__(self, messages: Sequence]) -> Optional: 接收自上次调用以来的消息增量序列，如果满足终止条件，则返回一个 StopMessage，否则返回 None。
○其他方法: reset(): 重置终止条件的状态。
○组合: 终止条件可以通过 AndTerminationCondition 和 OrTerminationCondition 进行逻辑组合（与、或）。
●TerminatedException(Exception):
○描述: 当任务因达到终止条件而结束时，可能会抛出的异常（尽管更常见的模式是 TaskResult 中包含终止原因）。
这些基础类和协议共同构成了 AgentChat 的骨架，为构建功能丰富、行为可控的智能体和智能体团队提供了坚实的基础。
autogen_agentchat.conditions (终止条件)
autogen_agentchat.conditions 模块提供了一系列预定义的终止条件 (TerminationCondition) 实现。在多智能体对话中，合理地设置终止条件对于控制对话流程、防止无限循环以及管理资源消耗（如 API调用成本）至关重要。每个终止条件类都实现了 TerminationCondition 协议，特别是 __call__ 方法，该方法检查最近的消息序列是否满足终止条件。
内置终止条件类型:
●MaxMessageTermination(max_messages: int):
○描述: 当产生的消息数量（通常指团队内部的交互轮次或特定智能体的发言次数）达到预设的最大值 max_messages 时，对话终止。
○应用场景: 防止对话无限进行，设定一个硬性的交互上限。
●TextMessageTermination(text_match: str, source_match: Optional[str] = None, case_sensitive: bool = False, regex: bool = False):
○描述: 当检测到来自特定来源（可选）的 TextMessage 内容与给定的文本 text_match 匹配时，对话终止。可以配置为区分大小写或使用正则表达式进行匹配。
○应用场景: 当某个智能体或用户发出特定指令或确认（如 "任务完成", "APPROVE"）时结束对话。
●StopMessageTermination():
○描述: 当任何智能体产生一个 StopMessage 类型的消息时，对话终止。
○应用场景: 允许智能体自身决定何时结束对话。
●HandoffTermination(agent_name: str):
○描述: 当产生一个目标为特定智能体 agent_name 的 HandoffMessage 时，对话终止。这通常用于 Swarm 模式之外，当需要将控制权移交给一个不在当前团队中的外部实体或流程时。
○应用场景: 将对话流程转交给人工处理或另一个独立的智能体系统。
●TimeoutTermination(timeout: float):
○描述: 当对话的总持续时间超过预设的 timeout（单位为秒）时，对话终止。
○应用场景: 为任务执行设置时间限制。
●TokenUsageTermination(max_total_tokens: Optional[int] = None, max_prompt_tokens: Optional[int] = None, max_completion_tokens: Optional[int] = None, model_client: Optional[ChatCompletionClient] = None):
○描述: 当 LLM 调用的 token 使用量（总计、提示或补全）超过预设的最大值时，对话终止。需要一个 model_client 来跟踪 token 使用情况。
○应用场景: 控制 LLM API 的使用成本。
●FunctionCallTermination(function_name: str, source_match: Optional[str] = None):
○描述: 当检测到来自特定来源（可选）的智能体请求调用名为 function_name 的特定函数（工具）时，对话终止。
○应用场景: 在智能体准备执行某个关键或最终步骤的工具调用时结束对话，可能用于在实际执行前进行审查。
●SourceMatchTermination(source_name: str, count: int = 1):
○描述: 当名为 source_name 的智能体发言达到 count 次时，对话终止。
○应用场景: 限制特定智能体的发言次数。
●FunctionalTermination(condition_func: Callable]], bool]):
○描述: 允许用户提供一个自定义的函数 condition_func，该函数接收消息序列并返回一个布尔值来决定是否终止。
○应用场景: 实现高度定制化的、基于复杂逻辑的终止条件。
组合终止条件:
终止条件可以使用 AndTerminationCondition 和 OrTerminationCondition 进行逻辑组合，或者直接使用 & (与) 和 | (或) 操作符。例如：
condition = MaxMessageTermination(10) | TimeoutTermination(60.0)
表示当消息达到10条或对话超过60秒时终止。
正确选择和配置终止条件是设计健壮、高效的 AgentChat 应用的关键环节。
autogen_agentchat.ui (用户界面)
autogen_agentchat.ui 模块提供了一些组件，用于在命令行界面 (CLI) 中与 AgentChat 应用进行交互和观察。这些组件简化了用户输入和对话流的显示。
●Console():
○描述: 这是一个实用工具类，用于将 AgentChat 的流式输出（通常来自 agent.run_stream() 或 team.run_stream()）以格式化的方式打印到控制台 18。它可以清晰地显示每个消息的来源、类型和内容，以及在任务结束时打印统计信息（如 token 使用量、耗时等）。
○使用方法: 通常将 run_stream() 的结果直接传递给 Console 的构造函数并 await 它。
Python
# 示例
# await Console(agent.run_stream(task="一些任务"))
# await Console(team.run_stream(task="团队任务"), output_stats=True)

○参数:
■stream (AsyncGenerator): run_stream() 返回的异步生成器。
■output_stats (bool): 是否在流结束时打印统计信息，默认为 False。
○功能:
■逐条打印流中的消息和事件。
■对不同类型的消息（如 TextMessage, ToolCallRequestEvent, ToolCallExecutionEvent）进行格式化，使其易于阅读。
■在 TaskResult 出现时，打印任务总结信息。
●UserInputManager:
○描述: (在较新版本中，其功能可能已更多地集成到 UserProxyAgent 或通过 input_func 实现) 这个类（或类似机制）用于管理从用户处获取输入的过程。它允许程序在需要时暂停并提示用户提供文本输入。
○与 UserProxyAgent 的关系: UserProxyAgent 通常会利用此类或类似逻辑通过其 input_func 参数来征求和处理人工输入。
○应用场景: 在需要人工干预、提供反馈或回答智能体问题的对话流程中使用。
这些 UI 组件虽然简单，但对于在开发和调试阶段观察智能体行为、与系统进行基本交互非常有用。对于更复杂的 UI需求，开发者可能需要构建自定义的用户界面并将其与 AutoGen 的核心逻辑集成。
autogen_agentchat.state (状态管理)
autogen_agentchat.state 模块定义了用于捕获和恢复 AgentChat 组件（如智能体和团队）状态的 Pydantic 模型。状态管理对于创建持久会话、从故障中恢复以及在不同执行之间迁移智能体状态至关重要。AutoGen 的组件化设计哲学在此处也得到体现，许多核心组件都支持状态的保存和加载 12。
主要状态模型类:
这些类通常与相应 AgentChat 组件的 save_state() 和 load_state() 方法配合使用。save_state() 方法会返回一个与这些 Pydantic 模型兼容的字典或直接返回模型实例，而 load_state() 方法则接收这样的状态对象来恢复组件。
●BaseState(ComponentModel):
○描述: 所有 AgentChat 状态模型的基础。它继承自 autogen_core.ComponentModel，表明状态本身也是一种组件配置。
○包含字段: 通常包含组件的配置信息 (config) 以及特定于该组件类型的状态数据。
●AssistantAgentState(BaseState):
○描述: 用于 AssistantAgent 的状态模型。
○可能包含的额外字段:
■model_context_state (Optional): AssistantAgent 使用的 ChatCompletionContext 的状态，其中包含消息历史。
■memory_states (Optional[List[Mapping[str, Any]]]): 如果 AssistantAgent 配置了记忆模块，这里可能存储各个记忆模块的状态。
●TeamState(BaseState):
○描述: 用于 Team（如 BaseGroupChat 及其子类）的状态模型。
○可能包含的额外字段:
■participants_state (List[Mapping[str, Any]]): 团队中每个参与智能体的状态。
■group_chat_manager_state (Optional): 群聊管理器的状态。
■termination_condition_state (Optional[Mapping[str, Any]]): 终止条件的状态。
■message_history (Optional[List[Mapping[str, Any]]]): 团队层面的消息历史（如果适用）。
●BaseGroupChatManagerState(BaseState):
○描述: 群聊管理器（如 RoundRobinManager, SelectorManager）的状态基类。
○子类示例:
■RoundRobinManagerState: 用于 RoundRobinGroupChat 的管理器状态。
■SelectorManagerState: 用于 SelectorGroupChat 的管理器状态，可能包含选择器相关的状态。
■SwarmManagerState: 用于 Swarm 团队的管理器状态。
■MagenticOneOrchestratorState: 用于 MagenticOneGroupChat 的协调器状态。
●SocietyOfMindAgentState(BaseState):
○描述: 用于 SocietyOfMindAgent 的状态模型。
○可能包含的额外字段:
■team_state (Optional): 其内部团队的状态。
■model_context_state (Optional): 该元智能体自身模型上下文的状态。
●ChatAgentContainerState(BaseState):
○描述: 可能用于包含多个 ChatAgent 的容器组件的状态。
使用方法:
开发者通常不需要直接实例化这些状态模型，而是通过调用智能体或团队实例的 save_state() 方法来获取状态对象（通常是字典形式，可以序列化为 JSON），并通过 load_state(state_dict) 方法来恢复状态。

Python


# 伪代码示例
# assistant = AssistantAgent(...)
# #... 运行一些任务...
# saved_state = await assistant.save_state()

# # 稍后或在另一个会话中
# new_assistant = AssistantAgent(...) # 使用相同的初始配置或从配置加载
# await new_assistant.load_state(saved_state)

通过这些状态管理类，AgentChat 应用可以实现更高级的功能，如会话持久化、检查点设置和故障恢复，这对于构建长时间运行或关键任务的智能体系统非常重要。
II. AutoGen Core API 参考 (autogen_core)
autogen_core 模块概述 (Module Overview)
autogen_core 是 AutoGen 框架的基石，提供了一个事件驱动、异步的底层 API，用于构建可扩展、灵活且具有弹性的多智能体系统 2。与主要面向快速原型设计和常见对话模式的 autogen_agentchat 不同，autogen_core 赋予开发者对智能体生命周期、消息传递机制和运行时环境更深层次的控制。它特别适合于需要构建自定义智能体、复杂工作流引擎或分布式智能体应用的场景。
核心特性与设计原则 3:
●异步消息传递 (Asynchronous Messaging): 智能体之间的通信基于异步消息，支持事件驱动和请求/响应等多种通信模型。
●可扩展与分布式 (Scalable & Distributed): 设计上支持构建跨越组织边界的复杂智能体网络，并能从本地运行平滑过渡到云端分布式系统。
●多语言支持 (Multi-Language Support): 目前主要支持 Python 和.NET 智能体之间的互操作，并计划支持更多语言。
●模块化与可扩展 (Modular & Extensible): 框架高度可定制，支持自定义智能体、记忆即服务、工具注册表和模型库等特性。
●可观察与可调试 (Observable & Debuggable): 提供了追踪和调试智能体系统的能力。
●事件驱动架构 (Event-Driven Architecture): 这是构建弹性、可伸缩系统的基础。
●组件化 (Component-Based): AutoGen 的一个核心理念是“万物皆组件”。智能体、工具、模型客户端等都被视为可配置、可序列化的组件，这通过 Component 基类及其相关机制实现 19。这种设计极大地增强了框架的模块化程度和可扩展性。
autogen_core 定义了智能体 (Agent)、智能体运行时 (Agent Runtime)、消息 (Message)、主题 (Topic)、订阅 (Subscription) 等核心概念的接口和基础实现。它将智能体的内部逻辑（可能涉及模型调用或代码执行）与消息传递机制完全解耦 20。
与 AgentChat 类似，autogen_core 也定义了用于日志记录的常量 19：
●ROOT_LOGGER_NAME: autogen_core 的根日志记录器名称 ('autogen_core')。
●EVENT_LOGGER_NAME: 用于结构化事件的日志记录器名称 ('autogen_core.events')。
●TRACE_LOGGER_NAME: 用于开发者追踪日志的记录器名称 ('autogen_core.trace')。
对于希望深入理解 AutoGen 工作原理、构建自定义底层组件或实现高级多智能体模式的开发者来说，autogen_core 是必须掌握的部分。
autogen_core.agent (代理基础)
此部分（在 8 原始结构中可能归属于 autogen_core 顶级模块）包含了 AutoGen 核心框架中定义智能体及其交互方式的基础类和概念。这些是构建任何基于 autogen_core 的智能体系统的基石。
核心类与协议:
●Agent(Protocol):
○描述: 定义了智能体必须遵循的接口（协议）。一个 Agent 能够接收和处理消息，并可以管理其自身状态。
○主要属性:
■id (AgentId): 智能体的唯一标识符。
■metadata (AgentMetadata): 描述智能体的元数据。
○主要方法:
■on_message(self, message: Any, sender: AgentId, cancellation_token: CancellationToken) -> Awaitable[Any]: 异步处理接收到的消息。
■save_state(self) -> Awaitable[Any]: 异步保存智能体的当前状态。
■load_state(self, state: Any) -> Awaitable[None]: 异步从给定的状态加载智能体。
■close(self) -> Awaitable[None]: 异步关闭智能体并释放资源。
●AgentId(type: str, key: str):
○描述: 用于在智能体运行时中唯一标识一个智能体实例 19。
○属性:
■type (str): 与智能体工厂函数关联的类型标识符。
■key (str): 智能体实例的唯一键。
○类方法: from_str(id_str: str) -> AgentId: 从字符串表示创建 AgentId。
●AgentMetadata(TypedDict):
○描述: 包含智能体元信息的类型字典 19。
○字段: type (str), key (str), description (Optional[str])。
●AgentRuntime(Protocol):
○描述: 定义了智能体运行时环境的接口。运行时负责管理智能体的生命周期、消息的分发和订阅等 19。
○主要方法:
■send_message(self, message: Any, recipient: AgentId, request_reply: bool, cancellation_token: CancellationToken) -> Awaitable[Any]: 异步向特定智能体发送消息。
■publish_message(self, message: Any, topic_id: TopicId, cancellation_token: CancellationToken) -> Awaitable[None]: 异步向特定主题发布消息。
■register_factory(self, agent_type: str, factory: Callable[[AgentId, AgentInstantiationContext], Awaitable[Agent]]) -> Awaitable[None]: 注册智能体工厂函数。
■其他方法涉及状态管理、订阅管理等。
●BaseAgent(Agent, ABC):
○描述: autogen_core 中智能体的抽象基类，实现了 Agent 协议。它提供了智能体注册和基本消息处理的框架 19。
○核心实现: 实现了 on_message 的最终版本，并引入了 on_message_impl 供子类覆盖以实现具体的消息处理逻辑。
○类方法: register(cls, runtime: AgentRuntime, agent_type: str, factory: Callable[, CT_Agent], subscriptions: Optional] = None) -> AgentId: 用于在运行时注册智能体类型及其工厂函数和订阅。
●RoutedAgent(BaseAgent):
○描述: 一个更具体的智能体基类，它能够根据消息类型和可选的匹配函数将传入消息路由到特定的处理程序方法 19。这是通过使用 @message_handler, @event, @rpc 等装饰器来实现的。
○方法: on_message_impl, on_unhandled_message。
●ClosureAgent(BaseAgent):
○描述: 允许使用一个闭包（即一个函数）而不是一个完整的类来定义智能体的行为，简化了简单智能体的创建 19。
○类方法: register_closure(...)。
消息传递原语:
●TopicId(type: str, source: str):
○描述: 在发布/订阅模型中定义广播消息的范围或类别 19。
○属性: type (事件类型), source (事件上下文或来源)。
●Subscription(Protocol):
○描述: 定义了智能体感兴趣的主题。智能体通过订阅来接收特定主题的消息 19。
○主要方法: is_match(topic_id: TopicId) -> bool, map_to_agent(topic_id: TopicId) -> Optional[AgentId]。
○具体实现示例: TypeSubscription, DefaultSubscription, TypePrefixSubscription。
●MessageContext:
○描述: 封装了消息的上下文信息，如发送者、主题ID、是否为RPC调用、取消令牌等 19。
●MessageHandlerContext:
○描述: 在消息处理函数内部提供上下文信息，如当前智能体的ID 19。
●MessageSerializer(Protocol):
○描述: 定义了消息序列化和反序列化的接口，用于在不同进程或系统间传递消息 19。
装饰器:
●@message_handler, @event, @rpc: 用于 RoutedAgent 中定义不同类型的消息处理函数 19。
●@default_subscription, @type_subscription: 用于简化向智能体类添加订阅的常用模式 19。
这些核心组件共同构成了 autogen_core 的基础，使得开发者能够构建出具有明确定义、可交互、可管理的智能体单元，并通过灵活的运行时环境进行编排。
autogen_core.code_executor (代码执行器)
autogen_core.code_executor 模块定义了在 AutoGen 框架内执行代码的核心接口和数据结构。代码执行是许多 AI 智能体应用的关键能力，例如，允许智能体运行由 LLM 生成的脚本来完成数据分析、与外部系统交互或执行特定任务。该模块本身不包含具体的执行逻辑（如在 Docker 中运行或本地执行），而是提供了一个标准化的契约，具体的执行器实现在 autogen_ext 包中提供。这种设计是 AutoGen 分层和可扩展架构的一个典型例子：核心层定义接口，扩展层提供实现 21。
核心类与数据结构:
●CodeExecutor(Component, ABC):
○描述: 代码执行器的抽象基类（协议）。任何希望在 AutoGen 中执行代码的组件都应实现此接口。它继承自 Component，意味着代码执行器本身也是可配置和可管理的组件。
○主要抽象方法:
■async execute_code_blocks(self, code_blocks: List, cancellation_token: CancellationToken) -> CodeResult: 异步执行一个或多个代码块。这是执行器最核心的方法。
■async restart(self) -> None: (可选) 重启执行器环境。
■async start(self) -> None: (可选) 启动执行器，例如启动一个容器或Jupyter内核。
■async stop(self) -> None: (可选) 停止执行器并清理资源。
○属性:
■work_dir (Path): 代码执行的工作目录。
●CodeBlock(language: str, code: str):
○描述: 表示一个待执行的代码块的数据类 21。
○属性:
■language (str): 代码块的语言，例如 "python", "bash", "shell", "powershell"。
■code (str): 实际的代码字符串。
●CodeResult(exit_code: int, output: str, file_path: Optional[str] = None):
○描述: 表示代码执行结果的数据类 21。
○属性:
■exit_code (int): 代码执行的退出码。0 通常表示成功。
■output (str): 代码执行的标准输出和标准错误合并的字符串。
■file_path (Optional[str]): (可选) 如果代码被保存到文件执行，则为该文件的路径。
●FunctionWithRequirements(func: Callable, requirements: Sequence[Union[str, ImportFromModule, Alias]]):
○描述: 允许定义一个函数及其执行所需的 Python 包依赖或模块导入。这对于确保代码在具有正确环境的执行器中运行非常有用 22。
○参数:
■func (Callable): 要执行的函数。
■requirements (Sequence[Union[str, ImportFromModule, Alias]]): 一个序列，包含：
■字符串形式的包依赖 (如 "pandas>=1.0")。
■ImportFromModule 对象，指定需要从哪个模块导入哪些名称。
■Alias 对象，指定模块导入时的别名。
●FunctionWithRequirementsStr(func_str: str, requirements: Sequence[Union[str, ImportFromModule, Alias]]):
○描述: 与 FunctionWithRequirements 类似，但函数本身以字符串形式提供，而不是直接的 Callable 对象。
●ImportFromModule(module: str, name: str, alias: Optional[str] = None):
○描述: 指定一个导入语句，例如 from module import name as alias。
●Alias(module: str, alias: str):
○描述: 指定一个模块导入别名，例如 import module as alias。
●with_requirements(requirements: Sequence[Union[str, ImportFromModule, Alias]]) -> Callable[[Callable], FunctionWithRequirements]:
○描述: 一个装饰器，用于方便地将 Python 函数包装成 FunctionWithRequirements 对象。
通过定义这些核心接口和数据结构，autogen_core.code_executor 为不同类型的代码执行器（如本地执行、Docker容器内执行、Jupyter 内核执行等）提供了一个统一的交互方式，增强了 AutoGen 框架的灵活性和可扩展性。
autogen_core.models (模型接口)
autogen_core.models 模块定义了 AutoGen 与大型语言模型 (LLM) 交互的核心接口和数据结构。它抽象了不同 LLM 提供商的具体实现细节，使得上层应用（如 AgentChat 中的智能体）可以以统一的方式与各种模型进行通信。
核心类与数据结构:
●ChatCompletionClient(Component, ABC):
○描述: 聊天补全客户端的抽象基类（协议）。所有具体的模型客户端（如 OpenAI 客户端、Anthropic 客户端等）都必须实现此接口。它继承自 Component，表明模型客户端也是可配置的组件。
○主要抽象方法:
■async create(self, messages: Sequence[LLMMessage], cache_seed: Optional[int] = None, **kwargs: Any) -> CreateResult: 异步发送消息序列给 LLM，并获取模型的回复。这是与 LLM 交互的核心方法。
■async create_stream(self, messages: Sequence[LLMMessage], cache_seed: Optional[int] = None, **kwargs: Any) -> AsyncGenerator: 与 create 类似，但以流式方式返回模型的回复，允许逐块处理生成的 token。
■count_tokens(self, messages: Sequence[LLMMessage], **kwargs: Any) -> int: 计算给定消息序列所占用的 token 数量。
■remaining_tokens(self, messages: Sequence[LLMMessage], **kwargs: Any) -> Optional[int]: 计算在当前模型限制下，给定消息序列后还剩余多少 token 可用。
○属性:
■model_info (ModelInfo): 描述模型能力和特性的信息。
■capabilities (ModelCapabilities): 模型的具体能力，如是否支持视觉、函数调用等。
●LLM 消息类型 (通常为 TypedDict 或 Pydantic 模型):
○SystemMessage(content: str): 系统消息，用于向 LLM 提供高级指令或上下文。
○UserMessage(content: Union[str, List[Union[str, Image]]]): 用户消息，代表用户的输入。内容可以是文本或文本与图像的混合列表（用于多模态模型）。
○AssistantMessage(content: Optional[str] = None, tool_calls: Optional[List[FunctionCall]] = None): 助手消息，代表 LLM 的回复。可以包含文本内容或工具调用请求 (FunctionCall)。
○FunctionExecutionResultMessage(tool_call_id: str, name: str, content: str): 函数（工具）执行结果消息，用于将工具的输出反馈给 LLM。
●CreateResult:
○描述: create 和 create_stream 方法返回结果的数据结构。
○主要属性:
■choices: 一个列表，包含 LLM 生成的回复选项。每个选项通常包含消息 (AssistantMessage) 和终止原因。
■usage (Optional): 本次请求的 token 使用情况。
■id: 请求的唯一 ID。
●RequestUsage(TypedDict):
○描述: 记录 LLM 请求中 prompt_tokens 和 completion_tokens (或 total_tokens) 的使用情况。
●ModelInfo(TypedDict):
○描述: 包含模型详细信息的字典，例如是否支持视觉 (vision: bool)、函数调用 (function_calling: bool)、JSON 输出 (json_output: bool) 等 23。
○函数: validate_model_info(): 用于验证 ModelInfo 对象的有效性。
●ModelCapabilities(TypedDict):
○描述: 更具体地描述模型支持的功能，如 vision (布尔值), function_calling (布尔值), json_output (布尔值)。
●ModelFamily(str, Enum):
○描述: 定义了已知的模型家族枚举，如 GPT_4O, GPT_4, GPT_35, GEMINI_1_5_PRO 等 23。这有助于 AutoGen 根据模型类型进行一些特定的处理或优化。
●ChatCompletionTokenLogprob 和 TopLogprob:
○描述: 如果模型支持，这些结构用于表示生成 token 时的对数概率信息，可用于更高级的分析或控制。
此模块通过标准化的接口和数据类型，为 AutoGen 框架接入和使用不同的 LLM 服务提供了基础，使得开发者可以更容易地切换模型或利用特定模型的功能。
autogen_core.model_context (模型上下文)
autogen_core.model_context 模块负责管理发送给大型语言模型 (LLM) 的聊天完成上下文。在与 LLM 的持续对话中，如何有效地构建和维护上下文窗口对于模型的性能、连贯性以及成本控制都至关重要。此模块提供了多种策略来处理消息历史，以适应不同的需求和模型限制。
核心类与概念:
●ChatCompletionContext(Component, ABC):
○描述: 聊天完成上下文的抽象基类。它定义了智能体存储和检索 LLM 消息的接口。所有具体的上下文管理策略都从此类派生。它也继承自 Component，意味着上下文管理器本身也是可配置的。
○主要方法:
■add_message(self, message: LLMMessage) -> None: 向上下文中添加一条消息。
■get_messages(self) -> Sequence[LLMMessage]: 获取当前上下文中用于发送给 LLM 的消息序列。具体的实现会根据其策略来决定返回哪些消息。
■clear(self) -> None: 清空上下文中的所有消息。
■save_state(self) -> ChatCompletionContextState: 保存上下文的当前状态。
■load_state(self, state: ChatCompletionContextState) -> None: 从给定的状态恢复上下文。
○参数 (构造时):
■initial_messages (Optional[List[LLMMessage]]): (可选) 初始化上下文时预置的一组消息。
●ChatCompletionContextState(TypedDict):
○描述: 用于保存和加载 ChatCompletionContext 状态的数据结构。
○主要字段: messages (List[LLMMessage]): 包含上下文中的完整消息历史。
具体的上下文管理实现:
●UnboundedChatCompletionContext(ChatCompletionContext):
○描述: 最简单的上下文管理器，它会保留并发送所有历史消息给 LLM。
○适用场景: 对话历史较短，或使用的模型对上下文长度没有严格限制（或限制非常大）的场景。
○注意事项: 可能会快速超出模型的 token 限制并导致成本增加。
●BufferedChatCompletionContext(ChatCompletionContext):
○描述: 仅保留最近的 buffer_size 条消息作为上下文发送给 LLM 24。
○参数 (构造时):
■buffer_size (int): 要保留的最近消息的数量。
○适用场景: 当需要一个简单的固定大小的滑动窗口来管理上下文时。
●HeadAndTailChatCompletionContext(ChatCompletionContext):
○描述: 一种更复杂的策略，它保留对话历史的头部（例如系统消息和最初几轮对话）和尾部（最近几轮对话），而中间的消息可能会被省略，以适应 token 限制 24。
○参数 (构造时):
■head_size (int): 头部保留的消息数量。
■tail_size (int): 尾部保留的消息数量。
○适用场景: 希望在保留关键初始指令和最近对话内容的同时，有效管理长对话的上下文。
●TokenLimitedChatCompletionContext(ChatCompletionContext):
○描述: 根据 token 数量限制来管理上下文。它会尝试包含尽可能多的最近消息，同时确保总 token 数不超过指定的限制或模型本身的限制 24。
○参数 (构造时):
■model_client (ChatCompletionClient): 用于计算 token 数量的模型客户端。
■token_limit (Optional[int]): 上下文的最大 token 数量。如果为 None，则使用模型客户端的 remaining_tokens() 方法确定的限制。
■tools (Optional]): (可选) 工具的模式，因为它们也可能消耗 token。
○适用场景: 需要精确控制发送给模型的 token 数量，以优化性能和成本。这是最常用的上下文管理策略之一。
通过选择和配置合适的 ChatCompletionContext 实现，开发者可以有效地管理 LLM 的上下文窗口，确保对话的连贯性，并避免超出模型的 token 限制。
autogen_core.tools (工具)
autogen_core.tools 模块定义了 AutoGen 框架中工具 (Tool) 和工作台 (Workbench) 的核心接口和数据结构。工具是智能体用来与外部世界交互、执行特定操作或获取专门知识的手段。工作台则是一组相关工具的集合，通常共享某些状态或资源。
核心类与协议:
●Tool(Protocol) / BaseTool(Component, Tool, ABC):
○描述: 定义了工具的基本接口。BaseTool 是一个抽象基类，它实现了 Tool 协议并继承自 Component，意味着工具也是可配置和可管理的。
○主要方法/属性:
■name (str): 工具的名称，必须是唯一的。
■description (str): 对工具功能的描述，LLM 会根据此描述来决定何时使用该工具。
■schema (ToolSchema): 工具的 JSON Schema 定义，描述了工具的参数。
■args_type(self) -> Optional]: (可选) 返回工具参数的 Pydantic 模型类型。
■return_type(self) -> Optional]: (可选) 返回工具输出的 Pydantic 模型类型。
■async run(self, arguments: Mapping[str, Any], cancellation_token: Optional = None) -> Any: 异步执行工具的核心逻辑。
■return_value_as_string(self, value: Any) -> str: 将工具的返回值转换为字符串，以便 LLM 理解。
■save_state_json(self) -> Optional[str]: (可选) 将工具的状态保存为 JSON 字符串。
■load_state_json(self, state: str) -> None: (可选) 从 JSON 字符串加载工具的状态。
○BaseToolWithState 是 BaseTool 的一个子类，专门为有状态的工具设计，提供了更结构化的状态保存和加载方法。
●FunctionTool(BaseTool):
○描述: 一个便捷的类，用于将普通的 Python 函数（同步或异步）快速包装成一个 AutoGen 工具 25。它会自动从函数的签名和文档字符串中推断出工具的名称、描述和参数模式。
○参数 (构造时):
■func (Callable): 要包装的 Python 函数。
■name (Optional[str]): (可选) 工具名称，默认为函数名。
■description (Optional[str]): (可选) 工具描述，默认为函数文档字符串。
■parameters_schema (Optional]): (可选) 参数的 Pydantic 模型。
●ToolSchema(TypedDict):
○描述: 定义工具的 JSON Schema 结构，符合 OpenAI 的函数调用规范。
○主要字段: name (str), description (str), parameters (ParametersSchema).
●ParametersSchema(TypedDict):
○描述: 定义工具参数的 JSON Schema。
○主要字段: type (通常为 "object"), properties (一个字典，描述每个参数的名称、类型、描述等), required (一个必需参数名称的列表)。
●ToolResult(TypedDict):
○描述: 表示工具执行结果的数据结构。
○主要字段:
■name (str): 被调用工具的名称。
■result (Any): 工具执行的原始结果。
■is_error (bool): 指示执行是否出错。
■type (Literal["text", "image"]): (可选) 结果的主要类型。
○方法: to_text(): 将结果转换为文本表示。
●TextResultContent 和 ImageResultContent:
○描述: 用于 ToolResult 中，更具体地指定结果内容的类型。
●Workbench(Component, ABC):
○描述: 工作台的抽象基类，代表一组工具的集合。它继承自 Component。
○主要方法:
■async list_tools(self) -> Sequence: 返回工作台中所有可用工具的模式列表。
■async call_tool(self, tool_name: str, arguments: Mapping[str, Any], cancellation_token: Optional = None) -> ToolResult: 调用工作台中的指定工具。
■start(), stop(), reset(), save_state(), load_state(): 管理工作台生命周期和状态的方法。
●StaticWorkbench(Workbench):
○描述: 一个简单的工作台实现，它在初始化时接收一个固定的工具列表。
○参数 (构造时): tools (Sequence).
这些接口和类为 AutoGen 智能体提供了强大的工具使用能力，使其能够执行远超简单文本生成的复杂任务。通过 FunctionTool 可以轻松集成现有代码，而 Workbench 则为管理和组织多组工具提供了便利。
autogen_core.tool_agent (工具代理)
autogen_core.tool_agent 模块提供了与工具使用相关的特定智能体逻辑和异常处理。虽然 AssistantAgent 在 AgentChat层面已经集成了工具调用能力，但 autogen_core 中的 ToolAgent 可能代表了一种更底层的、专门用于执行工具或与工具交互的智能体模式或辅助功能。
核心类与异常:
●ToolAgent(BaseAgent):
○描述: (具体实现和用途可能随版本演变，但从名称推断) 这可能是一个专门设计用于执行工具调用的智能体。它可以接收工具调用请求，执行相应的工具，并返回结果。它可能被其他更高级别的智能体用作一个专门的“执行单元”。
○职责可能包括:
■解析工具调用请求。
■从 Workbench 或其他来源查找并加载工具。
■安全地执行工具。
■格式化工具执行结果以供 LLM 或其他智能体使用。
●ToolException(Exception):
○描述: 与工具相关的通用异常基类。
●ToolNotFoundException(ToolException):
○描述: 当请求的工具未在可用工具列表或工作台中找到时抛出。
○应用场景: 帮助开发者诊断智能体为何无法执行预期的工具调用。
●InvalidToolArgumentsException(ToolException):
○描述: 当提供给工具的参数无效（例如，类型不匹配、缺少必需参数）时抛出。
○应用场景: 在工具执行前进行参数验证，或在工具内部检测到参数问题时使用。
●ToolExecutionException(ToolException):
○描述: 当工具在执行过程中发生内部错误时抛出。
○应用场景: 捕获并报告工具执行期间发生的运行时错误。
●tool_agent_caller_loop():
○描述: (从名称推断) 这可能是一个辅助函数或协程，用于实现一个循环，该循环负责从某个来源（如另一个智能体或消息队列）接收工具调用请求，调用 ToolAgent 或直接执行工具，然后将结果发送回去。这种模式常见于将工具执行逻辑与主智能体逻辑分离的场景。
虽然 autogen_agentchat.AssistantAgent 已经内置了复杂的工具调用和处理逻辑（包括调用模型生成工具参数、执行工具、处理结果并可能进行反思），autogen_core.tool_agent 中的组件可能为更细粒度的控制或构建专门的工具执行服务提供了基础。例如，在一个分布式系统中，一个 ToolAgent 实例可能运行在一个单独的服务中，专门负责执行耗时或需要特定环境的工具。
autogen_core.memory (记忆模块)
autogen_core.memory 模块定义了 AutoGen 框架中记忆功能的核心接口和基本实现。记忆是智能体能够存储、检索和利用先前信息以指导当前和未来行为的关键能力。这对于维持对话连贯性、学习用户偏好、执行多步骤任务以及实现如检索增强生成 (RAG) 等高级模式至关重要。
核心类与协议:
●Memory(Component, ABC):
○描述: 记忆存储的抽象基类（协议）。所有具体的记忆实现（如列表记忆、向量数据库记忆等）都应实现此接口。它继承自 Component，表明记忆模块也是可配置和可管理的。
○主要抽象方法:
■async add(self, content: Sequence[MemoryContent], cancellation_token: Optional = None) -> None: 异步向记忆存储中添加一条或多条内容。
■async query(self, query_text: str, k: int, cancellation_token: Optional = None) -> MemoryQueryResult: 异步根据查询文本从记忆存储中检索最相关的 k 条信息。
■async update_context(self, current_context: Sequence[LLMMessage], query_text: Optional[str] = None, k: Optional[int] = None, cancellation_token: Optional = None) -> UpdateContextResult: (在较新版本中，此方法可能演变为更通用的与 ChatCompletionContext 交互的方式，或者由 AssistantAgent 等上层组件直接调用 query 并处理结果) 此方法旨在根据查询结果更新提供给 LLM 的当前上下文。
■async clear(self, cancellation_token: Optional = None) -> None: 异步清空记忆存储中的所有内容。
■async close(self, cancellation_token: Optional = None) -> None: (可选) 关闭记忆存储并释放资源。
●MemoryContent(TypedDict):
○描述: 表示存储在记忆中的单条内容的数据结构。
○主要字段:
■content (str): 记忆内容的文本表示。
■mime_type (MemoryMimeType): 内容的 MIME 类型，指示其格式。
■metadata (Optional[Mapping[str, Any]]): (可选) 与此记忆内容相关的元数据字典，可用于过滤或提供额外信息。
●MemoryMimeType(str, Enum):
○描述: 定义了记忆内容支持的 MIME 类型枚举，例如 TEXT ("text/plain")。
●MemoryQueryResult(TypedDict):
○描述: query 方法返回结果的数据结构。
○主要字段:
■results (Sequence[MemoryContent]): 检索到的记忆内容列表。
■scores (Optional]): (可选) 每个检索结果的相关性得分。
●UpdateContextResult(TypedDict):
○描述: (可能已演变) update_context 方法返回结果的数据结构，通常包含更新后的消息上下文。
●ListMemory(Memory):
○描述: Memory 协议的一个简单实现，它将记忆条目按时间顺序存储在一个列表中 26。当更新上下文时，它通常会附加最近的记忆条目。
○特点: 实现简单，行为可预测，易于理解和调试。
○适用场景: 适用于简单的记忆需求或作为更复杂记忆实现的起点。
autogen_core.memory 模块提供的接口为构建各种记忆系统奠定了基础。虽然 ListMemory 是一个基础实现，但开发者可以基于 Memory 协议创建更高级的记忆存储，例如使用向量数据库 (ChromaDB, FAISS 等) 进行语义相似性检索，或与知识图谱集成。这些高级实现通常位于 autogen_ext.memory 包中，如 autogen_ext.memory.chromadb.ChromaDBVectorMemory 26。
autogen_core.exceptions (异常处理)
autogen_core.exceptions 模块定义了 AutoGen 核心框架中使用的自定义异常类型。这些异常用于指示在智能体交互、消息传递或组件操作过程中发生的特定错误情况。理解这些异常类型对于开发者编写健壮的错误处理逻辑和调试 AutoGen 应用非常重要。
主要异常类型:
●CantHandleException(Exception):
○描述: 当一个智能体或组件接收到一个它无法处理的请求或消息时，可能会抛出此异常。
○应用场景: 例如，一个专门处理文本的智能体接收到它不支持的多模态消息，或者一个组件收到了配置错误的任务。
●MessageDroppedException(Exception):
○描述: 当一条消息在传递过程中因为某种原因（例如，没有合适的订阅者、队列已满且无法阻塞、或被干预处理器明确丢弃）而被丢弃时，可能会记录或抛出此异常。
○应用场景: 帮助诊断消息未能到达预期接收者的问题。
●NotAccessibleError(Exception):
○描述: 当尝试访问一个不可访问的资源或执行一个不允许的操作时抛出。例如，尝试访问一个未初始化或已关闭的组件。
○应用场景: 确保组件在使用前已正确初始化和配置。
●UndeliverableException(Exception):
○描述: 当一条消息因为无法找到目标接收者或无法通过网络传递（在分布式场景中）而被确认为无法投递时，可能会抛出此异常。
○应用场景: 在消息传递失败时提供明确的错误信号。
除了这些通用的核心异常外，其他特定模块（如 autogen_core.tool_agent）可能还会定义更具体的异常类型，例如 ToolNotFoundException 或 InvalidToolArgumentsException 25。
通过捕获和处理这些特定的 AutoGen 异常，开发者可以构建出对各种运行时问题更具弹性的智能体应用，并能为最终用户提供更友好的错误提示或回退机制。
autogen_core.logging (日志记录)
autogen_core.logging 模块定义了 AutoGen 核心框架中用于结构化日志记录的事件类型和相关枚举。AutoGen 使用 Python 内置的 logging 模块，并通过定义特定的事件类来标准化关键操作和状态变化的日志输出。这有助于开发者追踪智能体的行为、调试问题以及监控系统性能。
核心日志事件类型 (通常为 TypedDict 或 Pydantic 模型):
●MessageEvent(TypedDict):
○描述: 与消息传递相关的通用事件。
○主要字段: timestamp (float), message_id (str), source_agent_id (Optional[str]), target_agent_id (Optional[str]), topic_id (Optional[str]), message_kind (MessageKind), delivery_stage (DeliveryStage), payload (Any).
●LLMCallEvent(TypedDict):
○描述: 当对大型语言模型 (LLM) 进行调用时记录的事件。
○主要字段: timestamp (float), client_id (str) (模型客户端的ID), model_id (str) (所用模型的ID), messages (Sequence[LLMMessage]) (发送给模型的输入消息), response (Optional) (模型的原始响应), cost (Optional[float]), usage (Optional) (token使用情况), cached (bool) (响应是否来自缓存)。
●LLMStreamStartEvent(TypedDict) 和 LLMStreamEndEvent(TypedDict):
○描述: 分别在 LLM 流式响应开始和结束时记录的事件。
●ToolCallEvent(TypedDict):
○描述: 当工具被调用时记录的事件。
○主要字段: timestamp (float), agent_id (str) (调用工具的智能体ID), tool_name (str), arguments (Mapping[str, Any]), result (Optional) (工具执行结果)。
●MessageDroppedEvent(TypedDict):
○描述: 当一条消息被丢弃时记录的事件。
○主要字段: timestamp (float), message_id (str), reason (str) (丢弃原因)。
●MessageHandlerExceptionEvent(TypedDict):
○描述: 当消息处理程序中发生未捕获的异常时记录的事件。
○主要字段: timestamp (float), agent_id (str), message_id (str), exception_type (str), exception_message (str), stack_trace (str)。
●AgentConstructionExceptionEvent(TypedDict):
○描述: 当智能体构造过程中发生异常时记录的事件。
相关枚举:
●MessageKind(str, Enum):
○描述: 消息的种类，例如 USER (用户消息), ASSISTANT (助手消息), SYSTEM (系统消息), FUNCTION_CALL (函数调用), FUNCTION_RESULT (函数结果)。
●DeliveryStage(str, Enum):
○描述: 消息传递的阶段，例如 SENDING (发送中), DELIVERED (已送达), PROCESSING (处理中), HANDLED (已处理)。
日志记录器名称:
autogen_core 定义了几个标准的日志记录器名称，开发者可以通过这些名称获取并配置相应的日志记录器：
●ROOT_LOGGER_NAME = "autogen_core" 19
●EVENT_LOGGER_NAME = "autogen_core.events" 19 (用于上述结构化事件)
●TRACE_LOGGER_NAME = "autogen_core.trace" 19 (用于更详细的开发者追踪日志)
通过配置这些日志记录器的级别和处理器 (handler)，开发者可以将 AutoGen 应用的内部行为输出到控制台、文件或其他日志聚合系统，从而实现有效的监控和调试。例如，AgentChat 的日志配置就是基于这些核心日志记录器名称进行的 10。
autogen_core.component (组件化)
autogen_core.component 模块是 AutoGen 框架设计哲学的核心体现之一，即“万物皆组件 (everything as a component)”。该模块提供了一套基类和协议，使得 AutoGen 中的各种元素——如智能体 (Agent)、工具 (Tool)、模型客户端 (Model Client)、记忆模块 (Memory)、代码执行器 (Code Executor) 甚至聊天完成上下文 (ChatCompletionContext)——都能够被视为可配置、可序列化和可动态加载的组件 19。
这种组件化架构带来了诸多好处：
●标准化配置: 组件可以拥有一个明确定义的配置模式 (schema)，通常通过 Pydantic 模型实现，使得配置过程更加规范和易于验证。
●可序列化与持久化: 许多组件实现了状态的保存 (save_state, dump_component) 和加载 (load_state, _from_config) 方法，允许将组件的状态或完整配置序列化（例如为 JSON），以便持久存储或在不同会话间传递 12。
●可重用性: 设计良好的组件可以在不同的应用或智能体团队中被重用。
●可扩展性: 开发者可以创建新的自定义组件，只要它们遵循相应的组件协议，就能无缝集成到 AutoGen 生态系统中。
●动态加载: 通过 ComponentLoader，可以根据配置动态加载和实例化组件，这为构建灵活和可插拔的系统提供了可能。
●简化集成: 例如，AutoGen Studio 等工具可以利用这种组件模型来提供图形化的界面，让用户能够配置和组合不同的智能体和工具，而无需编写大量代码。
核心类与概念:
●Component(Protocol):
○描述: 定义了组件的基本协议。一个组件通常需要指定其类型 (component_type) 和配置模式 (component_config_schema)。
●ComponentBase(ABC):
○描述: 组件接口的基类，可能提供了一些通用的组件相关功能。
●ComponentModel(BaseModel):
○描述: 一个 Pydantic 模型，用于表示组件的配置。它通常包含以下字段 19:
■provider (str): 组件的提供者或来源（例如，模块路径）。
■component_type (ComponentType): 组件的类型（如 'agent', 'model', 'tool'）。
■version (str): 组件配置的版本。
■component_version (str): 组件本身的实现版本。
■description (Optional[str]): 组件的描述。
■label (Optional[str]): 组件的标签。
■config (Mapping[str, Any]): 特定于该组件类型的配置参数字典。
●ComponentToConfig(Protocol):
○描述: 定义了组件如何将其自身转换为可序列化配置的接口。
○主要方法:
■_to_config(self) -> Mapping[str, Any]: 返回组件的配置字典。
■dump_component(self) -> ComponentModel: 返回一个完整的 ComponentModel 实例。
○类变量: component_type, component_version, component_provider_override, component_description, component_label。
●ComponentFromConfig(Protocol):
○描述: 定义了组件如何从配置对象创建实例的接口。
○主要类方法:
■_from_config(cls, config: ComponentModel) -> "ComponentFromConfig": 从 ComponentModel 创建组件实例。
●ComponentLoader:
○描述: 提供了加载组件的实用功能。
○主要方法: load_component(config: Union]) -> Any: 根据给定的配置（可以是 ComponentModel 实例或字典）动态加载并实例化组件。
●ComponentType(TypeAlias):
○描述: 一个类型别名，通常是一个包含预定义组件类型字符串（如 'model', 'agent', 'tool', 'termination', 'token_provider', 'workbench'）的 Literal 类型，或者是一个通用的 str 19。
●is_component_class(obj: Any) -> bool 和 is_component_instance(obj: Any) -> bool:
○描述: 用于检查一个对象是否为组件类或组件实例的辅助函数。
几乎 AutoGen 中所有重要的构建块，从 AssistantAgent 12 到 InMemoryStore 19，再到各种模型客户端和代码执行器，都直接或间接地利用了这个组件模型。这使得 AutoGen 框架具有高度的灵活性和可维护性，是其能够支持复杂和多样化 AI 应用的关键架构特性。
III. AutoGen Extensions API 参考 (autogen_ext)
autogen_ext 模块概述 (Module Overview)
autogen_ext 包是 AutoGen 框架中一个至关重要的组成部分，它包含了对 autogen_core 中定义的接口和协议的具体实现，并提供了大量预构建的、可直接使用的功能扩展 2。这些扩展极大地丰富了 AutoGen 的能力，使得开发者可以轻松集成各种外部服务和库，从而加速多智能体应用的开发。
autogen_ext 的内容广泛，主要可以归类为以下几个方面 8：
●特定智能体实现 (autogen_ext.agents.*): 提供具有特定功能的预构建智能体，例如与特定服务（如 OpenAI Assistants API、Azure AI 服务）集成的智能体，或用于特定任务（如网页浏览、文件操作）的智能体。
●模型客户端实现 (autogen_ext.models.*): 包含与各种大型语言模型 (LLM) 服务提供商（如 OpenAI, Azure OpenAI, Anthropic, Ollama 等）进行交互的客户端实现。
●工具实现 (autogen_ext.tools.*): 提供一系列即用型工具，智能体可以利用这些工具来执行代码、进行网络搜索、与 API 交互等。
●代码执行器实现 (autogen_ext.code_executors.*): 提供多种代码执行环境的实现，如本地命令行执行、Docker 容器内执行、Jupyter 内核执行以及基于云的执行服务。
●缓存存储实现 (autogen_ext.cache_store.*): 提供具体的缓存机制，如磁盘缓存和 Redis 缓存，用于缓存 LLM 调用结果等，以提高性能和降低成本。
●运行时实现 (autogen_ext.runtimes.*): 提供具体的智能体运行时环境实现，例如支持分布式智能体系统的 gRPC 运行时。
●记忆模块实现 (autogen_ext.memory.*): 提供更高级的记忆存储实现，例如与向量数据库集成的记忆模块，以支持检索增强生成 (RAG)。
●认证模块 (autogen_ext.auth.*): 提供特定认证机制的实现，如 Azure AD 令牌提供者。
通过使用 autogen_ext 中的组件，开发者可以避免从头开始编写与外部服务集成的底层代码，专注于应用的核心逻辑和智能体之间的协作。该包的设计也鼓励社区贡献新的扩展，从而不断增强 AutoGen 生态系统的功能。
autogen_ext.agents.* (扩展代理)
autogen_ext.agents 模块及其子模块提供了 autogen_core.BaseAgent 或 autogen_agentchat.BaseChatAgent 的一系列具体实现，这些智能体通常针对特定平台、服务或任务进行了优化和封装，提供了开箱即用的高级功能。
主要扩展智能体类型:
●autogen_ext.agents.openai.OpenAIAssistantAgent:
○描述: 此智能体与 OpenAI 的 Assistants API 进行集成。它允许 AutoGen 应用利用 OpenAI Assistants API 的特性，如持久化线程、内置工具（如代码解释器、文件检索）以及用户自定义的函数。
○关键功能: 管理 Assistants API 中的助手 (Assistant) 和线程 (Thread)，处理运行步骤 (Run steps)，以及与 Assistants API 的工具调用机制进行交互。
○适用场景: 希望利用 OpenAI Assistants API 的托管功能和状态管理，同时将其整合到更广泛的 AutoGen 多智能体协作流程中的应用。
○相关 Snippets: 1。
●autogen_ext.agents.web_surfer.MultimodalWebSurfer:
○描述: 一个多模态智能体，专门设计用于与网页进行交互。它通常使用 Playwright 或类似的浏览器自动化库来浏览网页、提取文本内容、获取截图，并能理解和响应包含图像的多模态信息 6。
○关键功能: 网页导航（点击链接、填写表单）、内容提取、屏幕截图、处理多模态输入（结合文本和图像进行网页理解）。
○依赖组件: 通常需要一个 LLM 客户端来理解任务和网页内容，并决定下一步操作；以及一个浏览器控制组件如 PlaywrightController 11。
○适用场景: 需要从网页上收集信息、执行基于 Web 的任务（如预订、信息查询）或进行网页内容分析的应用。
○相关 Snippets: 2。
●autogen_ext.agents.file_surfer.FileSurfer:
○描述: 一个设计用于在本地文件系统中导航、搜索和读取文件内容的智能体 8。
○关键功能: 列出目录内容、读取文件、搜索文件、理解文件结构。
○适用场景: 需要智能体访问和处理本地文件以完成任务的应用，例如代码理解、文档问答、日志分析等。
●autogen_ext.agents.video_surfer.VideoSurfer:
○描述: 一个专门用于处理和理解视频内容的智能体。它可能包含提取音频、转录语音、在特定时间点截取视频帧等工具 8。
○相关工具 (autogen_ext.agents.video_surfer.tools): extract_audio(), get_screenshot_at(), get_video_length(), transcribe_audio_with_timestamps() 等 11。
○适用场景: 视频内容摘要、视频问答、从视频中提取特定信息等。
●autogen_ext.agents.azure.AzureAIAgent:
○描述: (推测) 此智能体可能与 Azure AI 服务（如 Azure AI Studio 中的特定模型或功能）进行集成，提供针对 Azure 平台的优化或特定功能。
○相关 Snippets: 8。
●autogen_ext.agents.magentic_one.MagenticOneCoderAgent:
○描述: 作为 Magentic-One 架构一部分的编码智能体，可能专门用于代码生成、理解或调试任务 8。
○相关 Snippets: 4 (Magentic-One 整体介绍)。
这些扩展智能体通过封装特定领域的知识和工具，极大地简化了构建能够执行复杂、现实世界任务的多智能体系统。开发者可以直接使用这些预构建的智能体，或者将它们作为创建更专业化自定义智能体的基础。
autogen_ext.models.* (模型客户端实现)
autogen_ext.models 模块及其子模块提供了与各种大型语言模型 (LLM) 服务提供商进行交互的具体客户端实现。这些客户端都实现了 autogen_core.models.ChatCompletionClient 协议，使得 AutoGen 框架的上层组件（如 AssistantAgent）能够以统一的方式使用不同的 LLM。
主要模型客户端实现:
●autogen_ext.models.openai:
○OpenAIChatCompletionClient:
■描述: 用于与 OpenAI 的聊天补全 API (如 GPT-4, GPT-3.5-turbo, GPT-4o) 进行交互的客户端 6。
■主要参数: model (模型名称), api_key (OpenAI API 密钥), organization (可选的组织 ID), base_url (可选的基础 URL，用于代理或兼容 API), timeout, max_retries, model_info (可选的模型能力信息), 以及其他传递给 OpenAI API 的参数如 frequency_penalty, max_tokens, temperature, top_p 等 29。
○AzureOpenAIChatCompletionClient:
■描述: 用于与 Azure OpenAI 服务的聊天补全 API 进行交互的客户端 29。
■主要参数: model (模型名称), azure_endpoint (Azure OpenAI 端点 URL), azure_deployment (部署名称), api_version (API 版本), api_key (Azure OpenAI API 密钥) 或 azure_ad_token_provider (用于 Azure AD 认证) 29。其他参数与 OpenAIChatCompletionClient 类似。
○BaseOpenAIChatCompletionClient: 上述两个 OpenAI 相关客户端的基类。
○配置模型: AzureOpenAIClientConfigurationConfigModel, OpenAIClientConfigurationConfigModel, BaseOpenAIClientConfigurationConfigModel, CreateArgumentsConfigModel 用于这些客户端的配置序列化 29。
●autogen_ext.models.anthropic:
○AnthropicChatCompletionClient:
■描述: 用于与 Anthropic 的 Claude 系列模型进行交互的客户端 11。
■主要参数: model (Claude 模型名称，如 "claude-3-opus-20240229"), api_key (Anthropic API 密钥), 以及其他 Anthropic API 特定参数如 max_tokens_to_sample, temperature, top_k, top_p 30。
○AnthropicBedrockClientConfiguration: 也支持通过 AWS Bedrock 使用 Claude 模型。
○配置模型: AnthropicClientConfigurationConfigModel, AnthropicBedrockClientConfigurationConfigModel 等 30。
●autogen_ext.models.azure: (此处的 AzureAIChatCompletionClient 可能指与 Azure AI Studio 中更广泛的模型目录或特定 Azure AI 功能集成的客户端，区别于仅 Azure OpenAI 服务)
○AzureAIChatCompletionClient:
■描述: 用于与 Azure AI 聊天补全服务交互的客户端 11。
■配置模型: AzureAIChatCompletionClientConfig 11。
●autogen_ext.models.ollama:
○OllamaChatCompletionClient:
■描述: 用于与通过 Ollama 运行的本地 LLM (如 Llama 2, Mistral 等) 进行交互的客户端 11。
■主要参数: model (在 Ollama 中注册的模型名称), base_url (Ollama 服务器的 URL, 通常是 http://localhost:11434)。
○配置模型: BaseOllamaClientConfigurationConfigModel, CreateArgumentsConfigModel 11。
●autogen_ext.models.llama_cpp:
○LlamaCppChatCompletionClient:
■描述: 用于与通过 llama-cpp-python 库运行的 GGUF 格式 LLM 进行交互的客户端 12。
■适用场景: 在本地高效运行量化后的 LLM。
●autogen_ext.models.cache:
○ChatCompletionCache:
■描述: 一个包装器客户端，可以为任何其他 ChatCompletionClient 添加缓存功能 31。它将 LLM 的请求和响应存储在可配置的缓存存储 (如磁盘或 Redis) 中，当遇到相同的请求时，可以直接从缓存返回结果，从而减少 API 调用、降低延迟和成本。
■主要参数: client (被包装的 ChatCompletionClient 实例), store (CacheStore 实例，如 DiskCacheStore 或 RedisStore) 31。
●autogen_ext.models.replay:
○ReplayChatCompletionClient:
■描述: 一个特殊的客户端，用于重放预先录制的 LLM 交互序列。这对于测试、调试或演示非常有用，可以确保 LLM 的行为是确定性的 29。
下表总结了部分关键模型客户端及其用途：
客户端类 (Client Class)	LLM 服务/类型	中文描述
OpenAIChatCompletionClient	OpenAI API (GPT-4, GPT-3.5, etc.)	连接 OpenAI 官方 API。
AzureOpenAIChatCompletionClient	Azure OpenAI Service	连接 Azure 托管的 OpenAI 模型。
AnthropicChatCompletionClient	Anthropic API (Claude models)	连接 Anthropic 的 Claude 系列模型。
OllamaChatCompletionClient	Ollama (本地运行的 LLMs)	连接通过 Ollama 在本地运行的开源模型。
LlamaCppChatCompletionClient	Llama.cpp / GGUF (本地运行的量化 LLMs)	连接通过 llama-cpp-python 在本地运行的 GGUF 模型。
ChatCompletionCache	(包装器) 任何 ChatCompletionClient	为其他模型客户端添加缓存功能。
ReplayChatCompletionClient	(特殊) 预录制的交互	重放预先录制的 LLM 交互，用于测试和调试。
这些客户端的提供使得 AutoGen 能够灵活地适应不同的 LLM 后端，开发者可以根据项目需求、成本考虑和可用性选择最合适的模型服务。
autogen_ext.tools.* (工具实现)
autogen_ext.tools 模块及其子模块提供了多种即用型工具的具体实现，这些工具实现了 autogen_core.tools.BaseTool 协议，可以直接被 AssistantAgent 或其他支持工具使用的智能体所利用。这些工具扩展了智能体的能力，使其能够执行代码、与外部 API 交互、搜索信息等。
主要工具实现:
●autogen_ext.tools.code_execution.PythonCodeExecutionTool:
○描述: 允许智能体执行 Python 代码片段。这是 AutoGen 中最常用的工具之一，赋予智能体强大的编程和问题解决能力 34。
○工作方式: 它接收一个包含 Python 代码的字符串作为输入，并依赖于一个配置好的 CodeExecutor（在 autogen_core.code_executor 中定义接口，具体实现在 autogen_ext.code_executors.*）来实际运行代码。执行结果（包括标准输出、错误和退出码）会被返回。
○输入 (CodeExecutionInput): code (str): 要执行的 Python 代码。
○输出 (CodeExecutionResult): success (bool): 执行是否成功。 output (str): 代码的输出。
○依赖: 需要一个 CodeExecutor 实例（如 LocalCommandLineCodeExecutor 或 DockerCommandLineCodeExecutor）在初始化时传入 34。
○相关 Snippets: 34 (详细介绍及示例), 2。
●autogen_ext.tools.graphrag:
○描述: 提供了与 Microsoft GraphRAG 集成的工具，允许智能体在文档语料库上执行语义搜索和问答 35。GraphRAG 结合了图结构和语言模型来理解和查询非结构化数据。
○主要工具类:
■LocalSearchTool: 在本地索引的 GraphRAG 数据上执行搜索。
■GlobalSearchTool: 可能用于更全局或社区级别的搜索。
○配置: 需要预先完成 GraphRAG 的设置和索引过程，并提供相应的配置文件 (如 settings.yaml) 35。
○适用场景: 构建基于自有文档的 RAG (Retrieval Augmented Generation) 应用，如企业知识库问答、文档理解等。
○相关 Snippets: 11。
●autogen_ext.tools.azure.AzureAISearchTool:
○描述: 允许智能体使用 Azure AI Search (以前称为 Azure Cognitive Search) 服务进行搜索 7。
○功能: 查询 Azure AI Search 索引，检索相关文档或数据。
○配置: 需要提供 Azure AI Search 服务的端点、API 密钥和索引名称等信息 (AzureAISearchConfig)。
○适用场景: 将 Azure AI Search 的强大搜索能力集成到智能体应用中。
●autogen_ext.tools.mcp.McpWorkbench 和 mcp_server_tools():
○描述: McpWorkbench 是一个实现了 autogen_core.tools.Workbench 协议的类，用于与遵循模型-上下文协议 (Model-Context Protocol, MCP) 的外部工具服务器进行交互 6。MCP 是一种旨在标准化 LLM 与外部工具/服务之间通信的协议。mcp_server_tools() 可能是一个辅助函数，用于发现或列出 MCP 服务器提供的工具。
○适配器: StdioMcpToolAdapter 和 SseMcpToolAdapter 用于不同类型的 MCP 服务器通信（标准输入输出或 Server-Sent Events）。
○适用场景: 与实现了 MCP 的外部工具服务（可能是独立运行的进程或微服务）集成，允许 AutoGen 智能体使用这些远程工具。
●autogen_ext.tools.langchain.LangChainToolAdapter:
○描述: 提供了将 LangChain 工具适配为 AutoGen 工具的桥梁 1。这使得 AutoGen 智能体可以利用 LangChain 生态系统中丰富的工具集。
○适用场景: 希望在 AutoGen 应用中复用已有的 LangChain 工具或利用 LangChain 社区提供的工具。
●autogen_ext.tools.http.HttpTool:
○描述: 25 一个通用的 HTTP 请求工具，允许智能体发送 GET, POST 等 HTTP 请求到指定的 URL，并获取响应。
○适用场景: 与任何提供 HTTP API 的外部服务进行基本交互。
●autogen_ext.tools.semantic_kernel.KernelFunctionFromTool:
○描述: 25 允许将 AutoGen 工具转换为 Semantic Kernel 中的 Kernel Function，或反之，促进 AutoGen 和 Semantic Kernel 之间的互操作性。
这些工具实现为 AutoGen 智能体提供了与各种外部系统和服务交互的能力，是构建能够解决实际问题的复杂应用的关键。
autogen_ext.code_executors.* (代码执行器实现)
autogen_ext.code_executors 模块及其子模块提供了 autogen_core.code_executor.CodeExecutor 协议的具体实现。这些执行器负责在不同的环境中安全、可靠地运行由 LLM 生成或用户提供的代码。选择合适的代码执行器对于应用的安全性、依赖管理和可复现性至关重要。AutoGen 在这方面提供了多种选项，以满足不同场景的需求，这体现了其在处理 LLM 生成代码这一实际问题上的成熟度 21。
主要代码执行器实现:
1.autogen_ext.code_executors.local.LocalCommandLineCodeExecutor:
○描述: 在运行 AutoGen 应用的本地宿主机上直接通过命令行执行代码 21。代码块会被保存到临时文件然后执行。
○主要参数 (__init__):
■work_dir (Path): 代码执行的工作目录。
■virtual_env_context (Optional): (可选) 指定一个 Python 虚拟环境上下文（使用 venv 模块创建），代码将在此虚拟环境中执行，以隔离依赖 21。
○优点: 设置简单，无需额外依赖（如 Docker）。
○缺点与警告: 具有潜在安全风险，因为 LLM 生成的代码可能包含恶意指令或导致意外的系统更改。官方文档明确提示需谨慎使用 21。
○适用场景: 快速原型设计、受信任的代码源、或已采取其他安全措施的环境。
○相关 Snippets: 21 (详细介绍及示例), 21 (用户指南信息), 37 (警告), 11。
LocalCommandLineCodeExecutor 参数	类型	中文描述
work_dir	Path	代码执行的工作目录。
virtual_env_context	Optional	(可选) 用于执行代码的 Python 虚拟环境上下文。
2.autogen_ext.code_executors.docker.DockerCommandLineCodeExecutor:
○描述: 在 Docker 容器内执行代码。这为代码执行提供了一个隔离的环境，显著提高了安全性 21。
○主要参数 (__init__):
■image (str): 用于执行代码的 Docker 镜像名称，默认为 'python:3-slim' 36。镜像必须包含 sh 和 python。
■container_name (Optional[str]): (可选) Docker 容器的名称。
■timeout (int): 代码执行的超时时间（秒），默认为 60 36。
■work_dir (Optional[Union[Path, str]]): 容器内的工作目录。
■bind_dir (Optional[Union[Path, str]]): (可选) 将宿主机目录挂载到容器的工作目录。
■auto_remove (bool): 是否在容器停止后自动移除，默认为 True 21。
■stop_container (bool): 是否在执行器停止时自动停止容器，默认为 True 36。
■extra_volumes (Optional]]): (可选) 额外的卷挂载 38。
■init_command (Optional[str]): (可选) 在每个代码块执行前运行的初始化命令 38。
○优点: 安全性高，环境隔离，可自定义依赖环境（通过自定义 Docker 镜像）。
○安装: 需要安装 docker Python库 (pip install "autogen-ext[docker]") 36。
○“Docker out of Docker”: 支持在已容器化的 AutoGen 应用中再启动 Docker 执行器容器，需挂载 Docker socket (-v /var/run/docker.sock:/var/run/docker.sock) 21。
○适用场景: 大多数生产或需要安全代码执行的场景。
○相关 Snippets: 21 (详细介绍及示例), 36 (API 文档), 38 (参数列表), 1。
DockerCommandLineCodeExecutor 参数	类型	中文描述
image	str	用于执行代码的 Docker 镜像。
timeout	int	代码执行超时时间（秒）。
work_dir	Optional[Union[Path, str]]	容器内的工作目录。
auto_remove	bool	是否在容器停止后自动移除。
bind_dir	Optional[Union[Path, str]]	(可选) 挂载到容器工作目录的宿主机目录。
3.autogen_ext.code_executors.jupyter:
○JupyterCodeExecutor:
■描述: 通过连接到一个正在运行的 Jupyter 内核来执行代码。这允许在交互式、有状态的环境中执行代码，特别适合数据科学和需要逐步执行、检查中间结果的任务 11。
■JupyterCodeResult: Jupyter 执行器返回的特定结果类型。
○适用场景: 数据分析、机器学习实验、需要持久化会话状态的代码执行。
4.autogen_ext.code_executors.docker_jupyter:
○DockerJupyterCodeExecutor:
■描述: 结合了 Docker 的隔离性和 Jupyter 内核的交互性。它在 Docker 容器内启动一个 Jupyter 服务器和内核，然后连接到该内核执行代码 11。
■组件: DockerJupyterServer, JupyterClient, JupyterKernelClient。
○优点: 兼具安全隔离和交互式执行的优点。
○适用场景: 需要安全、隔离且具有交互式会话状态的代码执行环境。
5.autogen_ext.code_executors.azure.ACADynamicSessionsCodeExecutor:
○描述: 利用 Azure 容器应用 (Azure Container Apps, ACA) 的动态会话功能来执行代码。这是一种无服务器的代码执行方式，按需分配资源，并在执行完成后自动关闭 6。
○依赖: 通常需要 TokenProvider (如 autogen_ext.auth.azure.AzureTokenProvider) 进行 Azure 认证。
○优点: 无服务器、按需付费、可扩展、由 Azure 管理环境。
○适用场景: 需要可扩展、按需付费的云端代码执行环境，特别适合不希望自行管理 Docker 或 Jupyter 基础设施的场景。
选择合适的代码执行器是 AutoGen 应用设计中的一个重要决策，需要综合考虑安全性、易用性、环境依赖和成本等因素。
autogen_ext.cache_store.* (缓存存储实现)
autogen_ext.cache_store 模块提供了 autogen_core.CacheStore 协议的具体实现，用于持久化或共享缓存数据。在 AutoGen 中，缓存最常见的用途是与 autogen_ext.models.cache.ChatCompletionCache 结合使用，以缓存大型语言模型 (LLM) 的调用结果，从而减少 API 调用次数、降低延迟并节省成本 31。
主要缓存存储实现:
●autogen_ext.cache_store.diskcache.DiskCacheStore:
○描述: 使用 diskcache 库（一个基于磁盘的缓存库）作为后端存储。它将缓存数据存储在本地文件系统中 11。
○主要参数 (__init__):
■cache (diskcache.Cache): 一个 diskcache.Cache 实例，指向磁盘上的缓存目录。
○配置模型: DiskCacheStoreConfig，可能包含缓存目录路径等配置。
○优点: 设置简单，无需外部服务依赖，适合单机应用或开发环境。
○安装: 需要安装 diskcache 额外依赖 (pip install "autogen-ext[diskcache]") 31。
○使用示例 31:
Python
# import asyncio
# import tempfile
# from autogen_ext.models.cache import CHAT_CACHE_VALUE_TYPE
# from autogen_ext.cache_store.diskcache import DiskCacheStore
# from diskcache import Cache
#
# async def main():
#     with tempfile.TemporaryDirectory() as tmpdirname:
#         disk_cache = Cache(tmpdirname)
#         cache_store = DiskCacheStore(disk_cache)
#         # 然后可以将 cache_store 传递给 ChatCompletionCache
# asyncio.run(main())

●autogen_ext.cache_store.redis.RedisStore:
○描述: 使用 Redis（一个内存数据结构存储，可用作数据库、缓存和消息代理）作为后端存储 11。
○主要参数 (__init__):
■redis_client (redis.Redis): 一个连接到 Redis 服务器的 redis.Redis 客户端实例。
○配置模型: RedisStoreConfig，可能包含 Redis 连接参数（主机、端口、密码等）。
○优点: 高性能，支持分布式缓存（多个 AutoGen 应用实例可以共享同一个 Redis 缓存），适合生产环境和需要共享缓存的场景。
○安装: 需要安装 redis 额外依赖 (pip install "autogen-ext[redis]")。
○使用示例 (概念性) 31:
Python
# from autogen_ext.cache_store.redis import RedisStore
# import redis
#
# redis_instance = redis.Redis(host='localhost', port=6379, db=0)
# cache_store = RedisStore(redis_instance)
# # 然后可以将 cache_store 传递给 ChatCompletionCache

通过这些缓存存储实现，开发者可以根据应用的需求（单机 vs 分布式，性能要求，运维复杂度）选择合适的缓存后端，并与 ChatCompletionCache 配合使用，有效地优化 LLM 应用的性能和成本。
autogen_ext.runtimes.* (运行时实现)
autogen_ext.runtimes 模块提供了 autogen_core.AgentRuntime 协议的具体实现，特别是针对分布式智能体系统的运行时环境。autogen_core.SingleThreadedAgentRuntime 主要用于本地单进程开发和测试，而 autogen_ext 中的运行时则旨在支持更复杂的部署场景。
主要运行时实现:
●autogen_ext.runtimes.grpc.GrpcWorkerAgentRuntime:
○描述: 这是一个基于 gRPC (Google Remote Procedure Call) 的智能体运行时实现，专为构建分布式智能体系统而设计 1。它允许智能体在不同的进程甚至不同的机器上运行，并通过 gRPC 进行通信。
○核心组件:
■GrpcWorkerAgentRuntime: 作为客户端，连接到 gRPC 主机。
■GrpcWorkerAgentRuntimeHost: 作为 gRPC 服务器端，托管一个或多个智能体。
■GrpcWorkerAgentRuntimeHostServicer: gRPC 服务的具体实现。
○功能:
■远程智能体注册和发现。
■跨进程/机器的消息传递。
■支持智能体在独立的、可能具有不同依赖或语言环境（未来）的工作节点上运行。
○适用场景:
■需要将智能体部署到不同计算资源上的大规模应用。
■智能体具有不同的资源需求或依赖项，需要在隔离的环境中运行。
■构建具有高可用性和容错性的多智能体系统。
■实现跨语言的智能体互操作（尽管目前主要集中在 Python 和.NET 之间）。
○安装: 可能需要安装与 gRPC 相关的额外依赖 (pip install "autogen-ext[grpc]" 或类似命令)。
GrpcWorkerAgentRuntime 是 AutoGen 实现其“可扩展与分布式”核心特性的关键组件之一 3。它使得 AutoGen 应用能够从简单的本地原型验证，平滑地过渡到更复杂的、生产级别的分布式部署架构。这对于处理大规模任务、集成异构系统或构建需要跨越网络边界进行协作的智能体网络至
Works cited
1.AutoGen, accessed May 9, 2025, https://microsoft.github.io/autogen/
2.microsoft/autogen: A programming framework for agentic AI PyPi: autogen-agentchat Discord: https://aka.ms/autogen-discord Office Hour: https://aka.ms/autogen-officehour - GitHub, accessed May 9, 2025, https://github.com/microsoft/autogen
3.Core — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/index.html
4.AgentChat — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/index.html
5.AgentChat — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable//user-guide/agentchat-user-guide/index.html
6.Extensions — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/user-guide/extensions-user-guide/index.html
7.Changes in Autogen release 0.5.1 - Ravikanth Chaganti, accessed May 9, 2025, https://ravichaganti.com/blog/changes-in-autogen-release-0_5_1/
8.API Reference — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/index.html
9.autogen_agentchat — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_agentchat.html
10.Logging — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/logging.html
11.API Reference — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/dev/reference/index.html
12.autogen_agentchat.agents — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_agentchat.agents.html
13.Messages — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/tutorial/messages.html
14.Swarm — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/swarm.html
15.AutoGen v0.5.6 released : r/AutoGenAI - Reddit, accessed May 9, 2025, https://www.reddit.com/r/AutoGenAI/comments/1kdu20x/autogen_v056_released/
16.autogen_agentchat.teams — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_agentchat.teams.html
17.Releases · microsoft/autogen - GitHub, accessed May 9, 2025, https://github.com/microsoft/autogen/releases
18.Quickstart — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/quickstart.html
19.autogen_core — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_core.html
20.Quick Start — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/quickstart.html
21.Command Line Code Executors — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/components/command-line-code-executors.html
22.autogen/python/packages/autogen-core/tests/test_code_executor.py at main - GitHub, accessed May 9, 2025, https://github.com/microsoft/autogen/blob/main/python/packages/autogen-core/tests/test_code_executor.py
23.autogen_core.models._model_client — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/_modules/autogen_core/models/_model_client.html
24.autogen_core.model_context — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_core.model_context.html
25.autogen_core.tools — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_core.tools.html
26.Memory and RAG — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/user-guide/agentchat-user-guide/memory.html
27.AutoGen, accessed May 9, 2025, https://microsoft.github.io/autogen/stable//index.html
28.AutoGen, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/index.html
29.autogen_ext.models.openai — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_ext.models.openai.html
30.autogen_ext.models.anthropic — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable//reference/python/autogen_ext.models.anthropic.html
31.autogen_ext.models.cache — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_ext.models.cache.html
32.Caching in AutoGen V0.4.7 · microsoft autogen · Discussion #5792 - GitHub, accessed May 9, 2025, https://github.com/microsoft/autogen/discussions/5792
33.autogen_ext.models.cache — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/0.4.7/reference/python/autogen_ext.models.cache.html
34.autogen_ext.tools.code_execution — AutoGen, accessed May 9, 2025, https://microsoft.github.io/autogen/0.4.2/reference/python/autogen_ext.tools.code_execution.html
35.autogen_ext.tools.graphrag — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_ext.tools.graphrag.html
36.autogen_ext.code_executors.docker — AutoGen, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/reference/python/autogen_ext.code_executors.docker.html#autogen_ext.code_executors.docker.DockerCommandLineCodeExecutor
37.Code Execution — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/stable/user-guide/core-user-guide/design-patterns/code-execution-groupchat.html
38.autogen_ext.code_executors.docker — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/dev/reference/python/autogen_ext.code_executors.docker.html
39.API Reference — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/0.4.0/reference/index.html
40.API Reference — AutoGen - Microsoft Open Source, accessed May 9, 2025, https://microsoft.github.io/autogen/0.4.2/reference/index.html
41.AutoGen, accessed May 9, 2025, https://microsoft.github.io/autogen/dev/index.html
42.AutoGen, accessed May 9, 2025, https://microsoft.github.io/autogen/dev/