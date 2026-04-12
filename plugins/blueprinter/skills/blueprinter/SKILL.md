---
name: blueprinter
description: 使用 HTML/CSS 生成分层彩色架构图。适用于架构图、系统图、流程图或需要“语义分层 + 色带分区 + 工程化排版”的技术说明图。用户提到蓝图风、扁平技术图、架构可视化、技术图纸时触发。
---

# Blueprinter

使用 HTML/CSS 按照“扁平化工程蓝图”风格指南生成技术图表。

## 核心理念

精确、分层、分区、可扫读。输出应像一张经过工程化约束的信息图：有明确的层级、区域归属、模块分组和阅读路径，而不是单纯的白底规格书，也不是营销落地页。

## 视觉规则

### 1. 保持扁平，但允许柔和色块
- 不要使用投影
- 不要使用渐变
- 不要使用玻璃拟态 / 模糊效果
- 可以使用**柔和的语义底色**表达层级、域、区块
- 可以使用**中等圆角**（如 12px ~ 20px）用于 `band / group / node / flow-section` 容器

### 2. 先分区，再放模块
- 先搭建整张图的**纵向分层结构**，再往每层中放 `group / node`
- 每个大层（`band`）都应有独立标题、说明和背景色
- 每层内部优先使用“区域容器 > 分组容器 > 节点卡片”的三级结构
- 不要把整张图退化成一排排白色描边盒子

### 3. 颜色按语义层复用

| 层级/用途 | 推荐颜色 |
|-----------|----------|
| 页面背景 | 极浅暖灰或冷灰（如 `#f5f7fb`） |
| 主链路 / 阅读流 | 独立浅紫 Flow 区（如 `#f3f0ff`，不要并入某个 band） |
| 总览层 / 入口层 | Aqua / Teal（如 `#dff7f5`） |
| 接入 / 协议层 | Peach / Orange（如 `#ffe7cf`） |
| 业务 / 服务层 | Mint / Green（如 `#def4df`） |
| 能力 / 编排层 | Lavender（如 `#efe3ff`） |
| 数据 / 平台层 | Sky / Indigo（如 `#dce8ff` / `#d9ddff`） |
| 主文字 | 深色高对比（如 `#1f2937`） |
| 次文字 | 中性灰（如 `#667085`） |
| 边框 | 比底色略深的柔和描边 |

规则：
- 颜色必须**按层复用**，同一层内颜色体系一致
- 颜色用于表达结构，不是随机装饰
- 节点卡片通常使用白色或浅色半透明底，放在对应 `band / group` 内
- `flow-section` 是**独立语义区域**，用于承载主链路、推荐阅读顺序或跨层调用路径
- 强调色只用于关键路径、告警、重点说明；不要把每个节点都做成强调态

### 4. 排版层级
- 主标题：无衬线字体，醒目但克制
- 层标题 / 分组标题：无衬线字体，强调层级关系
- 节点标题：无衬线字体，易扫读
- 技术注记 / 路径 / 协议 / 版本号：等宽字体
- **等宽字体只用于技术微文案，不要成为主视觉字体**

### 5. 布局结构
- 整张图必须包裹在 `diagram-canvas` 中
- 页面头部应包含：`diagram-kicker`、标题区、说明文案、`meta-row`
- 主体采用**纵向堆叠的多个 `band-section`**
- 每个 `band-section` 内可再分为若干 `band-group`
- 每个 `band-group` 内放 `node-card`
- 如果图中存在明确的主调用链、推荐阅读顺序或跨层主链路，必须在 header 下方、`band-stack` 上方放一个独立的 `flow-section`
- `flow-section` 不属于任何单独业务层，**不要**把它塞进某个 `band-section` 的底部
- 阅读顺序应清晰：通常为**从上到下、从左到右**

