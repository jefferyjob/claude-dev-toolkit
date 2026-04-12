# Flowprinter

使用 Mermaid 文本语法生成流程图、时序图、状态图、类图、ER 图、甘特图等技术图表的 Claude Code 插件。

## 概述

Flowprinter 面向开发者的日常技术表达场景，适合在需求讨论、接口设计、架构说明、故障排查和技术文档编写时快速生成结构化图表。

这个插件当前提供一个 Mermaid 图表生成 skill，重点不是生成“设计感海报”，而是生成**可读、可维护、可嵌入文档**的工程图。

## 能力范围

Flowprinter 适合生成以下类型的技术图表：

- Flowchart / 流程图
- Sequence Diagram / 时序图
- State Diagram / 状态图
- Class Diagram / 类图
- ER Diagram / 实体关系图
- Gantt / 甘特图
- Journey / 用户旅程图
- Mindmap / 思维导图
- Kanban / 看板图
- XY Chart / 简单趋势图

## 适用场景

- 业务流程梳理
- API 调用链说明
- 服务交互时序图
- 状态流转建模
- 数据模型关系表达
- 研发计划与排期可视化
- 在 Markdown 文档中内嵌 Mermaid 图表

## 使用方式

安装插件后，可直接在 Claude Code 中请求生成 Mermaid 图表。

### 示例

```text
请用 flowprinter 画一个用户登录流程图
```

```text
请把下面的服务调用过程整理成 Mermaid 时序图
```

```text
用 Mermaid 类图表达当前订单模块的核心对象关系
```

如果使用 slash command，也可以直接围绕该 skill 的能力描述任务，例如：

```text
/flowprinter 为支付回调流程生成一个 Mermaid 流程图
```
