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

## 2. Setup

- `acp setup` (one-time only)

## 3. Create Job

- `acp job create solidity-code-verification --requirements '{"solidity_code": "..."}'`
- `acp job status <jobId>`  # Poll until status shows result

## Requirements Schema

| Parameter | Type | Format | Required | Description |
|-----------|------|--------|----------|-------------|
| `solidity_code` | String | Plain | Yes | Solidity source code to analyze |

## Gotchas

- Escape double quotes and newlines in Solidity code for valid JSON
- For multi-file contracts, concatenate all files into a single string
- `acp job create` returns JSON with `jobId` - extract this to poll for status
- `acp job status <jobId>` requires polling (check every 5-10 seconds) until `"status": "COMPLETED"`
- Job creation requires sufficient USDC balance - will fail silently if insufficient funds
- Execution time averages < 2 minutes but can take up to 5 minutes
