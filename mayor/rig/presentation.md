---
title: Claude Code
subtitle: The Complete Guide to Agentic Coding in Your Terminal
author: Based on 2026 Research
---

# What is Claude Code?

Claude Code is Anthropic's **agentic coding tool** that lives in your terminal and understands your entire codebase.

## Key Capabilities

* Terminal-native development environment
* Multi-file editing with codebase awareness
* Git workflow automation (issues, tests, PRs)
* Extended thinking for complex tasks
* Enterprise integration (AWS Bedrock, GCP Vertex)

---

<!-- end_slide -->

# Why Claude Code?

Unlike traditional AI coding assistants that require **copy-paste workflows**, Claude Code integrates directly with your development environment.

## The Paradigm Shift

* **Before**: Copy code to AI, copy response back, repeat
* **Now**: Set tasks, monitor progress in real-time, review completed work

Claude Code's environment **is** your development environment.

---

<!-- end_slide -->

# Installation & Setup

```bash
# Install via Homebrew (macOS/Linux)
brew install claude-code

# Or download from GitHub releases
# https://github.com/anthropics/claude-code
```

<!-- pause -->

## Authentication

```bash
claude auth login
```

This opens a browser for secure authentication via Anthropic.

---

<!-- end_slide -->

# Core Concepts

## The Big Three

1. **CLAUDE.md** - Project context & instructions
2. **MCP Servers** - Model Context Protocol integrations
3. **Slash Commands** - Reusable workflows

These transform Claude from a chatbot into a **deterministic engineering engine**.

---

<!-- end_slide -->

# CLAUDE.md

## What It Is

A markdown file in your project root that provides context to Claude Code about your codebase, conventions, and preferences.

## Best Practices

<!-- pause -->

1. **Start with a one-liner** explaining the project
2. **Include specific, actionable** code style preferences
3. **Add architecture context** only when relevant
4. **Keep it concise** - overload reduces effectiveness
5. **Iterate based on** Claude's assumptions

```markdown
# Project Context

This is a React Native fitness app using TypeScript.

## Code Style
- Use functional components with hooks
- Prefer composition over inheritance
- Follow Airbnb style guide
```

---

<!-- end_slide -->

# MCP Servers

## Model Context Protocol

MCP enables Claude Code to connect to external tools, APIs, and data sources without hard-coded integrations.

## Popular MCP Servers (2026)

* **GitHub** - PR/issue management
* **PostgreSQL/MySQL** - Database queries
* **Slack** - Team notifications
* **Filesystem** - Direct file operations
* **Browser** - Web scraping & research

## Configuration

```yaml
# ~/.claude/mcp_config.json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@anthropic-ai/mcp-server-github"]
    }
  }
}
```

---

<!-- end_slide -->

# Slash Commands

## What They Are

Reusable prompts saved as markdown files that automate common workflows.

## Creating Commands

```bash
# Location: .claude/commands/test.md or ~/.claude/commands/test.md
```

```markdown
# Run the test suite

Run all tests using npm test. If tests fail, analyze the output and suggest fixes.
```

## Usage

```bash
claude> /test
```

Claude executes the defined workflow automatically.

---

<!-- end_slide -->

# Skills

## SKILL.md Files

Skills are knowledge bases that guide Claude on specific tasks.

**Key Difference from Commands:**
* Commands = workflows ("run tests")
* Skills = expertise ("how to write React hooks")

## Example Skill

```markdown
# React Testing Best Practices

## Testing Components
1. Test user behavior, not implementation details
2. Use @testing-library/react
3. Avoid testing internal state

## Example
```tsx
test('submits form', () => {
  render(<ContactForm />);
  fireEvent.change(screen.getByLabelText('Email'), {target: {value: 'a@b.c'}});
  fireEvent.click(screen.getByText('Submit'));
  expect(submitForm).toHaveBeenCalled();
});
```
```

---

<!-- end_slide -->

# Hooks

## Event-Driven Automation

Hooks trigger actions at specific points in the Claude Code lifecycle.

## Hook Types

* **pre-build** - Before compilation
* **post-commit** - After git commits
* **on-error** - When commands fail
* **session-start** - When opening a project

## Example

```yaml
# .claude/hooks.yaml
post-commit:
  - run: npm run lint
  - run: npm test
```

---

<!-- end_slide -->

# Subagents

## Specialized Task Delegation

Subagents are specialized Claude instances with specific tools and capabilities.

## When to Use

* **Plan agent** - Architecture design, implementation strategy
* **Test agent** - Test suite creation and execution
* **Explore agent** - Codebase understanding and pattern discovery
* **General-purpose** - Research, multi-step tasks

