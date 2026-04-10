# claude-dev-toolkit

[English](README.en.md) | 简体中文

一个面向开发者效率插件与技能的 Claude Code 市场。

这个仓库提供可安装的市场插件，聚焦于软件工程工作流，例如单元测试生成、架构图创建、技术文档编写以及其他开发自动化任务。

## 这是什么

`claude-dev-toolkit` 是一个面向 Claude Code 的插件市场仓库。

它适用于希望通过 marketplace/plugin 工作流来扩展 Claude Code 的开发者，而不是手动复制单个 skill。

本仓库中的插件聚焦于常见开发场景，包括：

- 生成单元测试代码
- 创建技术架构图
- 产出工程文档
- 协助代码审查与实现任务
- 提升开发工作流自动化程度

## 适用人群

这个仓库适合：

- 后端工程师
- 全栈开发者
- AI 应用开发者
- 技术负责人
- 在日常开发中使用 Claude Code 的工程团队

## 安装

将这个 marketplace 添加到 Claude Code：

```bash
/plugin marketplace add jefferyjob/claude-dev-toolkit
```

添加 marketplace 后，从中安装插件：

```bash
/plugin install <plugin-name>@claude-dev-toolkit
```

## Skill 列表

| Skill | 说明 |
| --- | --- |
| blueprinter | 以扁平化工程蓝图风格生成分层彩色技术架构图，适用于架构图、系统图、流程图与技术可视化说明。 |

## 设计原则

本仓库遵循以下几个简单原则：

1. **开发者优先**
   每个插件都应解决一个实际的工程问题。

2. **可安装**
   插件应能够通过 Claude Code 的 marketplace/plugin 工作流进行分发。

3. **结构清晰**
   每个插件都应自包含，并且易于理解、维护和扩展。

4. **可复用**
   Skills 应以可在不同项目中广泛复用的方式编写。

5. **务实**
   专注于真正能帮助开发工作提速的工具。

## 使用理念

这些插件旨在帮助开发者：

* 减少重复性的工程工作
* 提升输出质量的一致性
* 加快文档与测试任务的推进
* 支持团队内部的技术沟通

它们并不是为了替代工程判断。

相反，它们是面向常见开发工作流的实用助手。

## 贡献

欢迎贡献。

你可以通过以下方式参与：

* 添加新的开发者导向插件
* 改进现有 skills
* 完善文档
* 修复插件元数据与结构问题
* 分享更好的提示词与工作流模式

## 说明

本仓库旨在配合 Claude Code 的 marketplace 和 plugin 系统使用。
每个插件都应包含其自身的插件元数据以及一个或多个 skill。

## 许可证
本库基于 MIT 协议授权。详情请参见 LICENSE 文件。