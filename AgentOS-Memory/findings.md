# Agent Memory System 研究发现

## C.A.P.E 对比框架

### 1. 架构与底层范式层 (Architecture & Paradigm)
| 维度 | 说明 |
|------|------|
| 技术分类 | RAG外挂检索 / OS内存页置换 / Transformer注意力修改(模型原生) |
| 存储范式 | 扁平向量(Flat Vector) / 会话时序(Time-Series) / 图数据库(GraphDB) / 文件目录树(File System) |
| 系统定位 | 中间件插件 / Memory-as-a-Service / 内置于大模型底座 |
| 记忆粒度 | 事实级 / 文档级 / 会话级 / 技能级 |
| 检索机制 | 向量相似度 / 关键词BM25 / 混合检索 / 目录浏览 / 图遍历 |

### 2. 认知与演进能力层 (Cognition & Evolution)
| 维度 | 说明 |
|------|------|
| 自我进化 | 死记忆(只存不更新) / 活记忆(反思+融合+淘汰) |
| 反思机制 | 无 / 事后总结 / 后台异步反思 / 主动反思触发 |
| 记忆融合 | 无 / 去重合并 / 语义融合 / 知识图谱推理融合 |
| 遗忘机制 | 无 / TTL过期 / 重要性评分淘汰 / LRU |
| 结构化推理 | 扁平 / 分类标签 / 实体关系图 / 超图 |

### 3. 工程与生产力层 (Production & Engineering)
| 维度 | 说明 |
|------|------|
| Token效率 | 无优化 / 简单截断 / 分层加载 / 智能压缩 / 渐进披露 |
| 可观测性 | 黑箱 / 日志 / 可视化面板 / 人类可读文件 |
| 可读可写 | 二进制 / JSON/结构化 / Markdown人类可读 |
| 部署复杂度 | 零配置 / 单二进制 / Docker / 多组件依赖 |
| 集成方式 | SDK / MCP / 插件 / API |

### 4. 业务与生态层 (Business & Ecosystem)
| 维度 | 说明 |
|------|------|
| 适用场景 | C端闲聊 / B端运维 / 编码Agent / 多Agent仿真 |
| 多Agent支持 | 单Agent / 多Agent隔离 / 共享记忆 / 协作记忆 |
| 开源许可 | MIT / Apache / AGPL / 闭源 |
| 社区活跃度 | Stars / Contributors / Recent commits |

---

## 系统研究发现

（待填充）
