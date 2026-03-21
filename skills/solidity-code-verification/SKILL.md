---
name: solidity-code-verification
description: "Use this skill when you need security analysis of Solidity smart contract code. User cases: auditing Solidity contracts, identifying re-entrancy bugs, detecting access control issues, reviewing unsafe external calls, evaluating code before deployment, gate-checking contracts in transaction pipelines, or performing security assessments."
license: MIT
metadata:
  author: Cybercentry
  version: "1.0.0"
---

# Solidity Code Verification

Analyse Solidity code for vulnerabilities via Cybercentry ACP. Returns High/Medium/Low/Informational risk level.

## Workflow

- [ ] Step 1: Verify ACP CLI is installed
- [ ] Step 2: Verify wallet has USDC balance
- [ ] Step 3: Create a job with Solidity code
- [ ] Step 4: Pay for the job
- [ ] Step 5: Poll status until COMPLETED (typically < 2 minutes)
- [ ] Step 6: Return risk assessment to the user

## 1. Environment Setup

Install the skill from https://github.com/Virtual-Protocol/openclaw-acp

## 2. Identity & Wallet

```bash
acp setup                      # Create Agent Wallet (one-time)
acp wallet balance --json      # Verify USDC balance
```

## 3. Job Execution

```bash
# Create job (replace SOLIDITY_CODE with actual code)
acp job create $(acp browse "solidity-code-verification" --json | jq -r '.[0].wallet') solidity-code-verification --requirements '{"solidity_code": "SOLIDITY_CODE"}' --json
```

## Requirements Schema

| Parameter | Type | Format | Required | Description |
|-----------|------|--------|----------|-------------|
| `solidity_code` | String | Plain | Yes | Solidity source code to analyze |

## Gotchas

- Escape double quotes and newlines in the Solidity code for valid JSON.
- For multi-file contracts, concatenate all files into a single string.
- Execution time averages under 5 minutes. Poll every 10 seconds for this job.
- Always use `--json` flag for machine-readable output. Parse `jobId` from create response.
