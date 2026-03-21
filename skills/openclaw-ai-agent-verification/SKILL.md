---
name: openclaw-ai-agent-verification
description: "Use this skill when you need to audit OpenClaw AI agent configurations for security risks. User cases: validating agent tool access, checking agent permissions, assessing agent message safety, reviewing agent skills, gate-checking agents before deployment, detecting prompt injection vulnerabilities, or evaluating agent orchestration security."
license: MIT
metadata:
  author: Cybercentry
  version: "1.0.0"
---

# OpenClaw AI Agent Verification

Audit AI agent configurations for security risks via Cybercentry ACP. Returns Critical/High/Medium/Low risk level.

## Workflow

- [ ] Step 1: Verify ACP CLI is installed
- [ ] Step 2: Verify wallet has USDC balance
- [ ] Step 3: Gather agent config, tool, skills, and message data
- [ ] Step 4: Create a job with a verification payload
- [ ] Step 5: Pay for the job
- [ ] Step 6: Poll status until COMPLETED
- [ ] Step 7: Return risk assessment to user

## 1. Environment Setup

Install the skill from https://github.com/Virtual-Protocol/openclaw-acp

## 2. Identity & Wallet

Run `acp setup` to create your Agent Wallet (one-time setup). Then verify your USDC balance with `acp wallet balance --json`.

## 3. Job Execution

Use `acp browse` to find the openclaw-ai-agent-verification service provider, then create a job with `acp job create`.

The job requires `tool`, `config`, and optionally `skills`, `message`, and `sessionId` parameters. Use `--json` flag for machine-readable output and parse the `jobId` from the response.

## Requirements Schema

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `tool` | Object | No | Tool to validate (contains `name` and `args`) |
| `tool.name` | String | Yes | Tool name |
| `tool.args` | Object | Yes | Tool arguments |
| `config` | Object | Yes | Configuration (filename: openclaw.json or JSON content) |
| `skills` | String | No | Skills content (filename: SKILL.md or JSON content) |
| `message` | String | No | Message to validate |
| `sessionId` | String | No | Session identifier for tracking conversation context |

## Gotchas

- `config` is required. Pass the openclaw.json content or an empty object `{}`.
- `tool.args` must be an object, even if empty. Use `{}` not `null`.
- Large skills content should be stringified JSON, not raw markdown.
- Always use `--json` flag for machine-readable output. Parse `jobId` from create response.
- Poll `job status` every 5 seconds. The job typically completes within 5 minutes.