### 6. 元素规范
- **Band（大层）**：大面积柔和底色，承担语义分层
- **Group（分组）**：放在 band 中，负责表达子系统 / 子域 / 子流程
- **Node（节点）**：具体模块、服务、角色、接口、存储、能力点
- **Flow Section（主链路区）**：独立展示调用主线、阅读主线、跨层传递顺序
- **Flow Chip（链路胶囊）**：承载简洁链路片段，如 `Client → Gateway`
- **Legend / Meta**：用于说明图例、环境、协议、版本等

### 7. 图形语言
- 更像“架构地图 / 分层看板”，而不是“黑白工程线框图”
- 允许使用：
  - 色带
  - 圆角面板
  - 标签胶囊
  - 层内分组
  - 简洁箭头或流向提示
- 避免使用：
  - 大量纯黑硬描边白盒
  - 过多装饰图标
  - 复杂插画式图形

## CSS 变量参考

```css
:root {
  --c-page: #f5f7fb;
  --c-canvas: #ffffff;
  --c-text-main: #1f2937;
  --c-text-sub: #667085;
  --c-line: #b8c2d1;
  --c-node-border: #cfd7e6;

  --c-band-aqua: #dff7f5;
  --c-band-peach: #ffe7cf;
  --c-band-mint: #def4df;
  --c-band-lavender: #efe3ff;
  --c-band-sky: #dce8ff;
  --c-band-indigo: #d9ddff;
  --c-flow-surface: #f3f0ff;

  --c-group-surface: rgba(255, 255, 255, 0.58);
  --c-node-surface: rgba(255, 255, 255, 0.90);
  --c-strong: #344054;
  --c-highlight: #7c3aed;

  --radius-band: 20px;
  --radius-group: 16px;
  --radius-node: 14px;

  --font-ui: 'Inter', 'Helvetica Neue', sans-serif;
  --font-mono: 'JetBrains Mono', 'Consolas', monospace;
}
```

## HTML 结构模板

直接以 `references/template.html` 为准。

使用要求：
- 保留 `diagram-container > diagram-canvas > header + flow-section + main.band-stack` 的整体结构
- 如果当前图没有明确主链路，可以删掉 `flow-section` 的内容；但只要存在推荐阅读顺序或调用主线，就应保留这个独立区域
- 不要把 `flow-row` 挂在某个 `band-section` 里面替代 `flow-section`
- 新增层时优先复用既有语义色；只有当现有层级语义无法覆盖时，才引入新色

## 示例：分层系统图

直接以 `references/example.html` 为准。

阅读要点：
- `flow-section` 位于 header 与 band-stack 之间，是整张图的独立主链路说明区
- 示例中的主链路使用浅紫色区块，表示“跨层阅读流”，而不是某个业务域本身
- 入口层、接入层、业务与能力层分别使用 aqua、peach、mint 三组语义底色
- 节点卡片维持白色高可读表面，语义主要由 band/group 的层色承载

## 使用指南

1. **先定层，再铺内容**：先想清楚大层（band），再细化 group 和 node。
2. **主链路单独成区**：只要有推荐阅读顺序、调用主线、跨层路径，就使用独立 `flow-section`，不要内嵌到业务层底部。
3. **颜色按层复用**：同一层使用同一组色彩语义，不要随机给每个模块单独配色。
4. **优先区域化表达**：先让人一眼看懂“哪一块是什么域”，再看具体节点。
5. **标题层级要清楚**：主标题、层标题、组标题、节点标题必须一眼区分。
6. **等宽字体只做注记**：协议、路径、Topic、RPC、版本、环境等可以用 `--font-mono`。
7. **连线适可而止**：优先通过空间位置和分层表达关系，必要时再补 flow / connector。
8. **避免回退成规格书风格**：不要整图只剩白底描边框；要保留分层色带和区域分组的整体观感。
9. **模板与示例优先级最高**：结构和细节以 `references/template.html` 与 `references/example.html` 为准，文档规则用于解释这些结构背后的意图。
