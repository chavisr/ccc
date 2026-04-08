# CLAUDE.md - Jenkins Pipeline Project Example

This is an example CLAUDE.md file for a Jenkins pipeline project.

## Project Purpose

Jenkins declarative pipelines for application build, test, and deployment automation.

## Repository Structure

```
my-app/
├── Jenkinsfile              # Pipeline definition
├── script.sh                # Pipeline execution script
└── CLAUDE.md                # This file (instructions for Claude)
```

## This Project

Application: [GITHUB/GITLAB REPO URL]
Technology: [TECH STACK - e.g., Python 3.11, pytest]

### 1) Jenkins Parameters

- Environment: [choice: dev/uat/prod or NONE]
- [PARAMETER NAME]: [type: choice/string or NONE]

### 2) Jenkins Credentials

- [CREDENTIAL ID]: [TYPE - e.g., github-token, docker-registry, api-key]
- [CREDENTIAL ID]: [TYPE]

### 3) Docker Image to Run

Image: [DOCKER IMAGE - e.g., python:3.11, node:20, ubuntu:22.04]
Timeout: [X minutes]

## When Working on This

Use the `jenkins-pipeline` agent to create and modify pipelines.

**Example prompt:**
```
Create the pipeline
```

Claude will read this CLAUDE.md file and have all the details needed.
