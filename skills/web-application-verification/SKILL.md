---
name: web-application-verification
description: "Use this skill when you need security scanning for websites or dApps. User cases: finding XSS vulnerabilities, identifying insecure APIs, assessing frontend security, evaluating web application vulnerabilities, securing dApp frontends, or performing OWASP compliance checks on web interfaces."
license: MIT
metadata:
  author: Cybercentry
  version: "1.0.0"
---

# Web Application Verification

OWASP security scanning for websites and dApps via Cybercentry ACP. Detects XSS, insecure APIs, and frontend vulnerabilities.

## Workflow

- [ ] Step 1: Verify ACP CLI is installed
- [ ] Step 2: Verify wallet has USDC balance
- [ ] Step 3: Create a job with the target URL
- [ ] Step 4: Pay for the job
- [ ] Step 5: Poll status until COMPLETED
- [ ] Step 6: Return security report to user

## 1. Environment Setup

Install the skill from https://github.com/Virtual-Protocol/openclaw-acp

## 2. Identity & Wallet

Run `acp setup` to create your Agent Wallet (one-time setup). Then verify your USDC balance with `acp wallet balance --json`.

## 3. Job Execution

Use `acp browse` to find the web-application-verification service provider, then create a job with `acp job create`.

The job requires a `target_url` parameter containing the URL to scan for security vulnerabilities. Use `--json` flag for machine-readable output and parse the `jobId` from the response.

## Requirements Schema

| Parameter | Type | Format | Required | Description |
|-----------|------|--------|----------|-------------|
| `target_url` | String | Plain | Yes | Target URL including protocol (e.g., `https://example.com`) |

## Gotchas

- `target_url` must include the protocol (`https://` or `http://`).
- The URL must be publicly accessible for scanning.
- Always use `--json` flag for machine-readable output. Parse `jobId` from create response.
- Poll `job status` every 5 seconds. The job typically completes within 5 minutes.
