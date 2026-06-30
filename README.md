# vibecoding-workflow

`vibecoding-workflow` 是一个用于启动小型软件项目的 Codex Skill。

它的目标是把一个粗略想法快速转成可执行的开发上下文，包括：

- `doc/proposal.md`：轻量需求文档
- `doc/detailed-design.md`：详细设计文档
- `doc/tasks/*.md`：按模块拆分的最小可执行任务
- `doc/tasks/progress.md`：总体进度
- `doc/prompt.md`：主 Agent 启动 Prompt

它适合小工具、原型、个人项目、轻量应用、脚本、Dashboard、实验性产品等场景。它不追求完整工程治理，而是帮助项目快速、清楚、可验证地开工。

## 工作流

`vibecoding-workflow` 会按轻量流程推进：

```text
Clarify → Brainstorm → Specify → Design → Plan → Launch
```

- `Clarify`：确认项目目标、用户、已有资料、技术约束、边界和验收标准。
- `Brainstorm`：当用户还不知道怎么设计、怎么开发、怎么拆功能或怎么选技术方向时，提出 2-3 个方案，比较取舍，并推荐一个默认方向。
- `Specify`：生成 `doc/proposal.md`，把项目目标、需求、非目标和验收标准写清楚。
- `Design`：生成 `doc/detailed-design.md`，明确模块、接口、数据结构、关键流程和验证策略。
- `Plan`：生成 `doc/tasks/*.md` 和 `doc/tasks/progress.md`，把设计拆成可执行、可验证的小任务。
- `Launch`：生成 `doc/prompt.md`，作为主 Agent 后续执行项目的启动 Prompt。

其中 `Brainstorm` 是条件触发的：如果项目方向已经清楚，就跳过；如果用户需要设计或实现思路，就先帮用户选方向，再进入文档和任务拆分。

## 灵感来源

这个 Skill 的灵感来自 B 站 UP 主“隔壁的程序员老王”的视频：[《VibeCoding就该这么做！》](https://www.bilibili.com/video/BV1YP5W6ZEP9/)。

它在这个思路上进一步结合了 `Superpowers` 的工程执行纪律，把“先形成需求、设计、任务和启动 Prompt，再让 Agent 执行”的流程整理成一个可复用的 Codex Skill。

## 和 Superpowers 的关系

`Superpowers` 更像一组通用工程执行纪律，强调 Agent 在编码过程中如何避免常见错误：

- 先澄清再实现
- 小步推进
- 测试驱动
- 系统化调试
- 完成前验证
- 避免无关重构

`vibecoding-workflow` 吸收了这些原则，但它不是 Superpowers 的替代品。

它更关注“开工前如何把想法变成可执行项目上下文”：

- 明确项目目标和边界
- 整理已有资料和技术约束
- 生成轻量需求文档
- 拆出模块和设计
- 把设计转成 Agent 可执行任务
- 生成后续开发用的启动 Prompt

简单说：

```text
Superpowers 关注：Agent 怎么把事情做稳。
vibecoding-workflow 关注：项目怎么从想法进入可执行状态。
```

## 和 OpenSpec 的关系

OpenSpec 更适合中大型项目、长期演进项目，或者需要正式规格治理的场景。它通常强调：

- 明确的规格结构
- 变更提案
- 设计评审
- 任务拆分
- 生命周期管理
- 后续演进和治理

这些能力很强，但对小项目来说可能偏重。

`vibecoding-workflow` 刻意保持轻量：

- 不引入复杂规格系统
- 不维护正式变更账本
- 不要求完整治理流程
- 不强制使用特定技术栈
- 不把小项目变成大项目流程

简单说：

```text
OpenSpec 关注：项目如何被长期、正式、可治理地演进。
vibecoding-workflow 关注：小项目如何快速形成清楚的开工上下文。
```

## 这个 Skill 的优势

### 1. 比直接 Vibe Coding 更稳

直接开始写代码很快，但容易出现几个问题：

- 需求边界不清
- Agent 擅自补功能
- 任务过大，难以验证
- 后续 Agent 接不上上下文
- 做完以后不知道是否真的完成

`vibecoding-workflow` 会先把项目拆成文档、设计、任务和验证标准，让后续开发更可控。

### 2. 比 OpenSpec 更轻

它只保留小项目真正需要的结构：

- 需求
- 设计
- 任务
- 进度
- 启动 Prompt

没有复杂流程，也不要求用户先学一套规格系统。

### 3. 比一次性 Prompt 更可复用

一次性 Prompt 模板需要用户手动复制、替换、调整，也很难根据不同项目状态稳定变形。

Skill 版本可以被 Codex 自动触发或显式调用，并且会根据当前项目上下文决定：

- 该问哪些问题
- 是否需要先 Brainstorm 几个方案
- 该生成哪些文档
- 任务应该拆到什么粒度
- 哪些验证方式适合当前技术栈
- 什么时候应该暂停向用户确认

### 4. 适合多 Agent 后续执行

生成的 `doc/prompt.md` 会明确主 Agent 和子 Agent 的协作方式：

- 主 Agent 负责整体进度、任务状态、协调和阶段验证
- 子 Agent 只处理单个模块或单个任务
- 每个任务都要有输入、输出、修改范围和验证方式

这让后续开发更容易并行，也更容易交接。

## 适用场景

适合：

- 从零启动一个小项目
- 把一句想法整理成开发计划
- 给 Agent 准备完整上下文
- 为原型或工具项目拆任务
- 在开工前明确验收标准

不适合：

- 已经很清楚的一行代码修改
- 大型组织级工程治理
- 需要正式规格审批的长期项目
- 需要严格 OpenSpec 流程的项目

## 安装

最简单的方式是直接告诉 AI：

```text
安装这个 skill：https://github.com/jedidevlab/vibecoding-workflow/blob/main/SKILL.md
```

安装后，重启 Codex 或开启新的 Codex 会话，让 Skill 被重新发现。

## 使用

显式调用：

```text
Use $vibecoding-workflow to turn this small project idea into requirements, design, tasks, and an agent launch prompt.
```

中文也可以：

```text
用 $vibecoding-workflow 帮我把这个小项目想法整理成需求文档、详细设计、任务拆分和 Agent 启动 Prompt。
```

## 文件结构

```text
vibecoding-workflow/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── README.md
```

其中：

- `SKILL.md` 是 Skill 的核心说明，Codex 会读取它来执行 workflow。
- `agents/openai.yaml` 是 Codex UI 元数据。
- `README.md` 面向 GitHub 读者，说明定位、安装和使用方式。
