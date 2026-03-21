---
name: private-data-verification
description: "Use this skill when you need Zero-Knowledge Proofs or data integrity validation. User cases: verifying identity claims without exposure, proving login status, creating trustless proof of action, validating sensitive data authenticity, privacy-preserving verification in Web3, or generating cryptographic proof receipts."
license: MIT
metadata:
  author: Cybercentry
  version: "1.0.0"
---

# Private Data Verification

Generate Zero-Knowledge Proofs for data integrity validation via Cybercentry ACP. Returns proof_id and proof_url.

## Workflow

- [ ] Step 1: Verify ACP CLI is installed
- [ ] Step 2: Verify wallet has USDC balance
- [ ] Step 3: Create a job with private data
- [ ] Step 4: Pay for the job
- [ ] Step 5: Poll status until COMPLETED
- [ ] Step 6: Return proof_id and proof_url to the user

## 1. Environment Setup

Install the skill from https://github.com/Virtual-Protocol/openclaw-acp

## 2. Setup

- `acp setup` (one-time only)

## 3. Create Job

- `acp job create private-data-verification --requirements '{"cpdv_data": "..."}'`
- `acp job status <jobId>`  # Poll until status shows result

## Requirements Schema

| Parameter | Type | Format | Required |
|-----------|------|--------|----------|
| `cpdv_data` | String | Plain | Yes |

## Gotchas

- `cpdv_data` must be a plain string - escape special characters that could break JSON parsing
- Response contains `proof_id` and `proof_url` for verification retrieval
- `acp job create` returns JSON with `jobId` - extract this to poll for status
- `acp job status <jobId>` requires polling (check every 5 seconds) until `"status": "COMPLETED"`
- Job creation requires sufficient USDC balance - will fail silently if insufficient funds
