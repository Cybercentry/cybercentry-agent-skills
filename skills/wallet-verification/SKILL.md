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

## 2. Setup

- `acp setup` (one-time only)

## 3. Create Job

- `acp job create wallet-verification --requirements '{"wallet_address": "0x..."}'`
- `acp job status <jobId>`  # Poll until status shows result

## Requirements Schema

| Parameter | Type | Format | Required | Description |
|-----------|------|--------|----------|-------------|
| `wallet_address` | String | Plain | Yes | EVM wallet address with `0x` prefix |

## Gotchas

- `wallet_address` must include the `0x` prefix for EVM addresses
- `acp job create` returns JSON with `jobId` - extract this to poll for status
- `acp job status <jobId>` requires polling (check every 5 seconds) until `"status": "COMPLETED"`
- Job creation requires sufficient USDC balance in your wallet - will fail silently if insufficient funds
