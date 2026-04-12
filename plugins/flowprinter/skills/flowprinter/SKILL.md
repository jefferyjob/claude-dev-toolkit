---
name: mermaid
description: 使用简洁的文本语法创建流程图、时序图、状态机图、类图、甘特图和思维导图。适合展示流程、API 交互和技术文档。不适合数据驱动图表（请使用 vega）、快速 KPI 可视化（请使用 infographic）或分层系统架构图（请使用 architecture）。
---

# Mermaid 图表可视化

**快速开始：** 先确定图表类型（flowchart/sequence/state/class/ER/gantt/mindmap）→ 定义带形状的节点 → 使用箭头连接 → 包裹在 ` ```mermaid ` 代码块中。默认方向为从上到下（`TD`），优先使用 `flowchart` 而不是 `graph`，支持 Unicode。

---

## 关键语法规则

### 规则 1：列表语法冲突
```
❌ [1. Item]     → 不支持的 Markdown：列表
✅ [1.Item]      → 去掉句点后的空格
✅ [① Item]      → 使用带圈数字 ①②③④⑤⑥⑦⑧⑨⑩
✅ [(1) Item]    → 使用括号
```

### 规则 2：子图命名
```
❌ subgraph AI Agent Core    → 含空格但未加引号
✅ subgraph agent["AI Agent Core"]  → 使用 ID 和显示名称
✅ subgraph agent            → 仅使用简单 ID
```

### 规则 3：子图中的节点引用
```
❌ Title --> AI Agent Core   → 引用显示名称
✅ Title --> agent           → 引用子图 ID
```

### 规则 4：节点文本中的特殊字符
```
✅ ["Text with spaces"]       → 含空格时使用引号
✅ 用 #quot; 代替 "            → 避免直接使用双引号
✅ 用 #lpar;#rpar; 表示 ()    → 避免直接使用括号
```

### 规则 5：优先使用 flowchart 而不是 graph
```
❌ graph TD      → 旧写法
✅ flowchart TD  → 支持子图方向和更多特性
```

---

## 常见问题

| 问题 | 解决方案 |
|------|----------|
| 图表无法渲染 | 检查括号或引号是否未配对 |
| 列表语法错误 | 使用 `[1.Item]`，不要写成 `[1. Item]` |
| 子图引用失败 | 使用 ID，不要使用显示名称 |
| 内容过于拥挤 | 拆分成多个图表 |
| 连线交叉过多 | 更换布局方向，或使用不可见边 `~~~` |

---

## 输出格式

````markdown
```mermaid
[diagram code]
```
````

---

## 相关文件

> 如需查看特定图表类型的详细语法和高级特性，请参考下面的引用文件：

- [syntax.md](references/syntax.md) — 覆盖 14+ 图表类型的详细语法：流程图形状、时序图参与者、类关系、状态迁移、ER 基数、甘特任务等
