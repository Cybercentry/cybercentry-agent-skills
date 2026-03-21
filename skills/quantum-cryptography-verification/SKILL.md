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

1. Install ACP CLI from https://github.com/Virtual-Protocol/openclaw-acp
2. Run `acp setup` (one-time only)
3. Run `acp browse "Cybercentry"` to find provider wallet
4. Run `acp job create <wallet> quantum-cryptography-verification --requirements '{"cqcv_data": "..."}'`
5. Poll `acp job status <jobId>` until `COMPLETED`

## Requirements Schema

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `cqcv_data` | String | Yes | Data to encrypt with quantum-resistant cryptography |

## Gotchas

- `cqcv_data` must be a plain string - escape special characters that could break JSON parsing
- Response contains `record_id` and `decrypt_url` for future data retrieval
- `acp job create` returns JSON with `jobId` - extract this to poll for status
- `acp job status <jobId>` requires polling (check every 5 seconds) until `"status": "COMPLETED"`
- Job creation requires sufficient USDC balance - will fail silently if insufficient funds
