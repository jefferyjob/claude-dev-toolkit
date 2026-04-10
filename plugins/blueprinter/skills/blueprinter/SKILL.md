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
- 可以使用**中等圆角**（如 12px ~ 20px）用于 band / group / node 容器

### 2. 先分区，再放模块
- 先搭建整张图的**纵向分层结构**，再往每层中放 group / node
- 每个大层（band）都应有独立标题、说明和背景色
- 每层内部优先使用“区域容器 > 分组容器 > 节点卡片”的三级结构
- 不要把整张图退化成一排排白色描边盒子

### 3. 颜色按语义层复用

| 层级/用途 | 推荐颜色 |
|-----------|----------|
| 页面背景 | 极浅暖灰或冷灰（如 `#f5f7fb`） |
| 总览层 / 入口层 | Aqua / Teal（如 `#dff7f5`） |
| 接入 / 协议层 | Peach / Orange（如 `#ffe7cf`） |
| 业务 / 服务层 | Mint / Green（如 `#def4df`） |
| 能力 / 编排层 | Lavender / Pink（如 `#efe3ff`） |
| 数据 / 平台层 | Sky / Indigo（如 `#dce8ff` / `#d9ddff`） |
| 主文字 | 深色高对比（如 `#1f2937`） |
| 次文字 | 中性灰（如 `#667085`） |
| 边框 | 比底色略深的柔和描边 |

规则：
- 颜色必须**按层复用**，同一层内颜色体系一致
- 颜色用于表达结构，不是随机装饰
- 节点卡片通常使用白色或浅色半透明底，放在对应 band/group 内
- 强调色只用于关键路径、告警、重点说明

### 4. 排版层级
- 主标题：无衬线字体，醒目但克制
- 层标题 / 分组标题：无衬线字体，强调层级关系
- 节点标题：无衬线字体，易扫读
- 技术注记 / 路径 / 协议 / 版本号：等宽字体
- **等宽字体只用于技术微文案，不要成为主视觉字体**

### 5. 布局结构
- 整张图必须包裹在 `diagram-canvas` 中
- 页面头部应包含：标题、说明、副标题/元信息
- 主体采用**纵向堆叠的多个 `band-section`**
- 每个 `band-section` 内可再分为若干 `band-group`
- 每个 `band-group` 内放 `node-card`
- 阅读顺序应清晰：通常为**从上到下、从左到右**

