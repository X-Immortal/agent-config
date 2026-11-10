---
name: gense-workflow
description: 以生成式软件工程（GenSE）方式开展新项目、重大功能、跨模块变更、需求与架构设计或全流程工程开发。涵盖从意图澄清、SRS、系统架构与适度详细设计，到功能切片实现、多子代理 worktree 并行协作与工程级 Git 交付。简单局部修改无需调用。
---

# GenSE 工程开发工作流（核心摘要与导航）

软件开发是持续对齐 **Intent（意图） → Spec（规格） → Implementation（实现） ↔ Feedback（反馈）** 的过程：**人负责定义目标、决定关键取舍与裁决最终体验；Agent 负责调研现状、提供有依据的完整流转方案、在授权边界内增量实现、分层验证并报告客观证据。**

## 1. 任务分级与路径选择

| 任务类型 | 默认推进路径 |
| :--- | :--- |
| **新项目 / 重大方向演化** | 意图澄清 → 形成 `docs/srs.md` 与 `docs/architecture.md` → 搭最小公共底座 → 按端到端功能切片推进与验证 |
| **新功能 / 跨模块变更** | 阅读相关 SRS、架构与代码 → 增量更新受影响的规格与关键设计 → 实施变更与集中验证 |
| **探索性原型 / UI 交互打磨** | 根据体验方向是否明确选择轻量原型或直接调整 → 尽早验证交互 → 按需同步后端契约、数据模型与规格 |
| **重构 / 结构治理** | 明确需保持的外部行为与结构目标 → 建立验证基准 → 调整实现并验证行为一致 |

上述路径用于组织工作，不是逐阶段强制审批流程。结合用户授权、已有决策与变更影响设置确认点：完整实施任务中方向明确的工作可连续推进；实质性歧义、尚未授权的重大取舍、范围扩展或不可逆操作先确认。仅要求方案或单一阶段产出时，完成该范围后停止；用户明确指定的评审点仍须遵守。

## 2. 核心原则摘要

- **适度规格化与单一权威来源**：`docs/srs.md` 管业务行为与内嵌验收条件；`docs/architecture.md` 管选型、模块边界、数据所有权与核心一致性机制；实际 Schema 脚本管完整数据库结构；代码及导出的 `openapi.yaml` 管具体接口定义。
- **契约变更自上而下同步**：实施或验证暴露规格缺口或设计过度时，先明确问题与最小调整方案，再同步受影响的规格、设计与实现；是否需要确认按上述授权与影响判断，已有决策范围内的细化可直接推进。
- **通用方法与项目事实分离**：Skill 保存可迁移的判断方法与适用条件；具体表名、业务参数、分支处置与项目复盘保留在项目资料中，不作为其他项目的默认方案。
- **交付汇报四要素**：简明说明 **做了什么（修改范围与提交状态）**、**为什么这样做（仅关键取舍）**、**怎样验证（实际命令、场景与未覆盖项）**、**还有什么（遗留问题与下一步）**。

## 3. 按需加载阶段细则（References）

根据当前所处的具体工程环节，仅读取下方对应的参考文件：

| 当前工作环节 | 读取文件 |
| :--- | :--- |
| **意图澄清、待决问题闭环与 SRS 编写** | [references/01-requirements-and-srs.md](references/01-requirements-and-srs.md) |
| **总体架构、模块边界、数据建模与事务并发设计** | [references/02-architecture-and-data-design.md](references/02-architecture-and-data-design.md) |
| **最小底座、端到端功能切片实现与分层验证诊断** | [references/03-implementation-and-verification.md](references/03-implementation-and-verification.md) |
| **完整工程级 Git 流、多子代理 worktree 并行与打包交付** | [references/04-project-git-and-parallel-agents.md](references/04-project-git-and-parallel-agents.md) |
| **项目文档目录组织、单一权威边界与图表风格** | [references/05-project-documentation.md](references/05-project-documentation.md) |