Subagents run in parallel for maximum efficiency.

---

<!-- end_slide -->

# Common Workflows

## 1. Bug Fixing

```
"Fix the authentication bug in src/auth/login.ts"
```

Claude reads the file, identifies the issue, proposes a fix, and tests it.

---

<!-- pause -->

## 2. Feature Development

```
"Add user profile editing with validation"
```

Claude:
1. Analyzes existing code structure
2. Plans implementation
3. Writes the code
4. Creates tests
5. Submits PR

---

<!-- pause -->

## 3. Code Refactoring

```
"Extract duplicate logic into a shared utility"
```

Claude identifies patterns, creates abstractions, and updates all references.

---

<!-- end_slide -->

# CLI Reference

## Essential Commands

```bash
# Start Claude Code
claude

# Navigate to a topic
claude code /test

# Get help
claude --help

# Check version
claude --version
```

## Within Claude Code

```
/help           # Show all commands
/clear          # Clear conversation
/commit         # Create git commit
/review-pr      # Review a pull request
```

---

<!-- end_slide -->

# Advanced Features

## Parallel Execution

Claude can launch multiple subagents simultaneously:

```
"Run tests in parallel: unit tests, integration tests, and linting"
```

## Background Tasks

```
"Run the build in the background and notify me when complete"
```

## Plan Mode

```
"Enter plan mode for the new payment feature"
```

Claude explores the codebase and presents an implementation plan for approval before writing code.

---

<!-- end_slide -->

# Best Practices

## 1. Provide Context

> "Fix the bug in the payment flow" vs "Fix the Stripe integration bug in src/payments/stripe.ts where customers are charged twice"

Specific prompts yield specific results.

---

<!-- pause -->

## 2. Iterate on CLAUDE.md

Review and refine your CLAUDE.md based on:
* Claude's incorrect assumptions
* Repetitive explanations
* Team-specific conventions

---

<!-- pause -->

## 3. Use Slash Commands for Repetition

If you find yourself giving the same instructions repeatedly, create a slash command.

---

<!-- pause -->

## 4. Let Claude Read Files

Don't paste code - let Claude read it directly:
> "Read src/components/Header.tsx and make it responsive"

---

<!-- pause -->

## 5. Trust but Verify

Claude makes mistakes. Always review generated code, run tests, and validate outputs.

---

<!-- end_slide -->

# VS Code Integration

## Claude Code Extension

Full VS Code integration available for seamless workflow.

## Features

* Sidebar chat interface
* Inline code suggestions
* File context awareness
* Integrated terminal

## Setup

```bash
code --install-extension anthropic.claude-code
```

---

<!-- end_slide -->

# Troubleshooting

## Common Issues

### Claude ignores CLAUDE.md
* Ensure file is in project root
* Check for syntax errors in markdown
* Verify Claude Code is running in project directory

### MCP servers not connecting
* Check `~/.claude/mcp_config.json` syntax
* Verify server dependencies are installed
* Check Claude Code logs: `claude --log-level debug`

### Slow performance
* Reduce CLAUDE.md context
* Use `.gitignore` to exclude large directories
- Consider using `plan mode` for complex tasks

---

<!-- end_slide -->

# Key Takeaways

1. **CLAUDE.md** provides project-specific context and instructions
2. **MCP servers** extend Claude's capabilities with external tools
3. **Slash commands** automate repetitive workflows
4. **Skills** encode best practices and domain expertise
5. **Hooks** enable event-driven automation
6. **Subagents** delegate specialized tasks efficiently

Claude Code transforms AI from a chatbot into an **agentic development partner** that understands, acts, and delivers.

---

<!-- end_slide -->

# Resources

## Official Documentation

* [Claude Code Docs](https://docs.anthropic.com/en/docs/claude-code/overview)
* [GitHub Repository](https://github.com/anthropics/claude-code)
* [Best Practices](https://www.anthropic.com/engineering/claude-code-best-practices)

## Community Resources

* [ClaudeLog](https://claudelog.com) - Tutorials & best practices
* [r/ClaudeAI](https://reddit.com/r/ClaudeAI) - Community discussions
* [r/ClaudeCode](https://reddit.com/r/ClaudeCode) - Code-specific discussions

## Guides (2026)

* [Complete Guide to Claude Code](https://blakecrosley.com/guide/claude-code)
* [CLAUDE.md Guide](https://www.builder.io/blog/claude-md-guide)
* [MCP Server Setup](https://generect.com/blog/claude-mcp/)

---

<!-- end_slide -->

# Questions?

<!-- end_slide -->
