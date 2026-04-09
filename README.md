# Chavis Claude Code

Personal repository for Claude Code agents, skills, configurations, and reference materials.

## Overview

This repository contains custom Claude agents, skills, and reference materials for working with Claude Code CLI. It focuses on specialized agents that help with common development tasks following established best practices.

## Repository Structure

```
ccc/
├── agents/          # Custom agent definitions (markdown files)
├── skills/          # Custom skills for Claude Code
├── examples/        # Example CLAUDE.md files demonstrating agent usage
└── configs/         # Configuration files (future)
```

## Available Agents

### Shell Script Agents
Based on the Google Shell Style Guide:

- **shell-writer.md** - Creates new shell scripts following best practices
  - Template-based approach with complete error handling
  - For scripts < 100 lines

- **shell-reviewer.md** - Reviews existing shell scripts for compliance
  - Provides categorized feedback (critical/style/best-practice)
  - Specific line-by-line analysis with examples

- **shell-refactor.md** - Refactors shell scripts to comply with standards
  - Incremental approach preserving functionality
  - Test-driven improvements

### Jenkins Pipeline Agent

- **jenkins-pipeline.md** - Creates and reviews Jenkins declarative pipelines
  - Follows Jenkins best practices and common conventions
  - Complete pipeline template embedded in agent markdown
  - Covers credentials handling, Docker integration, post-build cleanup

## Skills

Custom skills that can be invoked via slash commands:

- **/commit** - Git commit convention helper
- **/nixit** - Generate flake.nix for project dependency management using Nix

## Examples

The `examples/` directory contains example CLAUDE.md files demonstrating how to use agents:

- **jenkins-pipeline-CLAUDE.md** - Example showing how to use the jenkins-pipeline subagent
  - Interactive workflow demonstration
  - Common use cases and tips
  - Sample requests and expected outputs

## Agent Design Pattern

All agents use **embedded templates** - code is included directly in markdown using code blocks.

**Benefits:**
- **Portable** - Agents work from any directory when symlinked to `~/.claude`
- **Self-contained** - No external file dependencies
- **Authoritative** - Complete templates serve as canonical patterns

## Usage

Load any agent markdown file into Claude Code to activate its specialized capabilities. Agents will guide Claude to follow specific practices and patterns for their domain.

## Resources

- [Claude Code Documentation](https://github.com/anthropics/claude-code)
- [Claude Agent SDK](https://github.com/anthropics/claude-agent-sdk)
- [Claude API Documentation](https://docs.anthropic.com/)
