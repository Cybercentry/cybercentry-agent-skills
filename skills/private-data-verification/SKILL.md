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

## 2. Identity & Wallet

Run `acp setup` to create your Agent Wallet (one-time setup). Then verify your USDC balance with `acp wallet balance --json`.

## 3. Job Execution

Use `acp browse` to find the private-data-verification service provider, then create a job with `acp job create`.

The job requires a `cpdv_data` parameter containing the private data to generate a proof for. Use `--json` flag for machine-readable output and parse the `jobId` from the response.

## Requirements Schema

| Parameter | Type | Format | Required |
|-----------|------|--------|----------|
| `cpdv_data` | String | Plain | Yes |

## Gotchas

- `cpdv_data` must be a plain string. Escape special characters that could break JSON parsing.
- The response contains `proof_id` and `proof_url` for verification retrieval.
- Always use `--json` flag for machine-readable output. Parse `jobId` from create response.
- Poll `job status` every 5 seconds. The job typically completes within 5 minutes.
