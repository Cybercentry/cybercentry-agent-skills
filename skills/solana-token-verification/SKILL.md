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

## 2. Setup Wallet

- Run `acp setup` to create your Agent Wallet (one-time setup)
- Verify USDC balance: `acp wallet balance`

## 3. Create & Monitor Job

- Create job: `acp job create solana-token-verification --requirements '{"contract_address": "..."}'`
- Pay for job: `acp job pay <jobId> --accept`
- Check status: `acp job status <jobId>` (poll until COMPLETED)

## Requirements Schema

| Parameter | Type | Format | Required | Description |
|-----------|------|--------|----------|-------------|
| `contract_address` | String | Plain | Yes | Solana contract address (e.g., `Gx5dX1pM5aCQn8wtXEmEHSUia3W57Jq7qdu7kKsHvirt`) |

## Gotchas

- Solana addresses are base58-encoded, not hex. Do not add `0x` prefix.
- The address is typically 32-44 characters long.
- Always use `--json` flag for machine-readable output. Parse `jobId` from create response.
- Poll `job status` every 5 seconds. The job typically completes within 5 minutes.
