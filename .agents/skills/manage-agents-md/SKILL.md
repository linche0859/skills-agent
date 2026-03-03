---
name: manage-agents-md
description: Helps create, manage, and optimize AGENTS.md files to provide context for AI coding agents. Use this when the user asks to configure project AI rules, define coding standards, or manage AGENTS.md files.
---

# Manage AGENTS.md files

You are an expert at configuring and optimizing `AGENTS.md` files. This file acts as persistent context that AI agents (like Copilot Workspace/CLI agents) read to understand project-specific rules, code styles, and workflows.

## 核心原則 (Core Principles)

When creating or modifying an `AGENTS.md` file, you MUST follow these best practices derived from official AI context guidelines:

1. **Apply Broadly (Use Skills for Specifics)**: `AGENTS.md` is loaded every session, so only include things that apply broadly. For domain knowledge or workflows that are only relevant sometimes, create and use **Skills** instead. Agents load them on demand without bloating every conversation.
2. **Keep it Short and Concise**: Bloated `AGENTS.md` files cause AI to lose focus and ignore instructions. For each line, ask: _"Would removing this cause the Agent to make mistakes?"_ If not, cut it.
3. **Review & Prune**: Treat `AGENTS.md` like code. If things go wrong, review it. If instructions are ambiguous to the AI, refine them. Prune the file regularly.
4. **Use Emphasis**: Tune instructions by adding emphasis (e.g., `**IMPORTANT**` or `**YOU MUST**`) to improve adherence.

## 內容守則 (Include vs Exclude)

Follow this strict criteria for what goes into `AGENTS.md` and what stays out:

| ✅ MUST Include | ❌ MUST Exclude |
| :--- | :--- |
| **Project-specific CLI commands** the Agent can’t guess. | Anything the Agent can figure out by reading the code itself. |
| **Code style rules** that differ from defaults. | Standard language conventions the Agent already knows. |
| **Testing instructions** and preferred test runners. | Detailed API documentation (provide links instead). |
| **Repository etiquette** (branch naming, PR conventions). | Information that changes frequently. |
| **Architectural decisions** specific to this project. | Long explanations or tutorials. |
| **Developer environment quirks** (required env vars). | File-by-file descriptions of the codebase. |
| **Common gotchas** or non-obvious behaviors. | Self-evident practices like “write clean code”. |

## Monorepo 架構支援 (Monorepo Architecture Support)

For Monorepo projects, `AGENTS.md` supports a powerful hierarchical structure:

- **Root vs Package Level**: Place a baseline `AGENTS.md` at the repository root for global rules, and place another `AGENTS.md` inside each specific package or subproject. 
- **Precedence**: Agents automatically read the nearest file in the directory tree, meaning **the closest `AGENTS.md` takes precedence**. 
- **Tailored Instructions**: Every subproject can ship tailored instructions. For example, a frontend package might have different rules than a backend package. Do not bloat the root `AGENTS.md` with package-specific rules; decentralize them.

## 建議支援的工作流程 (Execution Workflow)

When a user asks you to "initialize", "update", or "optimize" an `AGENTS.md` file, perform the following steps:

1. **Analyze Project Base**: Look at `package.json`, `tsconfig.json`, or the primary build/test tools in the repository. If working in a Monorepo, identify whether you are configuring the global root or a specific package.
2. **Draft the File**: Create a structured breakdown focusing on:
   - Command aliases (Build, Test, Lint)
   - Code Style (e.g., "Use ES modules", "Destructure imports when possible")
   - Workflow & Gotchas (e.g., "Prefer running single tests, not the whole suite")
3. **Refine**: Check the drafted content directly against the `❌ MUST Exclude` list in this skill to ensure you aren't bloating the file.
4. **Create/Update File**: Write the final optimized output to the appropriate `AGENTS.md` file (either root or the nearest specific package directory).
