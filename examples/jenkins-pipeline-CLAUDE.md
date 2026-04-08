# Jenkins Pipeline Agent Usage Example

This is an example CLAUDE.md file demonstrating how to use the jenkins-pipeline subagent to create Jenkins declarative pipelines.

## Overview

The `jenkins-pipeline` agent is a specialized subagent that helps create and review Jenkins pipelines following best practices. It uses an interactive workflow to gather requirements before generating the pipeline.

## How to Use the Jenkins Pipeline Agent

When you need to create a Jenkins pipeline, use Claude Code's Task tool to spawn the jenkins-pipeline subagent:

```markdown
I need to create a Jenkins pipeline that [describe your use case]
```

Claude will automatically use the Task tool with `subagent_type: "jenkins-pipeline"` to spawn the specialized agent.

## Example Task: Creating a Python Test Pipeline

**Your request:**
> Create a Jenkins pipeline that runs Python tests using pytest in a Docker container

**What the agent will ask:**

1. **Code Availability:**
   - "Do you already have the code/scripts for this pipeline, or should I create them for you first?"
   - Example answer: `Already have code` or `Please create them for me`

2. **Code/Repository Information:**
   - "What code or application will this pipeline build/test/deploy?"
   - Example answer: `Python app, runs pytest for testing`

3. **Jenkins Agent Label:**
   - "Which Jenkins agent label should this pipeline use?"
   - Example answer: `az-dev`

4. **Docker Image:**
   - "Which Docker image should be used for execution?"
   - Example answer: `docker.io/library/python:3.11`

5. **Pipeline Parameters:**
   - "Will this pipeline have parameters?"
   - If yes, for each parameter:
     - Name: `environment`
     - Type: `choice`
     - Choices: `dev, uat, prod`
     - Description: `Target environment for testing`

6. **Credentials:**
   - "Will this pipeline need Jenkins credentials?"
   - If yes:
     - Credential ID: `github-token`
     - Type: `string`
     - Variable name: `GITHUB_TOKEN`

## What You'll Get

The agent will generate:

1. **Jenkinsfile** - Complete declarative pipeline with:
   - Proper agent configuration
   - All required options (ansiColor, buildDiscarder, timeout, etc.)
   - Parameters block (or commented out if none)
   - Credentials handling (or commented out if none)
   - Docker execution with proper user mapping
   - Post-build cleanup

2. **script.sh** - Shell script to execute inside Docker:
   ```bash
   #!/bin/bash
   set -euo pipefail

   # Run pytest with coverage
   pytest tests/ --cov=src --cov-report=term-missing
   ```

3. **Setup Instructions:**
   - Required Jenkins credentials to configure
   - Agent labels needed
   - Docker images to prepare

## Tips for Using the Agent

### Be Specific About Requirements
The more details you provide upfront, the better the pipeline:
- Mention the programming language/framework
- Specify test commands or deployment steps
- List any required credentials or secrets

### Let the Agent Ask Questions
The interactive workflow ensures all necessary details are captured. Answer each question or say "no" / "skip" for optional items.

### Review Generated Code
The agent follows best practices, but always review:
- Credential IDs match your Jenkins setup
- Docker images are available in your registry (docker.io, etc.)
- Timeout values are appropriate for your use case
- Parameter names and descriptions are clear

## Common Use Cases

### 1. Deployment Pipeline
```
Create a Jenkins pipeline that deploys a Node.js application to Kubernetes
```

The agent will ask about:
- Deployment environment parameters (dev/uat/prod)
- Kubernetes credentials
- Docker image for kubectl/helm commands
- Deployment script details

### 2. Database Migration Pipeline
```
Create a Jenkins pipeline that runs database migrations with approval gates
```

The agent will ask about:
- Database credentials
- Migration tool (Flyway, Liquibase, custom scripts)
- Approval message for production
- Rollback strategy

### 3. Security Scanning Pipeline
```
Create a Jenkins pipeline that runs SAST/DAST security scans
```

The agent will ask about:
- Security scanning tools (SonarQube, Trivy, etc.)
- API credentials for scanning services
- Fail/pass thresholds
- Report artifact handling

## Advanced: Reviewing Existing Pipelines

You can also use the agent to review existing Jenkinsfiles:

```markdown
Review this Jenkins pipeline and suggest improvements:
[paste your existing Jenkinsfile]
```

The agent will check:
- ✅ Compliance with best practices
- ✅ Security best practices for credentials
- ✅ Proper error handling and cleanup
- ✅ Timeout and build retention settings
- ✅ Code style and organization

## Reference

For full details on the agent's capabilities, see:
- Agent definition: `agents/jenkins-pipeline.md`
- Core principles and patterns
- Complete template reference
- Review checklist
