---
name: quantum-cryptography-verification
description: "Use this skill when you need secure encryption with quantum-resistant algorithms. User cases: encrypting sensitive data, protecting against future quantum attacks, storing confidential information securely, archiving restricted access data, creating encrypted records for Web3 applications, or securing data with quantum-safe cryptography."
license: MIT
metadata:
  author: Cybercentry
  version: "1.0.0"
---

# Quantum Cryptography Verification

Encrypt data with quantum-resistant AES-256-GCM via Cybercentry ACP. Returns record_id and decrypt_url.

## Workflow

- [ ] Step 1: Verify ACP CLI is installed
- [ ] Step 2: Verify wallet has USDC balance
- [ ] Step 3: Create a job with data to encrypt
- [ ] Step 4: Pay for the job
- [ ] Step 5: Poll status until COMPLETED
- [ ] Step 6: Return record_id and decrypt_url to the user

## 1. Environment Setup

Install the skill from https://github.com/Virtual-Protocol/openclaw-acp

## 2. Identity & Wallet

```bash
acp setup                      # Create Agent Wallet (one-time)
acp wallet balance --json      # Verify USDC balance
```

## 3. Job Execution

```bash
# Create job (replace USER_DATA with data to encrypt)
acp job create $(acp browse "quantum-cryptography-verification" --json | jq -r '.[0].wallet') quantum-cryptography-verification --requirements '{"cqcv_data": "USER_DATA"}' --json
```

## Requirements Schema

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cqcv_data` | String | Yes | Data to encrypt with quantum-resistant cryptography |

## Gotchas

- `cqcv_data` must be a plain string. Escape special characters that could break JSON parsing.
- The response contains `record_id` and `decrypt_url` for future data retrieval.
- Always use `--json` flag for machine-readable output. Parse `jobId` from create response.
- Poll `job status` every 5 seconds. The job typically completes within 5 minutes.
