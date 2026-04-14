
## 第1章：深度研究并洞察如下产业界 agent memory system，撰写《agent memory system洞察》研究报告，要求进行技术方案的深度对比，可以参考以下四个层次的模型（C.A.P.E 框架）：

	1. 架构与底层范式层 (Architecture & Paradigm)
		- 技术分类 (Tech Taxonomy)：是基于 RAG 的外挂检索、基于 OS 的内存页置换，还是修改 Transformer 注意力机制的模型原生记忆？
		- 存储范式 (Storage Paradigm)：扁平向量（Flat Vector）、会话时序（Time-Series）、图数据库（GraphDB）、还是文件目录树（File System）？
		- 系统定位 (System Positioning)：是作为中间件插件、独立 Memory-as-a-Service 服务，还是直接内置于大模型底座？
		- XXX
		
	2. 认知与演进能力层 (Cognition & Evolution)
		- 自我进化 (Self-Evolution)：记忆是“死”的还是“活”的？系统是否具备后台反思（Reflection）、记忆融合（Fusion）、以及主动淘汰脏数据（Forgetting）的机制？
		- 结构化与推理能力 (Structural Reasoning)：能否处理复杂实体关系（如 A 隶属于 B，B 昨天被 C 修改）？
		- XXX
		
	3. 工程与生产力层 (Production & Engineering)
		- Token 节省效能 (Token Efficiency)：通过精准的上下文压缩和路由，能在多大程度上降低基础模型的推理成本（API 费用）？
		- 可观测性与可读性 (Observability & Readability)：当 Agent 出现幻觉或行为异常时，人类工程师能否直观地打开面板，查看 Agent “当时脑子里在想什么”（Traceability）？记忆数据对人类是否可读可写？
		- XXX

	4. 业务与生态层 (Business & Ecosystem)
		- 适用场景 (Use Cases)：适合 C 端闲聊陪伴、B 端复杂系统运维，还是多 Agent 仿真？
		- XXX
	5. 主要局限与短板 (Limitations)：
		- 部署成本、延迟瓶颈、生态锁死风险。
		- XXX
	
	6. Agent Memory System 的演进方向趋势
		- 如静态 -> 动态
		- 被动 -> 主动
		- 单体 -> 集体意识总线
		- XXX

### OpenViking（volcengine/OpenViking） + VikingBot
OpenViking is an open-source context database designed specifically for AI Agents(such as openclaw). OpenViking unifies the management of context (memory, resources, and skills) that Agents need through a file system paradigm, enabling hierarchical context delivery and self-evolving.
**问题背景**：传统 Agent 记忆分散（记忆在代码、资源在向量库、技能散落），检索黑箱、上下文不可分层、无法自我迭代，导致 token 成本高、调试难、长期记忆弱。

**技术方案**：采用**虚拟文件系统范式（viking:// 协议）**统一管理记忆、资源、技能。层次结构：
- `viking://user/memories/`、`agent/memories/`、`resources/` 等。
- 每项支持 **L0（摘要 ~100 tokens）→ L1（概览 ~2k tokens）→ L2（完整内容）** 分层加载。
- 检索：意图分析 + 向量预滤 + 目录递归探索 + 可视化轨迹。
- Session 管理：自动压缩对话、工具调用，异步提取长期记忆并更新 User/Agent 目录，实现**自进化循环**。
- VikingBot 是其上层 Agent 框架，提供 7 个专用工具（memory_commit 等）。

**优劣势**：
- **优势**：统一管理、可观测、可分层节省 token（基准显示 OpenClaw + OpenViking 节省 83-91% token，完成率提升 43-49%）；自我迭代让 Agent “越用越聪明”。
- **劣势**：依赖 VLM/Embedding 模型；AGPL-3.0 许可对商用有一定限制；早期项目需编译环境。

**演进趋势**：从 RAG 平面存储 → 层次化上下文工程；未来向 Rust 重写（RAGFS）、本地模型（vLLM/Ollama）演进，已集成 OpenClaw 等框架。
https://github.com/volcengine/OpenViking
https://openviking.ai/blog


