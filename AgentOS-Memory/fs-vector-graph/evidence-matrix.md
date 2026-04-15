# Filesystem-like / Vector-Graph-like Agent Memory 证据矩阵

> 说明：
> - `类别` 按 `report_v3.md` 的主导接口划分
> - `证据等级` 含义见主报告
> - `主线结论` 表示该系统是否直接用于支撑报告的主结论
> - 访问与核验时间：2026-04-15

## 主线系统

| 系统 | 类别 | 一手来源 | 已核验的核心事实 | 公开量化 / 公开信号 | 证据等级 | 主线结论 | 备注 |
|------|------|----------|------------------|---------------------|----------|----------|------|
| OpenViking | Filesystem-like | 官方 GitHub README / 官方站点 | filesystem paradigm；`viking://`；L0/L1/L2；目录递归检索；retrieval trajectory；session self-iteration | README 给出相对 OpenClaw / LanceDB 的 completion 与 token 改善 | A | 是 | 量化为项目 README 官方口径，不做跨论文总排 |
| memsearch | Filesystem-like | 官方 GitHub README / 官方文档 | Markdown source of truth；Milvus shadow index；dense + BM25 + RRF；`search -> expand -> transcript` | 4 个 coding-agent 平台；3 层 recall；Milvus Lite 单文件 | A | 是 | coding agent 场景证据最清晰 |
| memU | Filesystem-like | 官方 GitHub README / 官方站点 | memory as file system；24/7 proactive agents；categories/items/resources/cross refs | one-click install `<3 min`；token 成本约 `~1/10` 为官方口径 | B | 是 | 方向鲜明，但量化主要来自官方自报 |
| Acontext | Filesystem-like | 官方 GitHub README / 官方 docs | skill memory layer；task learnings -> skill files；Markdown skill files；progressive disclosure | 后台学习延迟与默认 agent loops 有官方文档说明 | A | 是 | 对“技能即记忆”定义最清晰 |
| Voyager | Filesystem-like / Procedural | 原始论文 | executable code skill library；iterative prompting；long-horizon skill accumulation | 论文给出 `3.3x` 更多 unique items、`15.3x` 更快里程碑 | A | 是 | 程序性记忆的学术代表 |
| lossless-claw | Filesystem-like / Compaction | 官方 GitHub README | SQLite 持久化；DAG summary；`lcm_grep` / `lcm_describe` / `lcm_expand`；保留原始消息可恢复 | 无统一 benchmark，但机制可核验 | B | 是 | 解决上下文压缩与可恢复展开，不是通用 memory 平台 |
| Memoria | Filesystem-like / Governance | 官方 GitHub README / 官方站点 | Git for AI agent memory；snapshot/branch/merge/rollback；CoW；contradiction detection；quarantine；audit trail | 部署拓扑、版本语义、治理能力公开清晰 | A | 是 | 治理层代表 |
| mem0 | Vector/Graph-like | 官方 docs / 官方 repo / 原始论文 / 官方 research page | universal self-improving memory layer；extract/consolidate/retrieve；graph-enhanced path | 论文与官方 research page 都有 benchmark；新研究页口径更激进但展示层次不完全一致 | A | 是 | 强生态样本；最新 benchmark 需显式标注官方口径 |
| Honcho | Vector/Graph-like | 官方 GitHub README / 官方 docs / 官方 benchmark blog | entities/peers/sessions/representations；continual learning；entity state modeling | 官方 blog 自报 LongMem S 90.4、LoCoMo 89.9、BEAM 多档分数 | B | 是 | entity-aware memory 代表；benchmark 非论文主线 |
| Graphiti / Zep | Vector/Graph-like | 官方 GitHub README / 官方 docs / 原始论文 | temporal knowledge graph；dynamic graph；time+full-text+semantic+graph retrieval | 论文给出 DMR 与 LongMemEval 结果 | A | 是 | 时序关系 memory 的强代表 |
| eion | Vector/Graph-like | 官方 GitHub README / 官方站点 | shared memory storage；unified knowledge graph；PostgreSQL + pgvector + Neo4j；guest access | 架构参数和工具集公开，但无统一 benchmark | B | 是 | 多 agent + 权限模型表达清晰 |
| ContextLoom | Vector/Graph-like | 官方 GitHub README | shared brain；Redis-first；memory from compute decoupling；cold-start hydration；cycle hash | 官方宣称 sub-millisecond retrieval | B | 是 | shared context plane 方向明确，产品成熟度仍较早 |
| mem9 | Vector/Graph-like | 官方 GitHub README / 官方站点 | stateless plugin + central memory server；shared memory pool；TiDB hybrid retrieval；visual dashboard | 插件数量、memory tools、免费层规格公开 | B | 是 | coding-agent 协作与集中治理样本 |
| UltraContext | Adjacent context infrastructure | 官方 docs / 官方站点 | Context API；history/fork/clone/edit；CLI + MCP；same context everywhere | 无统一 memory benchmark | B | 否 | 重要邻接基础设施；更像 context plane 而非完整长期 memory 系统 |
| XiaoClaw | 生态包装层 | 官方站点 / 安装页 | 更像 OpenClaw 安装封装、API 产品层，不是独立 memory core | 无可靠官方 benchmark | X | 否 | 不进入主线技术结论 |

