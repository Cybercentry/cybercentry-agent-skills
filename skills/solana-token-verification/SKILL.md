---
name: solana-token-verification
description: "Use this skill when you need to verify Solana token contracts for security. User cases: checking Solana token legitimacy, scanning for rug pulls, detecting hidden taxes, assessing liquidity risks, analysing holder distribution, evaluating tokens before investment, or gate-checking Solana tokens in automated pipelines."
license: MIT
metadata:
  author: Cybercentry
  version: "1.0.0"
---

# Solana Token Verification

Verify Solana token contracts for security risks via Cybercentry ACP with Rust Scan AI detection.

## Workflow

- [ ] Step 1: Verify ACP CLI is installed
- [ ] Step 2: Verify wallet has USDC balance
- [ ] Step 3: Create a job with the Solana contract address
- [ ] Step 4: Pay for the job
- [ ] Step 5: Poll status until COMPLETED
- [ ] Step 6: Return risk assessment to the user

## 1. Environment Setup

Install the skill from https://github.com/Virtual-Protocol/openclaw-acp

## 2. Setup

- `acp setup` (one-time only)

## 3. Create Job

- `acp job create solana-token-verification --requirements '{"contract_address": "..."}'`
- `acp job status <jobId>`  # Poll until status shows result

## Requirements Schema

| Parameter | Type | Format | Required | Description |
|-----------|------|--------|----------|-------------|
| `contract_address` | String | Plain | Yes | Solana contract address (e.g., `Gx5dX1pM5aCQn8wtXEmEHSUia3W57Jq7qdu7kKsHvirt`) |

## Gotchas

- Solana addresses are base58-encoded, not hex - do not add `0x` prefix
- Address is typically 32-44 characters long
- `acp job create` returns JSON with `jobId` - extract this to poll for status
- `acp job status <jobId>` requires polling (check every 5 seconds) until `"status": "COMPLETED"`
- Job creation requires sufficient USDC balance - will fail silently if insufficient funds