### 6. 元素规范
- **Band（大层）**：大面积柔和底色，承担语义分层
- **Group（分组）**：放在 band 中，负责表达子系统 / 子域 / 子流程
- **Node（节点）**：具体模块、服务、角色、接口、存储、能力点
- **Connector（连接）**：用于表达依赖、调用、流向；可用细线、箭头、虚线
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

  --c-group-surface: rgba(255, 255, 255, 0.58);
  --c-node-surface: rgba(255, 255, 255, 0.88);
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

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[图示标题]</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
  <style>
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
      --c-group-surface: rgba(255, 255, 255, 0.58);
      --c-node-surface: rgba(255, 255, 255, 0.9);
      --c-strong: #344054;
      --c-highlight: #7c3aed;
      --radius-band: 20px;
      --radius-group: 16px;
      --radius-node: 14px;
      --font-ui: 'Inter', 'Helvetica Neue', sans-serif;
      --font-mono: 'JetBrains Mono', 'Consolas', monospace;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: var(--font-ui);
      background: var(--c-page);
      color: var(--c-text-main);
      padding: 32px;
    }

    .diagram-container {
      max-width: 1480px;
      margin: 0 auto;
    }

    .diagram-canvas {
      background: var(--c-canvas);
      border: 1px solid #dde3ec;
      border-radius: 28px;
      padding: 28px;
    }

    .diagram-header {
      margin-bottom: 24px;
      display: grid;
      gap: 12px;
    }

    .diagram-kicker {
      font-family: var(--font-mono);
      font-size: 11px;
      color: var(--c-text-sub);
      letter-spacing: 0.08em;
      text-transform: uppercase;
    }

    .diagram-title-row {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      gap: 16px;
      flex-wrap: wrap;
    }

    .diagram-title {
      font-size: 28px;
      font-weight: 700;
      line-height: 1.15;
    }

    .diagram-subtitle {
      max-width: 760px;
      color: var(--c-text-sub);
      line-height: 1.6;
      font-size: 14px;
    }

    .meta-row {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
    }

    .meta-pill {
      border: 1px solid var(--c-node-border);
      background: #fff;
      border-radius: 999px;
      padding: 6px 10px;
      font-size: 11px;
      color: var(--c-text-sub);
      font-family: var(--font-mono);
    }

    .band-stack {
      display: grid;
      gap: 18px;
    }

    .band-section {
      border-radius: var(--radius-band);
      padding: 20px;
      display: grid;
      gap: 16px;
      border: 1px solid rgba(52, 64, 84, 0.08);
    }

    .band-section.aqua { background: var(--c-band-aqua); }
    .band-section.peach { background: var(--c-band-peach); }
    .band-section.mint { background: var(--c-band-mint); }
    .band-section.lavender { background: var(--c-band-lavender); }
    .band-section.sky { background: var(--c-band-sky); }
    .band-section.indigo { background: var(--c-band-indigo); }

    .band-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      gap: 16px;
      flex-wrap: wrap;
    }

    .band-title {
      font-size: 18px;
      font-weight: 700;
      line-height: 1.2;
    }

    .band-desc {
      margin-top: 6px;
      color: var(--c-text-sub);
      font-size: 13px;
      line-height: 1.6;
      max-width: 760px;
    }

    .band-tag {
      font-family: var(--font-mono);
      font-size: 11px;
      padding: 6px 10px;
      border-radius: 999px;
      background: rgba(255, 255, 255, 0.72);
      color: var(--c-strong);
      border: 1px solid rgba(52, 64, 84, 0.1);
    }

    .band-grid {
      display: grid;
      grid-template-columns: repeat(12, minmax(0, 1fr));
      gap: 14px;
    }

    .band-group {
      grid-column: span 4;
      background: var(--c-group-surface);
      border: 1px solid rgba(255, 255, 255, 0.55);
      border-radius: var(--radius-group);
      padding: 16px;
      display: grid;
      gap: 12px;
      backdrop-filter: none;
    }

    .group-title {
      font-size: 14px;
      font-weight: 700;
    }

    .group-note {
      font-size: 12px;
      color: var(--c-text-sub);
      line-height: 1.5;
    }

    .node-list {
      display: grid;
      gap: 10px;
    }

    .node-card {
      background: var(--c-node-surface);
      border: 1px solid var(--c-node-border);
      border-radius: var(--radius-node);
      padding: 12px 14px;
      display: grid;
      gap: 6px;
    }

    .node-kicker {
      font-family: var(--font-mono);
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.06em;
      color: var(--c-text-sub);
    }

    .node-title {
      font-size: 14px;
      font-weight: 700;
      line-height: 1.35;
    }

    .node-meta {
      font-size: 12px;
      line-height: 1.6;
      color: var(--c-text-sub);
    }

    .flow-row {
      display: flex;
      align-items: center;
      flex-wrap: wrap;
      gap: 8px;
      color: var(--c-strong);
      font-size: 12px;
      font-family: var(--font-mono);
    }

    .flow-chip {
      padding: 6px 10px;
      border-radius: 999px;
      border: 1px dashed rgba(52, 64, 84, 0.24);
      background: rgba(255, 255, 255, 0.65);
    }

    .legend-row {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 8px;
    }

    .legend-item {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      font-size: 12px;
      color: var(--c-text-sub);
    }

    .legend-swatch {
      width: 14px;
      height: 14px;
      border-radius: 999px;
      border: 1px solid rgba(52, 64, 84, 0.14);
    }

    @media (max-width: 1100px) {
      .band-group {
        grid-column: span 6;
      }
    }

    @media (max-width: 720px) {
      body {
        padding: 16px;
      }

      .diagram-canvas {
        border-radius: 20px;
        padding: 18px;
      }

      .band-group {
        grid-column: span 12;
      }
    }
  </style>
