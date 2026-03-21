---
name: wallet-verification
description: "Use this skill when you need blockchain forensics for wallet addresses. User cases: investigating wallet funding sources, screening sanctions compliance, detecting money laundering patterns, identifying bot automation, assessing wallet trustworthiness, evaluating counterparty risk, or gate-checking wallets in automated systems."
license: MIT
metadata:
  author: Cybercentry
  version: "1.0.0"
---

# Wallet Verification

Blockchain forensics for wallet addresses via Cybercentry ACP. Traces funding chains across 30+ EVM chains.

## Workflow

- [ ] Step 1: Verify ACP CLI is installed
- [ ] Step 2: Verify wallet has USDC balance
- [ ] Step 3: Create a job with a wallet address
- [ ] Step 4: Pay for the job
- [ ] Step 5: Poll status until COMPLETED
- [ ] Step 6: Return forensics report to user

## 1. Environment Setup

Install the skill from https://github.com/Virtual-Protocol/openclaw-acp

## 2. Setup Wallet

- Run `acp setup` to create your Agent Wallet (one-time setup)
- Verify USDC balance: `acp wallet balance`

## 3. Create & Monitor Job

- Create job: `acp job create wallet-verification --requirements '{"wallet_address": "0x..."}'`
- Pay for job: `acp job pay <jobId> --accept`
- Check status: `acp job status <jobId>` (poll until COMPLETED)

## Requirements Schema

| Parameter | Type | Format | Required | Description |
|-----------|------|--------|----------|-------------|
| `wallet_address` | String | Plain | Yes | EVM wallet address with `0x` prefix |

## Gotchas

- `wallet_address` must include the `0x` prefix for EVM addresses.
- The response includes sanctions screening, ownership clusters, and severity flags.
- Always use `--json` flag for machine-readable output. Parse `jobId` from create response.
- Poll `job status` every 5 seconds. The job typically completes within 5 minutes.
