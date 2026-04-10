# claude-dev-toolkit

English | [简体中文](README.md)

A Claude Code marketplace for developer productivity plugins and skills.

This repository provides installable marketplace plugins focused on software engineering workflows, such as unit test generation, architecture diagram creation, technical documentation, and other development automation tasks.

## What is this

`claude-dev-toolkit` is a plugin marketplace repository for Claude Code.

It is designed for developers who want to extend Claude Code with practical engineering tools that can be installed through the marketplace/plugin workflow, rather than manually copying individual skills.

The plugins in this repository are focused on common development scenarios, including:

- Generate unit test code
- Create technical architecture diagrams
- Produce engineering documentation
- Assist with code review and implementation tasks
- Improve developer workflow automation

## Who is this for

This repository is for:

- Backend engineers
- Full-stack developers
- AI application developers
- Technical leads
- Engineering teams using Claude Code in daily development

## Installation

Add this marketplace to Claude Code:

```bash
/plugin marketplace add jefferyjob/claude-dev-toolkit
````

After adding the marketplace, install a plugin from it:

```bash
/plugin install <plugin-name>@claude-dev-toolkit
```

## Skill list

| Skill | Description |
| --- | --- |
| `blueprinter` | Generates layered, color-coded technical architecture diagrams in a flat engineering blueprint style for architecture diagrams, system maps, flowcharts, and technical visualizations. |

## Design principles

This repository follows a few simple principles:

1. **Developer-first**
   Every plugin should solve a practical engineering problem.

2. **Installable**
   Plugins should be distributable through the Claude Code marketplace/plugin workflow.

3. **Clear structure**
   Each plugin is self-contained and easy to understand, maintain, and extend.

4. **Reusable**
   Skills should be written in a way that makes them broadly useful across different projects.

5. **Pragmatic**
   Focus on tools that help real development work move faster.

## Usage philosophy

These plugins are meant to help developers:

* reduce repetitive engineering work
* improve consistency in output quality
* speed up documentation and testing tasks
* support technical communication inside teams

They are not intended to replace engineering judgment.
Instead, they act as practical assistants for common development workflows.

## Contributing

Contributions are welcome.

You can contribute by:

* adding new developer-focused plugins
* improving existing skills
* refining documentation
* fixing plugin metadata and structure
* sharing better prompts and workflow patterns

## Notes

This repository is intended to be used with Claude Code's marketplace and plugin system.
Each plugin should include its own plugin metadata and one or more skills.

## License
This library is licensed under the MIT. See the LICENSE file for details.


