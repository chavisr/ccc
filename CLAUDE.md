# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a personal repository (Chavis Claude Code - ccc) for storing:
- Custom Claude agents
- Claude Code skills
- Claude Code configurations and setup

This is not a software project with build/test commands - it's a collection of agent definitions and configuration files.

## Repository Structure

```
ccc/
├── agents/          # Custom agent definitions (markdown files)
├── skills/          # Custom skills for Claude Code
├── examples/        # Example CLAUDE.md files demonstrating agent usage
└── configs/         # Configuration files (future)
```

## Shell Script Agents

The `agents/` directory contains specialized shell script agents based on the Google Shell Style Guide:

### Available Agents

1. **shell-writer.md** - Creates new shell scripts following best practices
   - Use for: Writing shell scripts from scratch (< 100 lines)
   - Template-based approach with complete error handling
   - Focus: Bash scripts with `set -euo pipefail`, proper quoting, documentation

2. **shell-reviewer.md** - Reviews existing shell scripts for compliance
   - Use for: Code review of shell scripts against Google Shell Style Guide
   - Provides specific feedback with line numbers and examples
   - Output: Categorized issues (critical/style/best-practice) with ratings

3. **shell-refactor.md** - Refactors shell scripts to comply with standards
   - Use for: Improving existing shell scripts while preserving functionality
   - Incremental approach: critical fixes → style → best practices → documentation
   - Focus: Preserve functionality, test between changes

### Common Shell Script Principles

All three agents follow these core principles:
- **Shebang**: Always `#!/bin/bash`
- **Formatting**: 2-space indentation, 80-char line limit
- **Naming**: lowercase_with_underscores for functions/variables, UPPERCASE for constants
- **Quoting**: Always quote variables: `"${var}"`
- **Tests**: Use `[[ ]]` not `[ ]`
- **Arithmetic**: Use `(( ))` or `$(( ))` not `let`/`expr`
- **Command substitution**: `$(command)` not backticks
- **Error handling**: Check return codes, route errors to stderr with `>&2`
- **Scope**: Use `local` for function variables
- **Arrays**: Use arrays for lists, not space-separated strings
- **Script size**: If > 100 lines, suggest rewriting in Python/Ruby/etc

### When to Use Each Agent

- **Writing new shell script?** → Use shell-writer.md
- **Reviewing someone's shell script?** → Use shell-reviewer.md
- **Fixing/improving existing shell script?** → Use shell-refactor.md

## Jenkins Pipeline Agent

The repository includes a specialized Jenkins agent for creating and reviewing Jenkins declarative pipelines.

### Available Agent

**jenkins-pipeline.md** - Creates and reviews Jenkins declarative pipelines
- Use for: Writing Jenkins pipelines following best practices
- Template: Complete pipeline template embedded in the agent markdown
- Focus: Declarative pipelines with proper credentials, Docker integration, cleanup

### Jenkins Pipeline Principles

The agent follows these core principles:
- **Syntax**: Declarative pipeline (`pipeline { }`) only
- **Documentation**: Comprehensive header comments (structure, requirements, credentials)
- **Options**: Always configure ansiColor, buildDiscarder, disableConcurrentBuilds, timeout, timestamps
- **Credentials**: Secure handling with `withCredentials`, export to `.env` file
- **Docker**: Standardized pattern with Docker registry, user mapping, env-file
- **Cleanup**: Always use `deleteDir()` in `post.always` block
- **Parameters**: Support choice and string types with descriptions

### When to Use Jenkins Agent

- **Writing new Jenkins pipeline?** → Use jenkins-pipeline.md
- **Reviewing Jenkins pipeline?** → Use jenkins-pipeline.md
- **Need Jenkins best practices?** → jenkins-pipeline.md includes complete template

## Marp Presentation Agent

The repository includes a specialized agent for creating professional presentation slides using Marp (Markdown Presentation Ecosystem).

### Available Agent

**marp-slides.md** - Creates professional presentations using Marp
- Use for: Creating slide decks from markdown for technical or non-technical audiences
- Templates: Complete embedded templates for both technical and non-technical presentations
- Focus: Professional design, appropriate complexity for audience, easy HTML export
- Option: Can render HTML automatically or let user do it manually

### Marp Presentation Principles

The agent follows these core principles:
- **Audience-First**: Different templates and approaches for technical vs non-technical audiences
- **Theme Selection**: Uses default Marp themes (default, gaia, uncover) for consistency
- **Professional Fonts**: Relies on built-in theme fonts for portability
- **Image Management**: Checks `assets/` directory for images; stops if user wants images but none found
- **Structure**: Title slide, agenda, content, closing (Q&A)
- **Export**: Designed for HTML rendering via `marp` CLI

### Presentation Types

**Technical Presentations:**
- Code snippets with syntax highlighting
- Architecture diagrams
- Technical terminology acceptable
- Detailed metrics and benchmarks
- Structured technical content

**Non-Technical Presentations:**
- Simple language, no jargon
- Business value focus
- Visual storytelling
- Customer success stories
- ROI and impact emphasis

### Repository Structure for Marp Projects

```
presentation-project/
├── slides.md              # Main presentation (Marp markdown)
├── assets/                # Images, diagrams, logos
│   ├── logo.png
│   ├── diagram-1.png
│   └── ...
├── output/                # Generated HTML presentations
│   └── presentation.html
└── README.md              # Build instructions
```

### When to Use Marp Agent

- **Creating presentation for technical team?** → Use marp-slides.md (technical template)
- **Creating presentation for executives/business?** → Use marp-slides.md (non-technical template)
- **Need professional slide deck from markdown?** → Use marp-slides.md

## Working with This Repository

### Adding New Agents
When adding new agent definitions:
- Create markdown files in `agents/` directory
- Follow clear agent role definition pattern
- Include examples and templates where applicable
- Document the agent's purpose and use cases

**Code Example Approach:**
- **Embedded templates**: All agents include code directly in markdown using code blocks
  - Ensures portability - agents work from any directory when symlinked to ~/.claude
  - Self-contained - no external file dependencies
  - Complete templates serve as authoritative patterns

### File Format
Agent files are markdown documents that define:
- Agent role and specialization
- Core principles and guidelines
- Examples and patterns
- Output format expectations
- Quality checklists

This repository uses git with `main` as the default branch.
