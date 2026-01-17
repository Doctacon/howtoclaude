---
title: Working with Claude Code
sub_title: A Comprehensive Yet Concise Guide
author: Claude Code
theme:
  name: dark
---

## Introduction

Claude Code is Anthropic's official CLI for building software with AI assistance.

It combines powerful models with tool use to:
- Read, write, and edit code
- Run terminal commands
- Search and navigate codebases
- Manage multi-step tasks with todos

## Core Philosophy

**Claude Code is your development partner**, not just a chat bot.

Key principles:
- __Read files before editing them__
- Prefer edits over writing new files
- Use parallel tool calls for efficiency
- Ask clarifying questions when needed

## Getting Started

```bash
# Install Claude Code
curl -fsSL https://claude.ai/install.sh | sh

# Start a session
claude

# Or work in a specific directory
claude /path/to/project
```

## Conversation Flow

1. **State your goal** clearly
2. Claude reads relevant files
3. Claude proposes changes
4. You review and approve
5. Claude executes and verifies

_Pro tip: Be specific about what you want for better results._

## File Operations

Claude can:

- **Read** any file in your project
- **Edit** existing files with precise string replacement
- **Write** new files when needed
- **Search** using glob patterns and grep

```
Claude: "Let me read the config file..."
[Reads src/config.yaml]
Claude: "I'll update the timeout setting..."
[Edits the file]
```

## Terminal Integration

Claude runs commands directly:

```bash
# Build the project
npm run build

# Run tests
pytest

# Check git status
git status
```

_No copy-pasting needed—Claude executes everything._

## Code Navigation

Claude understands your codebase structure:

```bash
# Find all TypeScript files
**/*.ts

# Search for function definitions
function \w+\(

# Locate API endpoints
@app\.route
```

_Claude uses specialized tools—don't ask it to run grep/find directly._

## Task Management

For complex work, Claude uses __todos__:

- Breaks down large tasks into steps
- Tracks progress in real-time
- Marks tasks complete as it works
- Gives you visibility into the workflow

## Advanced Features

**Parallel Execution:**
Claude makes multiple independent tool calls at once for speed.

**Context Awareness:**
Claude remembers conversation history across turns (with automatic summarization for long sessions).

**Error Recovery:**
Claude debugs issues and tries alternative approaches.

## Best Practices

__DO:__
- Give clear, specific instructions
- Let Claude read before editing
- Use Claude for multi-step workflows
- Review proposed changes

__DON'T:__
- Manually copy-paste code
- Skip Claude's file reading
- Use Claude for trivial one-liners
- Assume Claude can read your mind

## Common Workflows

**Adding a feature:**
1. Describe what you want
2. Claude explores the codebase
3. Claude identifies files to modify
4. Claude implements changes
5. Claude runs tests to verify

**Debugging:**
1. Show Claude the error
2. Claude investigates the code
3. Claude proposes fixes
4. Claude tests the solution

## Tips for Better Results

- __Provide context__: "Add authentication to the API" → "Add JWT authentication to the /api/users endpoint"
- __Show examples**: "Format dates like this: 2025-01-17"
- **Iterate**: "That's close, but can you make the button blue instead?"
- **Use natural language**: You don't need to be technical or precise

## Limitations

Claude Code:
- __Cannot__ browse the web (unless web search tools are enabled)
- __Cannot__ access files outside your project without permission
- __Does not__ remember conversations across different sessions
- __Cannot__ execute commands without showing you (transparent operation)

## Getting Help

In Claude Code, type `/help` to see:
- All available commands
- Keyboard shortcuts
- Configuration options

Found a bug? Report it at:
**github.com/anthropics/claude-code/issues**

## Summary

Claude Code = AI-powered development partner

**Key strengths:**
- Reads and writes code automatically
- Runs terminal commands directly
- Navigates complex codebases
- Manages multi-step tasks

**Your role:**
- Provide clear direction
- Review and approve changes
- Give feedback and iterate

_Together, you ship code faster._

## Questions?

**Resources:**
- Docs: docs.anthropic.com
- GitHub: github.com/anthropics/claude-code
- Community: community.anthropic.com

__Thanks for watching!__
