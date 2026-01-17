---
title: Working with Claude Code
sub_title: The Complete Guide to Agentic Coding
author: Based on Official Claude Code Documentation
theme:
  name: dark
---

## What is Claude Code?

Claude Code is Anthropic's **agentic coding tool** that lives in your terminal, understands your codebase, and helps you code faster by executing routine tasks, explaining complex code, and handling git workflows—all through natural language commands.

__Unlike traditional AI assistants__, Claude Code integrates directly with your development environment, taking action on your behalf rather than just generating text.


## Key Capabilities

**Build features from descriptions**
Tell Claude what you want in plain English. It plans, writes code, and ensures it works.

**Debug and fix issues**
Describe bugs or paste errors. Claude analyzes your codebase, identifies problems, and implements fixes.

**Navigate any codebase**
Ask questions about your project and get thoughtful answers with full context awareness.

**Automate tedious tasks**
Fix lint issues, resolve merge conflicts, write release notes—all via single commands.


## Installation

```bash
# Native Install (Recommended)
curl -fsSL https://claude.ai/install.sh | bash

# Homebrew (macOS/Linux)
brew install --cask claude-code

# WinGet (Windows)
winget install Anthropic.ClaudeCode

# Start using Claude Code
claude
```

**Prerequisites**: Claude subscription (Pro, Max, Teams, Enterprise) or Claude Console account


## Core Concepts

Claude Code extends through **four key mechanisms**:

1. **CLAUDE.md** - Project context and guidelines
2. **MCP** - Model Context Protocol for external integrations
3. **Slash Commands** - Reusable workflows (manual invocation)
4. **Agent Skills** - Context-aware capabilities (automatic invocation)


## CLAUDE.md

A markdown file in your project root that provides context about your codebase, conventions, and preferences.

**Best practices:**
- Start with a one-liner explaining the project
- Include specific, actionable code style preferences
- Add architecture context when relevant
- Keep it concise—overload reduces effectiveness
- Use progressive disclosure: simple → complex


## MCP (Model Context Protocol)

Claude Code functions as both an MCP **server** and **client**, connecting to hundreds of external tools and data sources.

**What MCP enables:**
- Implement features from JIRA, GitHub Issues
- Analyze monitoring data from Sentry, Statsig
- Query databases (PostgreSQL, MongoDB)
- Integrate designs from Figma, Google Drive
- Automate workflows with Gmail, Slack, Asana


## Installing MCP Servers

```bash
# HTTP servers (recommended for cloud services)
claude mcp add --transport http notion https://mcp.notion.com/mcp

# SSE servers
claude mcp add --transport sse asana https://mcp.asana.com/sse

# Local stdio servers
claude mcp add --transport stdio --env API_KEY=xxx api -- npx -y server-package
```

**MCP scopes:**
- **Local**: Project-specific (`~/.claude.json`)
- **Project**: Team-shared via `.mcp.json` in version control
- **User**: Cross-project in `~/.claude.json`


## Slash Commands

Reusable workflows you invoke manually with `/command` syntax.

**Installation:**
- Project-specific: `.claude/commands/`
- Personal: `~/.claude/commands/` for global use

**Example:**
```markdown
<!-- .claude/commands/review.md -->
Review the current changes for security issues,
performance problems, and maintainability.
```

Usage: `/review`


## Agent Skills

Model-invoked extensions that activate **automatically** based on task context.

**Built-in Skills:**
- `commit-message-generator` - Generates commit messages from diffs
- `review-pr` - Reviews PRs by analyzing changes
- `summarize-project` - Provides project overviews
- `summarize-text` - Condenses long documents

**Custom Skills:**
Create `SKILL.md` files with YAML frontmatter:

```text
name: code-review
description: Review code for security, performance, and maintainability
```

The `---` delimiters wrap the frontmatter section.


## Permission Modes

**Plan Mode** (`⏸ plan mode on`)
Read-only exploration. Perfect for new codebases and planning.

**Normal Mode**
Asks before each action. Safe for learning.

**Auto-Accept Mode** (`⏵⏵ accept edits on`)
Pre-approves all edits. For trusted workflows.

**Cycle modes**: `Shift+Tab`


## Extended Thinking

**Thinking Mode** (default: enabled)
Up to 31,999 tokens for internal reasoning on complex tasks.

**Toggle**: `Option+T` (macOS) or `Alt+T` (Windows/Linux)

**View thinking**: Press `Ctrl+O` to see Claude's reasoning process

**Configure**: Set `MAX_THINKING_TOKENS` environment variable

**Best for**: Complex architectural decisions, challenging bugs, multi-step planning


## Plan Mode

**Purpose**: Read-only analysis for safe code exploration and planning

**Activation**: `Shift+Tab` to cycle modes or `claude --permission-mode plan`

**Workflow:**
1. Start in Plan Mode for complex tasks
2. Let Claude interview you to clarify requirements
3. Review the plan before implementation
4. Execute step-by-step with checkpoints

**Use cases**: Multi-step implementations, code exploration, interactive development


## Interview Mode

Let Claude interview you to fill in requirements for large features.

**Benefits:**
- Produces better specs than anticipating everything upfront
- Uses multiple-choice requirement gathering
- Most active in Plan Mode

**When to use**: Large features, ambiguous requirements, complex user stories


## Session Management

**Resume sessions:**
```bash
claude --continue      # Most recent conversation
claude --resume        # Picker for previous sessions
```

**Name sessions**: Give descriptive names for easier tracking

**Git worktrees**: Run parallel sessions with complete code isolation

