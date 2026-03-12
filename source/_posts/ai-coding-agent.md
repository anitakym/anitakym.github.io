---
title: ai-coding-agent
date: 2025-09-22 11:24:43
tags:
---
- https://repomix.com/

- https://osawards.com/javascript/

以下基于你给的参考信息，对 Cline 功能做一份精炼分析与实用建议。

一、定位与架构
- VS Code 插件，开源的 Coding Agent，主打“Agent 模式”，不做 Tab 式自动补全。
- 双模式：Plan（需求澄清、方案设计）→ Act（按计划执行修改/运行/浏览器操作）。
- 通过一组工具链把 LLM 与本地开发环境打通：文件系统、终端、浏览器模拟等。

二、内置能力与工具
- 文件/项目操作：read_file、write_to_file、replace_in_file、search_files、list_files、list_code_definition_names 等。
- 终端执行：execute_command，跑构建、测试、脚本。
- 浏览器模拟：基于 Claude 3.5 Sonnet 的 Computer Use，做页面交互/验证。
- 安全与变更控制：
  - 忽略敏感文件读取（如 .env、.pem）。
  - 可配置哪些操作自动批准，其他需人工 Approve。
  - CheckPoint/Snapshot：每步保存快照，便于回滚和审计。
- 上下文感知：
  - 支持 @ 提及 文件/文件夹/URL/Terminal。
  - 利用 VS Code 上下文（可见编辑器、打开的 tab、终端输出、诊断信息等）。
- 协议与生态：支持 MCP，便于接入更多外部工具/服务。
- 成本与性能：有 Prompt Caching、上下文窗口管理、Token 计量；但同任务下 Token 消耗通常高于 Cursor。

三、典型工作流（建议）
1) Plan：让 Cline 收集需求与代码上下文，产出任务清单/方案（审阅确认）。
2) Act：按计划逐步修改代码、跑命令、开浏览器验证；每步由你批准关键动作。
3) 复核：查看 diff/快照，跑测试与构建，必要时回滚某步快照。
4) 收尾：生成变更说明、测试报告或提交信息。

四、适用场景
- 代码重构/批量替换、跨目录联动修改。
- 生成/完善单元测试，修复构建与依赖问题。
- 脚手架搭建、端到端小特性交付。
- 页面联调：修改前端代码并用浏览器模拟验证。

不适合/限制
- 不是日常“码字式补全”，与 Cursor 的实时补全体验不同。
- 超大仓库且缺乏清晰边界时，计划与上下文管理成本升高。
- Token 成本相对高，需设置预算与缓存策略。

五、安全与治理建议
- 设置敏感文件忽略清单；限制高风险命令（白名单/需手动批准）。
- 开启每步快照；重要改动点必须人工 Review。
- 使用低权限 Shell/工作目录，避免全局破坏。
- 监控 Token 用量，开启 Prompt 缓存；为大任务拆分阶段性 Plan/Act。

六、与 Cursor/其他 Agent 的差异要点
- Cline：Agent 优先、可视化变更与批准流、开源、工具齐全；资源消耗偏大。
- Cursor：补全体验更强，Agent 更“内聚”，Token 使用更克制；闭源。

七、落地配置提示（VS Code/macOS）
- 安装 Cline 插件 → 配置 LLM 提供商与 API Key（按需开启 Computer Use）。
- 配置敏感文件忽略与操作审批策略。
- 首次使用先在小仓库或分支演练，观察 Token 和变更质量。

总结
Cline 适合把“从需求到落地”的小到中型开发任务交给 Agent 流程化执行，强调可控性与可回溯性。在不追求实时补全的团队中，可作为“执行型 Agent”与现有工具链互补。




### reference
https://github.com/cline/cline
https://github.com/RooVetGit/Roo-Code
https://www.nazha.co/posts/how-cline-works
https://github.com/cline/cline/blob/main/src/core/prompts/system.ts


核心模块。Cline 的源码主要分为以下几个核心模块，各司其职。

Webview UI 层 (webview-ui/)： 基于 React 和 VSCode Webview UI Toolkit 构建用户界面，负责用户交互、状态展示和用户指令的传递。
Extension Core 层 (src/core/)： Cline 的核心逻辑所在，负责任务流程编排、工具调用管理、提示工程和对话管理。Cline.ts 是该层级的核心类，协调各个子模块完成复杂的编码任务。
Integrations 层 (src/integrations/)： 封装了 Cline 与 VS Code 各个子系统的集成逻辑，例如编辑器 (editor/)、终端 (terminal/)、浏览器 (browser/)、Checkpoints (checkpoints/) 和 Diagnostics (diagnostics/) 等。
Services 层 (src/services/)： 提供了各种独立的服务模块，例如身份验证 (auth/)、MCP 服务器连接 (mcp/)、文件系统操作 (glob/)、代码解析 (tree-sitter/) 和日志记录 (logging/) 等。
API 层 (src/api/)： 负责与各种 AI 模型 API 进行交互，包括 Anthropic、OpenAI、Bedrock、Vertex、Gemini 等，并提供统一的 API 接口和数据转换层，providers/ 目录下包含了各种 API Provider 的 Handler 实现。
2）一些核心流程。

任务执行流程： 在 Cline.ts 中，可以看到 Cline 如何通过 recursivelyMakeClineRequests 方法，将用户任务分解为一系列步骤，并循环调用各种工具来逐步完成任务。
工具调用流程： 以 execute_command 工具为例，TerminalManager.ts 负责终端的创建和管理，TerminalProcess.ts 封装了命令执行和输出处理的细节，Cline.ts 则负责工具参数的组装、用户授权的请求和工具执行结果的处理。
上下文管理流程： Cline.ts 中的 loadContext 方法揭示了 Cline 如何收集和处理上下文信息，包括工作区文件结构、可见编辑器、打开的选项卡、终端输出和问题诊断等。ClineIgnoreController.ts 则包含了 .clineignore 功能的具体实现，以及如何控制 Cline 对工作区文件的访问权限。
MCP： McpHub.ts 负责 MCP Server 的连接管理、工具和资源的发现与加载。