### memsearch（zilliztech/memsearch）
**问题背景**：编码 Agent（Claude Code、OpenClaw 等）跨会话遗忘，记忆不可读、不可编辑、跨平台不共享，传统 RAG 缺乏渐进式检索和去重。

**技术方案**：**Markdown-first**（源头真相），每日日志 `memory/YYYY-MM-DD.md` + Milvus 向量影子索引。插件（Claude/OpenClaw 等）自动捕获并追加 haiku 摘要。检索采用**混合搜索（dense + BM25 + RRF）+ 3 层渐进披露**（search → expand → transcript）。支持 CLI/Python API、实时 watch、LLM 压缩。

**优劣势**：
- **优势**：人类可读、可 git 版本控制、跨 Agent 零配置共享、去重高效、token 节省显著。
- **劣势**：依赖 Milvus（即使 Lite 模式）；首次需下载嵌入模型。

**演进趋势**：从 OpenClaw 提取的记忆子系统 → 独立库，支持更多 IDE 插件、混合检索升级，体现“人类可读 + 向量加速”的混合趋势。

### Hermes Agent（nousresearch/hermes-agent）
**问题背景**：传统 Agent 缺乏跨会话学习、技能自动生成、用户画像建模，导致每次会话“从零开始”。

**技术方案**：**Markdown 持久记忆层**（MEMORY.md、USER.md、skills/ 目录）+ 闭环学习循环。Agent 自主在复杂任务后创建/迭代技能；FTS5 + LLM 摘要实现跨会话搜索；Honcho 建模用户行为。支持 MCP、Telegram/CLI 多表面，内置压缩工具。

**优劣势**：
- **优势**：真正“自我成长”Agent（技能自进化 + 用户画像）；低成本部署（$5 VPS）；可迁移 OpenClaw 记忆。
- **劣势**：Windows 支持需 WSL；大上下文需手动压缩。

**演进趋势**：向 RL 训练（Atropos）、批量轨迹生成演进，强调“Agent 即研究员”的研究级记忆系统。

### Letta(memGPT)
Letta is the platform for building stateful agents: AI with advanced memory that can learn and self-improve over time.
https://github.com/letta-ai/letta
https://docs.letta.com/letta-code/

### mem0：
Universal memory layer for AI Agents
**问题背景**：LLM 应用缺乏持久个性化记忆，导致重复解释偏好、高 token 消耗。

**技术方案**：**多级记忆（User/Session/Agent）** + 向量语义检索 + 自适应更新。Python/JS SDK 一行集成，支持插件（Claude/Cursor）、CLI、LangGraph 等框架。使用向量库（Valkey 等）存储，支持托管/自托管。

**优劣势**：
- **优势**：基准领先（+26% 准确率、90% 少 token）；通用层，易集成；自改进。
- **劣势**：依赖外部 LLM/向量库；自托管需运维。

**演进趋势**：v1.0 大升级（API 现代化 + 新向量支持），从单一 RAG → 通用记忆层，未来向企业分析/安全扩展。
https://github.com/mem0ai/mem0
https://mem0.ai/

### memos
AI memory OS for LLM and Agent systems(moltbot,clawdbot,openclaw), enabling persistent Skill memory for cross-task skill reuse and evolution.
**问题背景**：技能无法跨任务复用、记忆缺乏统一调度和反馈。

**技术方案**：**Memory OS** 概念，将记忆视为一等资源。统一 API + 图结构存储 + MemScheduler（Redis 异步）+ 多 Cube 知识库 + 反馈修正 + 多模态/工具记忆。支持本地 SQLite / 云部署。

**优劣势**：
- **优势**：技能持久进化、43%+ 准确率提升、72% token 节省、多代理隔离共享。
- **劣势**：需 Neo4j/Qdrant 等外部组件。

**演进趋势**：v2.0 重大升级（多模态 + 调度器 + Helm），向 MAG（Memory-Augmented Generation）完整 OS 演进。

https://github.com/MemTensor/MemOS
https://memos.openmem.net/


