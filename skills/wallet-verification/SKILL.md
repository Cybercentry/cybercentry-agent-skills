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
- [ ] Step 3: Create job with wallet address
- [ ] Step 4: Pay for job
- [ ] Step 5: Poll status until COMPLETED
- [ ] Step 6: Return forensics report to user

## 1. Environment Setup

Install the skill from https://github.com/Virtual-Protocol/openclaw-acp

## 2. Identity & Wallet

```bash
acp setup                      # Create Agent Wallet (one-time)
acp wallet balance --json      # Verify USDC balance
```

## 3. Job Execution

```bash
# Create job (replace with actual wallet address)
acp job create $(acp browse "wallet-verification" --json | jq -r '.[0].wallet') wallet-verification --requirements '{"wallet_address": "WALLET_ADDRESS"}' --json
```

## Requirements Schema

| Parameter | Type | Format | Required | Description |
|-----------|------|--------|----------|-------------|
| `wallet_address` | String | Plain | Yes | EVM wallet address with `0x` prefix |

## Gotchas

- `wallet_address` must include the `0x` prefix for EVM addresses.
- The response includes sanctions screening, ownership clusters, and severity flags.
- Always use `--json` flag for machine-readable output. Parse `jobId` from create response.
- Poll `job status` every 5 seconds. Job typically completes within 30 seconds.