</head>
<body>
  <div class="diagram-container">
    <div class="diagram-canvas">
      <header class="diagram-header">
        <div class="diagram-kicker">[图示类型 / LANGUAGE / VERSION]</div>
        <div class="diagram-title-row">
          <div>
            <h1 class="diagram-title">[图示标题]</h1>
            <p class="diagram-subtitle">[一句话说明系统目的、范围、阅读方式]</p>
          </div>
          <div class="meta-row">
            <span class="meta-pill">[协议/技术栈]</span>
            <span class="meta-pill">[环境]</span>
            <span class="meta-pill">[更新时间]</span>
          </div>
        </div>
      </header>

      <main class="band-stack">
        <section class="band-section aqua">
          <div class="band-header">
            <div>
              <div class="band-title">[顶层概览 / 入口层]</div>
              <div class="band-desc">[说明这一层承载什么角色、入口、用户端或上游来源]</div>
            </div>
            <div class="band-tag">[Overview]</div>
          </div>

          <div class="band-grid">
            <div class="band-group">
              <div class="group-title">[用户角色 / 调用方]</div>
              <div class="group-note">[这组模块的职责说明]</div>
              <div class="node-list">
                <article class="node-card">
                  <div class="node-kicker">Role</div>
                  <div class="node-title">[Web / App / Admin / Upstream API]</div>
                  <div class="node-meta">[补充说明]</div>
                </article>
              </div>
            </div>
          </div>
        </section>

        <section class="band-section peach">
          <div class="band-header">
            <div>
              <div class="band-title">[接入层 / 协议层]</div>
              <div class="band-desc">[说明网关、协议、认证、中间件或入口控制]</div>
            </div>
            <div class="band-tag">[Access]</div>
          </div>
          <div class="band-grid">
            <div class="band-group">...</div>
            <div class="band-group">...</div>
            <div class="band-group">...</div>
          </div>
        </section>

        <section class="band-section mint">
          <div class="band-header">
            <div>
              <div class="band-title">[业务层 / 服务层]</div>
              <div class="band-desc">[说明核心域服务、逻辑模块、业务闭环]</div>
            </div>
            <div class="band-tag">[Domain]</div>
          </div>
          <div class="band-grid">
            <div class="band-group">...</div>
            <div class="band-group">...</div>
            <div class="band-group">...</div>
          </div>
          <div class="flow-row">
            <span class="flow-chip">[Client → Gateway]</span>
            <span class="flow-chip">[Gateway → Service]</span>
            <span class="flow-chip">[Service → Data / Capability]</span>
          </div>
        </section>
      </main>
    </div>
  </div>