### EverOS/EverMemOS
Build, evaluate, and integrate long-term memory for self-evolving agents.
https://github.com/EverMind-AI/EverOS
https://arxiv.org/pdf/2601.02163
https://mp.weixin.qq.com/s/SrARqbLyNGBkwz059e1TcA
HyperMem 超图：给结构化记忆加关联（比如「足球→运动→周末」）
EverCore 记忆 OS：自动删无用记忆、高频记忆优先读取
基准测试：用标准答案对比，算记忆准确率
@article{hu2026evermemos,
  title   = {EverMemOS: A Self-Organizing Memory Operating System for Structured Long-Horizon Reasoning},
  author  = {Chuanrui Hu and Xingze Gao and Zuyi Zhou and Dannong Xu and Yi Bai and Xintong Li and Hui Zhang and Tong Li and Chong Zhang and Lidong Bing and Yafeng Deng},
  journal = {arXiv preprint arXiv:2601.02163},
  year    = {2026}
}

@article{yue2026hypermem,
  title   = {HyperMem: Hypergraph Memory for Long-Term Conversations},
  author  = {Juwei Yue and Chuanrui Hu and Jiawei Sheng and Zuyi Zhou and Wenyuan Zhang and Tingwen Liu and Li Guo and Yafeng Deng},
  journal = {arXiv preprint arXiv:2604.08256},
  year    = {2026}
}

@article{hu2026evaluating,
  title   = {Evaluating Long-Horizon Memory for Multi-Party Collaborative Dialogues},
  author  = {Chuanrui Hu and Tong Li and Xingze Gao and Hongda Chen and Yi Bai and Dannong Xu and Tianwei Lin and Xiaohong Li and Yunyun Han and Jian Pei and Yafeng Deng},
  journal = {arXiv preprint arXiv:2602.01313},
  year    = {2026}
}

