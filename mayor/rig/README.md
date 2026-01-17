# Claude Code Presentation

A comprehensive, world-class presentation on Claude Code usage.

## Overview

This presentation covers everything you need to know about Claude Code, Anthropic's agentic coding tool:

- What Claude Code is and why it matters
- Installation and setup
- Core concepts (CLAUDE.md, MCP, Slash Commands, Skills, Hooks, Subagents)
- Common workflows
- CLI reference
- Best practices
- Troubleshooting
- Resources for further learning

## Running the Presentation

This presentation uses `presenterm` - a terminal-based presentation tool.

### Install presenterm

```bash
brew install presenterm
```

Or install from: https://github.com/mfontanini/presenterm/

### Present

```bash
cd howtoclaude/mayor/rig
presenterm presentation.md
```

### Presenterm Controls

- `Space` or `→` - Next slide/animation
- `←` - Previous slide
- `q` - Quit
- `s` - Toggle speaker notes (if any)
- `e` - Execute code snippets (if executable)

## Presentation Structure

1. **Introduction** - What Claude Code is and the paradigm shift
2. **Installation** - Getting started
3. **Core Concepts** - CLAUDE.md, MCP, Slash Commands
4. **Skills & Hooks** - Knowledge bases and automation
5. **Subagents** - Specialized task delegation
6. **Workflows** - Common development scenarios
7. **CLI Reference** - Essential commands
8. **Best Practices** - Pro tips for effective usage
9. **Resources** - Where to learn more

## Research Sources

This presentation is based on comprehensive research from:

- Official Anthropic documentation (docs.anthropic.com)
- ClaudeLog (claudelog.com) - Community resource
- 2026 blog posts and guides
- Reddit communities (r/ClaudeAI, r/ClaudeCode)
- GitHub repositories and examples

## Updating the Presentation

To update the content:

1. Edit `presentation.md`
2. Keep the presenterm format (`---` for slide breaks, `<!-- pause -->` for animations)
3. Test your changes with `presenterm presentation.md`

## Contributing

Feel free to enhance this presentation with:
- Real-world examples from your projects
- Team-specific conventions
- Additional MCP server configurations
- Custom slash commands
- Industry-specific workflows