## 学术与方法论参照

| 系统 / 论文 | 角色 | 一手来源 | 吸收的合理结论 | 证据等级 | 备注 |
|-------------|------|----------|----------------|----------|------|
| CoALA | 认知架构参照 | 原始论文 | memory 应按模块化认知架构理解，而非单库外挂 | A | 用于定义问题空间 |
| MemGPT / Letta | 虚拟上下文管理参照 | 原始论文 / 官方 docs | memory tiers 与 context management 是核心视角 | A | 更偏调度与 OS-like framing |
| LoCoMo | 基准参照 | 原始论文 / 项目页 | 长对话、多跳、时间、人物关系 benchmark | A | 不等于通用工程 memory 评测 |
| LongMemEval | 基准参照 | 原始论文 | 信息抽取、多 session、时间、知识更新、abstention 很关键 | A | 对“长期 chat memory”定义更细 |
| BEAM | 新一代基准参照 | 原始论文 | 百万 token 长时记忆评测开始成为 frontier | A | 更多用于判断评测趋势 |
| TiMem | 时间层次化参照 | 原始论文 | 时间树式 consolidation 与 complexity-aware recall 值得借鉴 | A | 学术路线强，但产业化尚早 |
| LiCoMemory | 轻量图参照 | 原始论文 | 图更适合作为导航与候选缩减层，而非总是重型 KG | A | 用于支持轻量结构化索引判断 |
| MIRIX | 多类型编排参照 | 原始论文 | memory types orchestration 与 active retrieval 很重要 | A | 用于支持“memory orchestration”观点 |

## 证据使用原则

### 可以作为强支撑的结论

- Filesystem-like 路线强调可读、可编辑、渐进式披露、程序性沉淀与治理能力
- Vector/graph-like 路线强调 northbound memory plane、共享状态、实体关系和时序演化
- `CortexMem` 适合做混合架构，而不是单路线押注
- `lossless-claw` 已可作为 append-only + layered summaries 的工程样本

### 不能作为强支撑的结论

- 把所有公开 benchmark 混成单一“总冠军榜”
- 用官方 blog / research page 数字替代同行评审 benchmark
- 把 `UltraContext` 当成已经成熟的长期 memory layer
- 把 `XiaoClaw` 当成独立 memory core

## 本轮最关键的证据判断

1. `memsearch`、`Acontext`、`Memoria`、`lossless-claw` 共同说明 filesystem-like 路线不是“没有检索能力”，而是把检索放在真相层之下。
2. `mem0`、`Honcho`、`Graphiti`、`eion`、`mem9`、`ContextLoom` 共同说明 northbound memory plane 已经从“向量库外挂”推进到“共享状态 / 实体表示 / 时序图 / 后台 consolidation”。
3. `UltraContext` 很有价值，但更适合作为 context plane / context engineering 邻接基础设施，而不是直接作为成熟 memory 主线代表。
4. `XiaoClaw` 仍应保留在生态包装层，不应被误读为独立 memory architecture。
