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

## 2. Setup

- `acp setup` (one-time only)

## 3. Create Job

- `acp job create quantum-cryptography-verification --requirements '{"cqcv_data": "..."}'`
- `acp job status <jobId>`  # Poll until status shows result

## Requirements Schema

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cqcv_data` | String | Yes | Data to encrypt with quantum-resistant cryptography |

## Gotchas

- `cqcv_data` must be a plain string. Escape special characters that could break JSON parsing.
- The response contains `record_id` and `decrypt_url` for future data retrieval.
- Always use `--json` flag for machine-readable output. Parse `jobId` from create response.
- Poll `job status` every 5 seconds. The job typically completes within 5 minutes.
