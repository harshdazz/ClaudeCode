# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is the Claude Code user configuration directory (`~/.claude`). It contains personal Claude Code settings and a cloned copy of the official Claude Code plugins marketplace.

## Key Locations

- `settings.json` - Claude Code global settings (auto-update channel, permissions, etc.)
- `plugins/marketplaces/claude-plugins-official/` - Official Claude Code plugins marketplace (git repo)
- `memory/` - Persistent memory files used across sessions
- `todos/` - Claude Code task tracking files (auto-managed)
- `debug/` - Debug logs from Claude Code sessions

## Plugins Marketplace Structure

The marketplace repo at `plugins/marketplaces/claude-plugins-official/` contains two categories:

- `plugins/` - Internal plugins developed and maintained by Anthropic
- `external_plugins/` - Third-party partner plugins

Each plugin follows this layout:
```
plugin-name/
├── .claude-plugin/plugin.json   # Required metadata (name, version, description)
├── .mcp.json                    # Optional MCP server configuration
├── commands/                    # Slash commands (markdown files with YAML frontmatter)
├── agents/                      # Agent definitions (markdown with system prompts)
├── skills/                      # Skill definitions (SKILL.md files)
├── hooks/                       # Hook configurations (hooks.json)
└── README.md
```

### Plugin Components

**Commands** (`commands/*.md`) - User-invoked via `/command-name`. Frontmatter fields:
- `description`, `argument-hint`, `allowed-tools`

**Skills** (`skills/<name>/SKILL.md`) - Model-invoked based on trigger phrases. Frontmatter fields:
- `name`, `description` (trigger conditions), `version`

**Agents** (`agents/*.md`) - Autonomous subagents with YAML frontmatter + system prompt. Frontmatter fields:
- `name`, `description` (with `<example>` blocks for reliable triggering), `model`, `color`, `tools`

**Hooks** (`hooks/hooks.json`) - Event-driven automation for: `PreToolUse`, `PostToolUse`, `Stop`, `SubagentStop`, `SessionStart`, `SessionEnd`, `UserPromptSubmit`, `PreCompact`, `Notification`

**MCP Servers** (`.mcp.json`) - Configures external tool integration via Model Context Protocol. Supports stdio (local), SSE (hosted/OAuth), HTTP (REST) server types.

### Plugin Installation

```bash
/plugin install {plugin-name}@claude-plugin-directory
```

### Key Environment Variable

`${CLAUDE_PLUGIN_ROOT}` - Use this for portable paths within plugin scripts and configurations.

## Notable Installed Plugins

- **plugin-dev** - Toolkit for creating new plugins (7 skills covering hooks, MCP, commands, agents, skills, structure, settings)
- **commit-commands** - Git commit/push/PR workflows
- **feature-dev** - Multi-agent feature development workflow
- **claude-md-management** - CLAUDE.md creation and improvement
- **hookify** - Hook-based automation configuration
