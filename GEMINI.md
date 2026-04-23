# claude-books 项目概览

## 📁 目录概览

本项目是一个非代码类的知识与文献仓库，主要包含了关于 AI Agent 架构、记忆系统研究报告、加密货币发展史，以及中国古典文学等多个领域的深度研究与书籍汇编。这些材料似乎是为了给大语言模型（如 Claude 或 Gemini）提供丰富的上下文、长文本处理测试素材或特定领域知识体系而构建的。

## 📂 核心目录与文件说明

### 1. `AgentHarness/` (Agent 控制平面与运行时研究)
*   **用途**：探讨和记录生产级 AI Agent 的基础架构构建，涵盖编程语言、编译器和运行时。
*   **关键文件**：
    *   `AgentHarness,Building-Production-Grade-AI-Agents-Deterministic-Foundation.md`：详细论述 Agent Harness 的核心设计与决定性基础架构的深度长文。
    *   `research-findings.md`：关于《Agent Harness：编程语言、编译器与运行时》的调研成果汇总，分析了学术定义、工程学定义以及多层架构设计。

### 2. `AgentOS-Memory/` (Agent 记忆系统洞察)
*   **用途**：针对产业界各种 Agent Memory System（代理记忆系统）的深度研究与对比分析报告。
*   **关键文件**：
    *   `AGENTS.md` / `agent_memory_system_insight_report.md` 等：采用 C.A.P.E 框架（架构、认知、工程、业务）对各类记忆系统（如 OpenViking, memsearch, Letta/memGPT, mem0 等）进行了详尽的技术路线拆解与优劣势评估。
    *   `fs-vector-graph/`：包含进一步的专项研究报告（V1 至 V9）和证据矩阵分析。

### 3. `CryptoSaga/` (《币圈风云录》)
*   **用途**：一部约 70 万字的演义体裁著作，记录了加密货币从诞生到万亿帝国的完整历史。
*   **关键文件**：
    *   `README.md`：本书的介绍，包含核心主题、四大篇章（起源、崛起、崩盘、复兴）及章节大纲。
    *   `chapters/`、`chapters_en/`、`chapters_revised/`：涵盖了从“密码学的曙光”到“未来的风云”的完整章节，包括中英文多语种版本及校订版。

### 4. `DreamOfTheRedChamber/` (《红楼梦》文献资料)
*   **用途**：中国古典文学巨著《红楼梦》的相关电子文本和特殊版本。
*   **关键文件**：
    *   `脂砚斋重评石头记_final.md`：包含大量批注的脂本《石头记》汇总。
    *   `chapters/`：按章节拆分的文本文件集合（共120回），可能用于大模型的长文本阅读分析与检索测试。
    *   `hlm.mobi`：电子书文件格式。

### 5. `vendor/` (第三方与引入资源)
*   **用途**：引入的其他开源仓库或知识集锦。
*   **包含内容**：如 `agency-agents-zh`（不同行业 Agent 的应用与设计），以及各类信息安全 (`infosec-books`) 和 IT 技术 (`itBooks`) 相关的书籍合集。

## 🚀 使用指南

由于此仓库为非代码项目，它的主要应用场景为：

1.  **大语言模型上下文输入**：作为长上下文阅读、内容摘要、信息检索（RAG 测试）的高质量素材库。
2.  **专业知识库查询**：当你需要了解生产级 Agent 架构设计（Harness & Memory）或加密货币历史脉络时，可直接查阅 `AgentHarness` 和 `AgentOS-Memory` 或 `CryptoSaga` 内的研究报告及章节内容。
3.  **开发与调研参考**：通过阅读 `.md` 文档和报告中的案例分析，为设计具备自我进化能力和层次化长期记忆的 AI Agent 操作系统提供理论支撑与竞品参考。

*(提示：当前内容作为 Gemini CLI 的内置指南指令。你随时可以通过检索具体子目录中的文件来获取更深度的知识细节。)*