</body>
</html>
```

## 使用指南

1. **先定层，再铺内容**：先想清楚大层（band），再细化 group 和 node。
2. **颜色按层复用**：同一层使用同一组色彩语义，不要随机给每个模块单独配色。
3. **优先区域化表达**：先让人一眼看懂“哪一块是什么域”，再看具体节点。
4. **标题层级要清楚**：主标题、层标题、组标题、节点标题必须一眼区分。
5. **等宽字体只做注记**：协议、路径、Topic、RPC、版本、环境等可以用 `--font-mono`。
6. **连线适可而止**：优先通过空间位置和分层表达关系，必要时再补 flow / connector。
7. **避免回退成规格书风格**：不要整图只剩白底描边框；要保留分层色带和区域分组的整体观感。

## 示例：分层系统图

```html
<div class="diagram-canvas">
  <header class="diagram-header">
    <div class="diagram-kicker">SYSTEM MAP / V1.0 / CN</div>
    <div class="diagram-title-row">
      <div>
        <h1 class="diagram-title">在线学习平台架构图</h1>
        <p class="diagram-subtitle">从用户入口到业务编排、能力服务与数据底座的分层视图。</p>
      </div>
      <div class="meta-row">
        <span class="meta-pill">Go + gRPC</span>
        <span class="meta-pill">Production</span>
        <span class="meta-pill">2026-04</span>
      </div>
    </div>
  </header>

  <main class="band-stack">
    <section class="band-section aqua">
      <div class="band-header">
        <div>
          <div class="band-title">入口与角色</div>
          <div class="band-desc">统一展示学习端、教师端、运营端与上游调用来源。</div>
        </div>
        <div class="band-tag">Overview</div>
      </div>
      <div class="band-grid">
        <div class="band-group">
          <div class="group-title">用户入口</div>
          <div class="node-list">
            <article class="node-card">
              <div class="node-kicker">Client</div>
              <div class="node-title">Student App / Teacher Console</div>
              <div class="node-meta">课堂、作业、讲评、互动统一接入</div>
            </article>
          </div>
        </div>
        <div class="band-group">
          <div class="group-title">外部调用</div>
          <div class="node-list">
            <article class="node-card">
              <div class="node-kicker">Upstream</div>
              <div class="node-title">API Gateway / Internal Services</div>
              <div class="node-meta">统一通过 RPC 或 HTTP 进入系统</div>
            </article>
          </div>
        </div>
      </div>
    </section>

    <section class="band-section peach">
      <div class="band-header">
        <div>
          <div class="band-title">接入与编排</div>
          <div class="band-desc">负责鉴权、路由、中间件与请求编排。</div>
        </div>
        <div class="band-tag">Access</div>
      </div>
      <div class="band-grid">
        <div class="band-group">
          <div class="group-title">网关能力</div>
          <div class="node-list">
            <article class="node-card">
              <div class="node-kicker">Gateway</div>
              <div class="node-title">REST / gRPC Router</div>
              <div class="node-meta">认证、限流、参数处理、日志</div>
            </article>
          </div>
        </div>
        <div class="band-group">
          <div class="group-title">流程编排</div>
          <div class="node-list">
            <article class="node-card">
              <div class="node-kicker">Logic</div>
              <div class="node-title">课堂流程 / 学习流程 / 任务流</div>
              <div class="node-meta">承接业务入口并路由至域服务</div>
            </article>
          </div>
        </div>
      </div>
    </section>

    <section class="band-section mint">
      <div class="band-header">
        <div>
          <div class="band-title">业务与能力层</div>
          <div class="band-desc">核心课程服务、LLM 能力、通知与数据处理等模块在此协同。</div>
        </div>
        <div class="band-tag">Domain</div>
      </div>
      <div class="band-grid">
        <div class="band-group">
          <div class="group-title">课程服务</div>
          <div class="node-list">
            <article class="node-card">
              <div class="node-kicker">Service</div>
              <div class="node-title">写作 / 文化史 / 课堂互动</div>
              <div class="node-meta">围绕学习场景组织核心业务闭环</div>
            </article>
          </div>
        </div>
        <div class="band-group">
          <div class="group-title">AI 与外部能力</div>
          <div class="node-list">
            <article class="node-card">
              <div class="node-kicker">Capability</div>
              <div class="node-title">LLM / TTS / IM / MQ</div>
              <div class="node-meta">通过 RPC、消息或 SDK 接入外部能力</div>
            </article>
          </div>
        </div>
        <div class="band-group">
          <div class="group-title">数据底座</div>
          <div class="node-list">
            <article class="node-card">
              <div class="node-kicker">Data</div>
              <div class="node-title">MySQL / Redis / Logs / Topics</div>
              <div class="node-meta">提供存储、缓存、日志与异步链路支撑</div>
            </article>
          </div>
        </div>
      </div>
      <div class="flow-row">
        <span class="flow-chip">Client → Gateway</span>
        <span class="flow-chip">Gateway → Logic</span>
        <span class="flow-chip">Logic → Domain Service</span>
        <span class="flow-chip">Domain Service → Data / AI Capability</span>
      </div>
    </section>
  </main>
</div>
```
