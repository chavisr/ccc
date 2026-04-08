# Jenkins Pipeline Agent Usage Example

This is an example CLAUDE.md file demonstrating how to use the jenkins-pipeline subagent to create Jenkins declarative pipelines.

## Before You Start

Before asking Claude to create a Jenkins pipeline, ensure your Jenkins setup is ready:

- [ ] Jenkins server is installed and running
- [ ] At least one Jenkins agent/node is configured (or plan to use controller)
- [ ] Docker is available on the agent(s) where pipeline will run
- [ ] Required Jenkins plugins installed: Pipeline, Docker, AnsiColor (if using color output)
- [ ] Jenkins credentials already configured (GitHub tokens, API keys, etc.) or list what you need to create
- [ ] Target Docker registry access configured (docker.io, private registry, etc.)
- [ ] Have the application/code repository URL ready
- [ ] Know the technology stack (Python, Node.js, Java, etc.)

## Overview

The `jenkins-pipeline` agent is a specialized subagent that helps create and review Jenkins pipelines following best practices. It generates:
- **Jenkinsfile** - Complete declarative pipeline with proper configuration
- **script.sh** - Executable shell script for pipeline stages
- **Setup instructions** - Credentials and configuration needed

## How to Use the Jenkins Pipeline Agent

Tell Claude exactly what you want the pipeline to do:

**Basic syntax:**
```
Create a Jenkins pipeline that [ACTION] for [TECHNOLOGY STACK].
- Application/code: [DESCRIBE]
- Target environment(s): [dev/uat/prod]
- Required credentials: [LIST CREDENTIAL NAMES YOU'VE ALREADY SET UP]
- Any special requirements: [TIMEOUTS, APPROVAL GATES, etc.]
```

Claude will ask clarifying questions and generate the complete pipeline.

## Step-by-Step Workflow

**Step 1: Understand Your Requirements**
- What does the pipeline need to do? (build, test, deploy, scan, migrate, etc.)
- What technology/language? (Python, Node.js, Java, Go, etc.)
- Where does code live? (GitHub URL, GitLab, BitBucket, etc.)
- Target environments? (dev, uat, prod, or single environment)
- What credentials does it need? (GitHub token, Docker registry, deployment creds, etc.)