### claude-mem
A Claude Code plugin that automatically captures everything Claude does during your coding sessions, compresses it with AI (using Claude's agent-sdk), and injects relevant context back into future sessions.
https://github.com/thedotmack/claude-mem
https://claude-mem.ai/


### mem9
Unlimited memory for OpenClaw
https://github.com/mem9-ai/mem9

### lossless-claw
Lossless Claw — LCM (Lossless Context Management) plugin for OpenClaw
https://github.com/Martian-Engineering/lossless-claw

### memU
Memory for 24/7 proactive agents like openclaw (moltbot, clawdbot).
- 为openclaw/moltbot等24/7 proactive agents设计
- 结合多个社区扩展：memu-cowork、memu-sillytavern-extension
- **技术栈**: Python + OpenClaw集成
- **演进**: 已有3代社区实现（memov.ai、memovyn等）
**问题背景**：24/7 主动 Agent 需要低成本长期上下文，但传统方案 token 爆炸、无法主动捕捉意图。

**技术方案**：**文件系统式分层记忆**（Category/Item/Resource + 符号链接），支持 RAG + LLM 双模式检索。主动式：自动分类、模式检测、上下文预测。集成 openclaw 等，支持 PostgreSQL/pgvector，多模态输入。

**优劣势**：
- **优势**：token 成本降至 1/10；92%+ Locomo 准确率；真正 24/7 主动。
- **劣势**：文档中未明确提及局限，但依赖 LLM/嵌入模型。

**演进趋势**：从 openclaw 生态衍生，v1.x 迭代强调多代理协作、多模态、云托管（memu.so）。

https://github.com/NevaMind-AI/memU
https://memu.pro/

### Ori-Mnemos
Local-first persistent agentic memory powered by Recursive Memory Harness (RMH). Open source must win.
https://github.com/aayoawoyemi/Ori-Mnemos
https://orimnemos.com/

### langmen
https://github.com/langchain-ai/langmem
https://langchain-ai.github.io/langmem/

### honcho
Memory library for building stateful agents
https://github.com/plastic-labs/honcho
https://docs.honcho.dev/

### ContextLoom
ContextLoom is the shared "brain" for multi-agent systems. It weaves together memory threads from frameworks like DSPy and CrewAI into a unified, persistent context, powered by Redis and hydrated from your existing databases.
https://github.com/danielckv/ContextLoom
https://danielckv.dev/

### eion
Shared Memory Storage for Multi-Agent Systems
https://github.com/eiondb/eion
https://www.eiondb.com/

### mindforge
MindForge is a Python library designed to provide sophisticated memory management capabilities for AI agents and models. It combines vector-based similarity search, concept graphs, and multi-level memory structures (short-term, long-term, user-specific, session-specific, and agent-specific) to enable more context-aware and adaptive AI responses.
https://github.com/aiopsforce/mindforge

### minecontext
MineContext is your proactive context-aware AI partner（Context-Engineering+ChatGPT Pulse）
https://github.com/volcengine/MineContext

### Memorizing Transformers
https://arxiv.org/abs/2203.08913

### memoryllm
https://github.com/wangyu-ustc/MemoryLLM
https://arxiv.org/abs/2402.04624

### acontext
Agent Skills as a Memory Layer
https://github.com/memodb-io/Acontext

### ultraContext
Open Source Context infrastructure for AI agents. Auto-capture and share your agents' context everywhere.
https://github.com/ultracontext/ultracontext
https://ultracontext.com/

### MemaryAI
This is an open-source project that provides an efficient memory layer for autonomous AI agents, helping AI agents better manage and utilize information by simulating how human memory works
https://github.com/MemaryAI/MemaryAI


### MindOS - 人机协作心智系统
  - 全局同步心智
  - 透明可控的Agent行为
  - 共生演进逻辑
https://github.com/GeminiLight/MindOS  

### 知识图谱
查看完整知识图表系统列表: [160+ Graph Memory Systems](https://github.com/search?q=knowledge+graph+memory+system&sort=stars)

### 向量数据库
向量数据库详细对比: [67+ Vector Database Implementations](https://github.com/search?q=vector+database+memory+embedding&sort=stars)


## 第2章： 网络上（google scholar、arXiv）全文检索“Agent Memory+ (Episodic / Semantic / Working)+ (Formation / Retrieval / Evolution)+ (Vector DB / Graph Memory / RAG)+ (Reflection / Self-evolving / Continual Learning)+ 
(Multi-agent / Shared Memory)+ (Evaluation / MemBench / LongMemEval)”，并研究检索到的所有论文，按照业务场景、问题挑战、技术方案或创新技术或解决方案、效果、优劣势、演进趋势

### 记忆：kvcache复用（感知记忆的更新，上文感知语义管理） ：降低记忆长度（信息熵）、承载更有价值的记忆

### [Awesome-Agent-Memory](https://github.com/TeleAI-UAGI/Awesome-Agent-Memory)



## 第3章：基于《agent memory system洞察》研究报告，借鉴如上agent memory system研究，参考如下方向，面向构建通用agent的memory系统，撰写技术解决方案，要求从业务场景、问题挑战、技术方案或创新技术或解决方案、差异化竞争优势、测评标准benchmark、预期效果维度：

### entire.io
非纯 GitHub 记忆仓库，而是 AI 编码/Agent 平台。其 Dispatch 更新重点优化**大仓库记忆、检查点、Agent 更新**，体现商业产品中“内存改进 + 远程仓库支持”的实践应用。非独立开源记忆层，但验证了分层记忆在实际编码 Agent 中的价值。

### User as Code（用代码表示用户记忆）
GitHub 未发现独立仓库，此为**前沿概念**：将用户信息/偏好编码为**可执行代码**（如 Python 函数、脚本、规则引擎），而非文本/结构化数据。Agent 可直接“执行”用户记忆，实现动态行为适配（如自动调用特定工具、应用自定义逻辑）。优势在于**可编程性、动态更新**；挑战是安全性、解释性、可维护性。未来可能与技能自进化结合，成为 Agent 记忆的“可执行层”。

### xiaoclaw-memory
Zero-cost layered memory system for 24/7 AI Agents. Inspired by memU, powered by pure Markdown.
https://github.com/huafenchi/xiaoclaw-memory
