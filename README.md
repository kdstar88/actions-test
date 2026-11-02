# DevSecOps Security Lab – GitHub Actions

**Hands-on CI/CD Security | GitHub Actions | Workflow Hardening | Security Automation**

## Overview

This repository documents my practical learning journey in DevSecOps and CI/CD pipeline security as part of my Cybersecurity Analyst training at CyberSteps.

The purpose of this lab is to explore how automated workflows operate, identify common security risks, simulate vulnerabilities in a controlled environment, and implement measures to strengthen pipeline security.

Rather than focusing only on successful workflow execution, these exercises demonstrate how security can be integrated directly into the development and automation process.

## Lab Environment

| Component | Technology |
|---|---|
| Source Control | Git & GitHub |
| CI/CD Automation | GitHub Actions |
| Workflow Configuration | YAML |
| Command Execution | Bash / Shell |
| Development Environment | Azure Cloud Shell |
| Security Focus | DevSecOps, Secure Automation, Workflow Hardening |

## Implemented Security Labs

### 1. CI/CD Workflow Fundamentals – Heartbeat

**Workflow:** `heartbeat.yml`

Created and executed a basic GitHub Actions workflow to understand how automated pipelines operate.

Key learnings:
- Understanding workflow triggers, jobs, steps, and runners
- Writing YAML-based automation configurations
- Using Git commands to commit and push workflow changes
- Monitoring execution status and troubleshooting workflow logs

### 2. Secrets Handling and Masking

**Workflow:** `secret_test.yml`

Explored how GitHub Actions handles sensitive information during workflow execution.

Key learnings:
- Understanding GitHub Actions secrets
- Examining secret masking in workflow logs
- Recognizing the risks of exposing credentials in CI/CD pipelines
- Learning why secrets require secure storage and careful handling

### 3. Forbidden File Security Gate

**Workflow:** `Security_gate.yml`

Implemented a security gate to demonstrate how automated checks can detect and reject files that violate a defined repository security rule.

Key learnings:
- Applying security rules through automated workflows
- Understanding pass/fail conditions in CI/CD
- Detecting prohibited files before they become part of a trusted development process
- Interpreting failed security checks and workflow logs

### 4. Command Injection – The Injection Lockdown

**Workflow:** `injection_test.yml`

Demonstrated a command injection vulnerability caused by inserting untrusted GitHub Issue titles directly into shell commands.

**Vulnerable implementation:**

```yaml
run: |
  echo "New issue title is: ${{ github.event.issue.title }}"
```

An attacker-controlled Issue title was able to introduce an additional shell command into the workflow.

**Secure implementation:**

```yaml
env:
  ISSUE_TITLE: ${{ github.event.issue.title }}
run: |
  echo "New issue title is: $ISSUE_TITLE"
```

After applying the fix, the malicious input was treated as data rather than executable shell code.

Key learnings:
- Understanding command injection vulnerabilities
- Recognizing untrusted input in GitHub Actions
- Separating data from executable shell commands
- Using environment variables to prevent direct expression injection
- Validating security fixes through repeated testing

## Security Concepts Explored

- **CI/CD Security:** Protecting automated development and delivery workflows.
- **Shift-Left Security:** Introducing security checks earlier in the development lifecycle.
- **Least Privilege:** Limiting workflow permissions to what is necessary.
- **Secrets Management:** Reducing the risk of credential exposure.
- **Command Injection Prevention:** Preventing untrusted input from being interpreted as executable code.
- **Security Gates:** Using automated checks to enforce defined security requirements.

## Key Takeaways

These exercises helped me understand that CI/CD pipelines are not just automation tools. They are also important security boundaries.

A pipeline can execute commands, access credentials, and interact with development infrastructure. Misconfigured workflows or untrusted input can therefore introduce serious security risks.

My main learning is that effective DevSecOps requires more than detecting vulnerabilities. It involves understanding how they occur, implementing appropriate safeguards, and verifying that those safeguards work as intended.

## Learning Context

These labs were completed as part of my ongoing Cybersecurity Analyst training at **CyberSteps**, with a focus on cloud security, security automation, and DevSecOps fundamentals.

This repository is a learning environment and does not represent a production-ready security framework.

## Disclaimer

All vulnerability demonstrations are intended for educational purposes within a controlled test repository. The examples should not be deployed to production environments without appropriate security review and hardening.
