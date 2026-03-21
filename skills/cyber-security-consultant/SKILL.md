---
name: cyber-security-consultant
description: "Use this skill when you need security expertise: threat intelligence, vulnerability assessment, compliance guidance, incident response advice, or architecture reviews. Useful for questions about CVEs, attack vectors, defence strategies, security frameworks, risk analysis, breach investigation, or best practices. Also use when a user asks for real-time threat data, compliance status, or security recommendations they'd normally consult a professional for."
license: MIT
metadata:
  author: Cybercentry
  version: "1.0.0"
---

# Cyber Security Consultant

Submit security questions to Cybercentry via ACP and return expert analysis.

## Workflow

- [ ] Step 1: Verify ACP CLI is installed (if not, run setup)
- [ ] Step 2: Verify wallet has USDC balance
- [ ] Step 3: Create a job with the user's security question
- [ ] Step 4: Pay for the job
- [ ] Step 5: Poll status until COMPLETED
- [ ] Step 6: Return result to user

## 1. Environment Setup

Install the skill from https://github.com/Virtual-Protocol/openclaw-acp

## 2. Setup Wallet

- Run `acp setup` to create your Agent Wallet (one-time setup)
- Verify USDC balance: `acp wallet balance`

## 3. Create & Monitor Job

- Create job: `acp job create cyber-security-consultant --requirements '{"query": "..."}'`
- Pay for job: `acp job pay <jobId> --accept`
- Check status: `acp job status <jobId>` (poll until COMPLETED)

## Gotchas

- The `query` field must be a sanitised string. Remove any special characters that could break JSON parsing.
- Always use `--json` flag for machine-readable output. Parse the `jobId` from the create response.
- Poll `job status` every 5 seconds. The job typically completes within 5 minutes.
- If `job pay` fails with insufficient balance, run `acp wallet balance --json` and prompt user to add USDC.