**Step 2: Set Up Jenkins Prerequisites**
- Ensure credentials are created in Jenkins first (don't create them in pipeline)
- Note the credential IDs you've already created
- Verify agent is configured and available
- Check Docker access from agent(s)

**Step 3: Create Pipeline with Claude**
Ask Claude with specific details (see "Common Tasks" section below).

Claude will ask:
- **Code/application details** - What repo, branch, build/test commands
- **Execution environment** - Docker image, agent label to use
- **Parameters** (optional) - Environment choice, version input, etc.
- **Credentials** (optional) - Which Jenkins credentials to pass to pipeline
- **Pipeline features** - Approval gates, notifications, retry logic, timeouts
- **Post-build actions** - Cleanup, artifact handling, notifications

**Step 4: Review Generated Files**
Claude will create:
- **Jenkinsfile** - Place in root of your Git repository
- **script.sh** - Place in repository root or in a `ci/` directory
- **Setup instructions** - List of credentials to configure in Jenkins

**Step 5: Configure Jenkins**
1. Add Jenkinsfile path to Jenkins pipeline job
2. Create any missing credentials (GitHub tokens, API keys, etc.)
3. Test pipeline with a manual trigger
4. Set up webhook (GitHub/GitLab) for automatic triggers

## Claude's Responsibilities

When Claude creates Jenkins pipelines:

1. **Confirm execution environment** - Ask for agent label and Docker image (or confirm controller node)
2. **Validate credentials needed** - Ask which Jenkins credentials exist and which need to be created
3. **Generate Jenkinsfile** - Include:
   - Declarative syntax only
   - Agent configuration with proper Docker setup
   - Options block: ansiColor, buildDiscarder, disableConcurrentBuilds, timeout, timestamps
   - Parameters block (if needed) with clear descriptions
   - Stages: Checkout, Build, Test, (Deploy/Release if applicable), Cleanup
   - Post block with proper cleanup and notifications
4. **Generate script.sh** - Executable shell script following Google Shell Style Guide:
   - Proper shebang and error handling (`set -euo pipefail`)
   - Inline comments explaining each section
   - Proper credential handling via exported environment variables
5. **Create setup instructions** - List of:
   - Jenkins credentials to create (with type and description)
   - Agent labels needed
   - Docker images to verify availability
   - Environment variables expected
   - Any plugins that might be needed
6. **Provide repository structure guidance** - Where to place Jenkinsfile and script.sh
7. **Handle credentials securely** - Never hardcode secrets, always use Jenkins credentials and `withCredentials`

## What You'll Get

1. **Jenkinsfile** - Complete declarative pipeline ready to commit to Git
2. **script.sh** - Shell script for pipeline stages (executable and portable)
3. **Setup instructions** - Exact credentials and configuration needed in Jenkins

## Common Tasks

### 1. Create a Python Testing Pipeline
```
Create a Jenkins pipeline that runs Python tests using pytest.
- Application: Python repo at https://github.com/myorg/python-app
- Technology: Python 3.11 with pytest
- Required credentials: github-token (already created in Jenkins)
- Run: pytest tests/ with coverage reports
- Target environments: dev only
- Timeout: 10 minutes
```

Claude will ask:
- Docker image: `python:3.11`
- Agent label: `linux-docker` (or controller)
- Parameters: None needed
- Additional credentials: None

### 2. Create a Node.js Build & Deploy Pipeline
```
Create a Jenkins pipeline that builds and deploys a Node.js app to Kubernetes.
- Application: Node.js repo at https://github.com/myorg/node-service
- Technology: Node.js 20, npm, Docker
- Required credentials: github-token, docker-registry, kubernetes-config
- Build: npm install && npm run build
- Deploy to: dev, uat, prod (environment parameter)
- Timeout: 15 minutes
```

Claude will ask:
- Docker image for build: `node:20`
- Docker image for deployment: `bitnami/kubectl:latest`
- Approval gate for production: Yes
- Agent label: `kubernetes-enabled`

### 3. Create a Database Migration Pipeline
```
Create a Jenkins pipeline that runs database migrations with approval gates.
- Application: Database migration scripts at https://github.com/myorg/db-migrations
- Technology: Flyway, PostgreSQL
- Required credentials: db-prod-creds, db-uat-creds, db-dev-creds
- Migrations directory: ./migrations
- Target: dev, uat, prod (parameter)
- Approval gate for prod: Yes, with message "Approve production migration"
- Timeout: 20 minutes
```

Claude will ask:
- Docker image: `flyway/flyway:latest`
- Rollback strategy: (agent will suggest options)
- Notification on failure: (email, Slack, etc.)

### 4. Create a Security Scanning Pipeline
```
Create a Jenkins pipeline that runs security scans on code.
- Application: https://github.com/myorg/backend-app
- Technology: SonarQube SAST scan
- Required credentials: sonarqube-token
- Scan directory: ./src
- Fail if quality gate fails: Yes
- Timeout: 30 minutes
```

Claude will ask:
- SonarQube server URL: (already configured)
- Docker image: `sonarsource/sonarqube:latest` or use SonarQube server
- Report artifacts: yes
- Notification on failure: yes

## Tips for Using the Agent

**Be Specific:**
- Provide repository URL
- List technology stack (language, frameworks, tools)
- Mention existing Jenkins credentials by ID
- Specify environments (dev, uat, prod)
- Note timeout requirements

**Let Claude Ask:**
The interactive workflow captures all necessary details. Answer each question completely or say "none" / "not needed" for optional items.

**Review Generated Code:**
Always check:
- Credential IDs match your Jenkins setup exactly
- Docker images are accessible from your agent(s)
- Timeout values are realistic for your workloads
- Stage names and descriptions are clear
- script.sh has proper error handling

## Repository Structure

When Claude generates pipeline files, place them in your Git repository:

```
my-app/
├── Jenkinsfile              # Pipeline definition (root of repo)
├── ci/
│   └── script.sh            # Or place script.sh here
├── src/                      # Application code
├── tests/                    # Test files
├── .gitignore               # Should exclude .env, secrets files
└── README.md                # Include build/deploy instructions
```

**Important:**
- Jenkinsfile must be in repository root (unless configured otherwise in Jenkins job)
- script.sh should be executable: `chmod +x ci/script.sh`
- Both files should be version controlled in Git
- Never commit secrets or credentials files

## Credentials Setup Checklist

Before Claude creates the pipeline, create required credentials in Jenkins:

**Steps to create credentials in Jenkins:**
1. Go to Jenkins → Manage Jenkins → Manage Credentials
2. Click on appropriate credential store (usually "Jenkins" store)
3. Click "Add Credentials" (left sidebar)
4. For each credential type:

**GitHub Token (secret text):**
- Kind: Secret text
- Scope: Global
- Secret: (paste your GitHub PAT)
- ID: `github-token`
- Description: GitHub personal access token

**Docker Registry (username/password):**
- Kind: Username with password
- Scope: Global
- Username: (docker username)
- Password: (docker token)
- ID: `docker-registry`
- Description: Docker registry credentials

**API Key (secret text):**
- Kind: Secret text
- Scope: Global
- Secret: (your API key)
- ID: `sonarqube-token` (or similar)
- Description: SonarQube token

**Kubernetes Config (secret file):**
- Kind: Secret file
- Scope: Global
- File: (kubeconfig file content)
- ID: `kubernetes-config`
- Description: Kubernetes cluster config

## Troubleshooting Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| **Build fails: "credential not found"** | Credential ID in pipeline doesn't match Jenkins | Verify credential IDs in Jenkins match pipeline, use exact IDs |
| **Build fails: "Docker image not found"** | Docker image unavailable on agent | Check agent has Docker access, pull image manually: `docker pull <image>` |
| **Build fails: agent offline** | Agent node is down or disconnected | Check Jenkins agent status, verify agent label in pipeline matches configured label |
| **Build hangs during checkout** | Git credentials missing or SSH key issues | Verify github-token credential exists, check agent SSH keys are configured |
| **script.sh permission denied** | Script not executable | Run: `chmod +x ci/script.sh` and commit with executable bit |
| **Credentials leak in logs** | Sensitive data exposed in console output | Use `withCredentials` in pipeline (Claude handles this automatically) |
| **Post cleanup fails** | Workspace cleanup permission issues | Ensure agent user has write permissions to workspace |
| **Docker: cannot connect to daemon** | Agent doesn't have Docker installed/running | Install Docker on agent, ensure agent user is in docker group: `usermod -aG docker $USER` |
| **Pipeline timeout** | Timeout value too short for actual workload | Increase timeout in pipeline options, review stage durations in console logs |

## Advanced: Reviewing Existing Pipelines

You can ask Claude to review and improve your existing Jenkinsfile:

```
Review this Jenkins pipeline and suggest improvements:

[paste your Jenkinsfile here]

Focus on: security, error handling, and maintainability
```

Claude will check:
- Compliance with declarative pipeline best practices
- Security (credentials handling, secret management)
- Error handling and cleanup
- Timeout and retry settings
- Build retention and artifact management
- Code organization and readability
