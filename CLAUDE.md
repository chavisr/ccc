# CLAUDE.md

Personal repository for Claude Code agents, skills, and configurations. Not a software project — no build/test commands.

## Agents

| Agent | Use for |
|-------|---------|
| `shell-writer` | Writing new shell scripts (< 100 lines, Google Shell Style Guide) |
| `shell-reviewer` | Reviewing shell scripts for compliance |
| `shell-refactor` | Refactoring shell scripts while preserving functionality |
| `jenkins-pipeline` | Creating/reviewing Jenkins declarative pipelines |
| `marp-slides` | Creating Marp presentations (technical or non-technical) |
| `kube-manifest` | Creating K8s manifests with Kustomize (base/dev/staging/production) |
| `readme-writer` | Generating README.md by analyzing project structure and tech stack |
| `dockerfile` | Writing optimized, multi-stage Dockerfiles with .dockerignore |
| `gitlab-ci` | Creating GitLab CI/CD pipelines (.gitlab-ci.yml) |

## Skills

| Skill | Use for |
|-------|---------|
| `/commit` | Conventional commit messages |
| `/nixit` | Generate flake.nix for project dependencies |

## Agent Standards

All agents must:
- **Dual mode**: Support both interactive (ask questions) and context-driven (read CLAUDE.md) modes. Use interactive only when CLAUDE.md lacks details.
- **Embedded templates**: Include code directly in markdown for portability
- **Self-contained**: No external file dependencies

## Usage

Symlink agents and skills into your Claude Code config directory:

```bash
# Agents
ln -s /path/to/ccc/agents/*.md ~/.claude/agents/

# Skills
ln -s /path/to/ccc/skills/* ~/.claude/skills/
```

Then agents are available as subagents and skills as slash commands in any project.

## Git

Default branch: `main`