**Fork sessions**: Use `/rewind` or `--fork-session` for experimentation


## Git Integration

**Conversational Git operations:**
- "commit my changes"
- "show last 5 commits"
- "create a new branch called feature/auth"

**Built-in commit generation**: Automatic commit message creation from diffs

**Merge conflict resolution**: Automated conflict handling

**Branch management**: Create branches, manage worktrees


## GitHub Actions Integration

**Quick setup**: Run `/install-github-app` command

**@claude mentions**: Trigger Claude from PR/issue comments

**Slash commands**: Use `/review`, `/fix`, etc. in workflows

**Cloud support**: AWS Bedrock and Google Vertex AI integration

**Enterprise**: Custom GitHub Apps, OIDC authentication


## Essential Commands

| Command | Purpose |
|---------|---------|
| `claude` | Start interactive mode |
| `claude "task"` | Run one-time task |
| `claude -p "query"` | One-off query, then exit |
| `claude -c` | Continue most recent conversation |
| `claude -r` | Resume previous conversation |
| `claude --permission-mode plan` | Start in Plan Mode |
| `/help` | Show available commands |
| `/clear` | Clear conversation history |


## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+C` | Exit Claude Code |
| `Ctrl+O` | Toggle verbose mode (see thinking) |
| `Shift+Tab` | Cycle permission modes |
| `Option/Alt+T` | Toggle thinking mode |


## Best Practices: Plan Then Execute

For complex tasks:

1. **Start in Plan Mode** - Read-only exploration
2. **Let Claude interview you** - Clarify requirements
3. **Review the plan** - Before implementation
4. **Execute step-by-step** - With checkpoints

This workflow prevents costly mistakes and ensures alignment.


## Best Practices: Task-Based Execution

**Break large features into smaller, testable chunks**

Use Git worktrees for parallel development streams

Leverage session naming to track multiple workstreams

**Example**: Instead of "build the entire auth system", try "add password reset flow" then "add 2FA integration"


## Best Practices: Project Memory

Use `CLAUDE.md` at repository root for:
- Coding standards and style preferences
- Review criteria and quality gates
- Preferred patterns and conventions
- Technology stack and architecture decisions
- Team conventions and workflows

**Progressive disclosure**: Start simple, layer in complexity


## Best Practices: Prompting

**Be specific** about what behavior you want to verify

**Provide context** about existing patterns and conventions

**Ask Claude to identify edge cases** you might have missed

**Use Plan Mode** for architectural decisions

**Example**: "Add input validation to prevent SQL injection in the user signup form" is better than "fix security issues"


## Security and Permissions

**Permission Modes control what Claude can do:**
- **Plan Mode**: No edits, read-only
- **Normal Mode**: Approval required for each action
- **Auto-Accept**: Pre-approve all edits

**Tool Restrictions**: Configure allowed/disallowed tools in `settings.json`

**Enterprise Security**:
- SAML/OIDC for SSO integration
- Managed MCP for centralized server control
- Network configuration for corporate proxies
- AWS/GCP hosting for data residency


## Cost Optimization

**GitHub Actions:**
- Use specific `@claude` commands to reduce API calls
- Configure `--max-turns` to prevent excessive iterations
- Set workflow-level timeouts

**API Usage:**
- Be specific in prompts to reduce token usage
- Use Plan Mode to avoid unnecessary edits
- Set `MAX_THINKING_TOKENS` appropriately
- Enable tool search when MCP definitions exceed 10% of context


## Team Collaboration

**Shared Configuration:**
- Check `.claude/` directory into version control
- Use project-scoped MCP servers via `.mcp.json`
- Create team marketplaces for plugin distribution
- Document conventions in `CLAUDE.md`

**Code Reviews:**
- Use `/review` slash command for consistency
- Define review criteria in Skills
- Leverage Plan Mode for PR analysis


## Common Workflows

**Adding a feature:**
1. Describe what you want
2. Claude explores the codebase (use Plan Mode)
3. Claude identifies files to modify
4. Claude implements changes
5. Claude runs tests to verify

**Debugging:**
1. Paste the error message
2. Claude investigates in Plan Mode
3. Claude proposes fixes
4. Claude tests the solution

**Code review:**
1. Use `/review` or `review-pr` skill
2. Claude analyzes changes
3. Claude provides feedback


## Why Developers Love Claude Code

**Terminal-native**
Works where you already work—not another chat window or IDE

**Action-oriented**
Can directly edit files, run commands, and create commits

**Unix philosophy**
Composable and scriptable—pipes and redirects work naturally

**Enterprise-ready**
AWS/GCP hosting, enterprise-grade security and compliance


## Resources

**Official Documentation:**
- code.claude.com/docs
- platform.claude.com/docs

**GitHub:**
- github.com/anthropics/claude-code

**Community:**
- Community Discord
- GitHub Issues for bug reports

**Built-in Help:**
Type `/help` in Claude Code for commands and configuration


## Summary

Claude Code = AI-powered development partner

**Key capabilities:**
- Builds features from descriptions
- Debugs and fixes issues
- Navigates complex codebases
- Automates tedious tasks
- Integrates with tools via MCP

**Your role:**
- Provide clear direction
- Review and approve changes
- Give feedback and iterate

_Together, you ship code faster._


## Questions?

**Key takeaways:**
- Start with `CLAUDE.md` for project context
- Use Plan Mode for complex tasks
- Extend with MCP, Skills, and Commands
- Leverage Git integration and GitHub Actions
- Follow best practices for optimal results

__Thanks for watching!__

code.claude.com | github.com/anthropics/claude-code
