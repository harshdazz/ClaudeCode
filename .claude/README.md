# Claude Code Personal Configuration

This repository contains my personal [Claude Code](https://claude.ai/code) configuration — including global instructions, custom commands, skills, and plugin management settings.

## What This Is

Claude Code stores its user configuration in `~/.claude/`. This repo is a version-controlled snapshot of that directory, making it easy to back up, share, and restore my setup across machines.

## Repository Structure

```
.claude/
├── CLAUDE.md                          # Global instructions loaded into every Claude session
├── settings.json                      # Claude Code global settings (auto-update channel, etc.)
├── commands/
│   └── review.md                      # /review — code review slash command
├── skills/
│   └── code-quality/
│       └── SKILL.md                   # Auto-triggered skill for enforcing code quality standards
└── plugins/
    ├── blocklist.json                 # Plugins blocked from installation
    ├── known_marketplaces.json        # Registered plugin marketplace sources
    └── marketplaces/
        └── claude-plugins-official/   # Official Anthropic plugins marketplace (separate git repo)
```

> **Note:** The `plugins/marketplaces/claude-plugins-official/` directory is a separately managed git repository cloned from [anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official). It is excluded from this repo via `.gitignore`.

## Custom Commands

| Command | Description |
|---------|-------------|
| `/review` | Reviews code for security vulnerabilities, performance issues, error handling, style consistency, and test coverage gaps |

## Skills

Skills are automatically triggered by Claude based on context — no manual invocation needed.

| Skill | Trigger | Behavior |
|-------|---------|----------|
| `code-quality` | When writing or reviewing code | Enforces style guide, meaningful naming, function length limits, error handling, and early returns |

## Installed Plugins

These plugins are installed locally but their files are not tracked in this repo (see `.gitignore`):

- **plugin-dev** — Toolkit for creating new Claude plugins (hooks, MCP, commands, agents, skills)
- **commit-commands** — Git commit, push, and PR workflow automation
- **feature-dev** — Multi-agent feature development workflow
- **claude-md-management** — CLAUDE.md creation and improvement tools
- **hookify** — Hook-based automation configuration

## Setup on a New Machine

1. Clone this repo into your `~/.claude` directory:
   ```bash
   git clone https://github.com/harshdazz/ClaudeCode.git ~/.claude
   ```

2. Clone the official plugins marketplace:
   ```bash
   git clone https://github.com/anthropics/claude-plugins-official \
     ~/.claude/plugins/marketplaces/claude-plugins-official
   ```

3. Reinstall plugins as needed from within Claude Code:
   ```
   /plugin install plugin-dev@claude-plugins-official
   /plugin install commit-commands@claude-plugins-official
   /plugin install feature-dev@claude-plugins-official
   /plugin install claude-md-management@claude-plugins-official
   /plugin install hookify@claude-plugins-official
   ```

## What Is Not Tracked

The `.gitignore` intentionally excludes:

- **Credentials** — `.credentials.json`, `mcp-needs-auth-cache.json`
- **Runtime/session data** — `todos/`, `debug/`, `projects/`, `plans/`, history files, stats, cache
- **Marketplace repo** — managed separately as its own git repository

## Requirements

- [Claude Code](https://claude.ai/code) installed
- Git
