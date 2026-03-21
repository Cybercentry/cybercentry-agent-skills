# Cybercentry Agent Skills

A comprehensive collection of security and verification skills for AI agents integrating with the Cybercentry platform via the Virtuals Protocol ACP (Agent Commerce Protocol) CLI.

## Overview

This repository contains 9 specialized skills designed to provide AI agents with access to advanced security analysis, blockchain forensics, code verification, and cryptographic services. All skills are executed through the Cybercentry ACP infrastructure and follow a consistent job-based workflow pattern.

## Quick Start

1. Install ACP CLI: `git clone https://github.com/Virtual-Protocol/openclaw-acp && cd openclaw-acp && npm install && npm link`
2. Run `acp setup` (one-time only)
3. For any skill, run `acp browse "Cybercentry"` to find the provider wallet
4. Create a job with skill-specific requirements
5. Poll `acp job status <jobId>` until `COMPLETED`

Each skill's SKILL.md contains the specific workflow and requirements.

## Skills

| Skill | Purpose | Documentation |
|-------|---------|-----------------|
| Cyber Security Consultant | General security expertise and threat analysis | `/skills/cyber-security-consultant/SKILL.md` |
| Ethereum Token Verification | EVM token contract security analysis | `/skills/ethereum-token-verification/SKILL.md` |
| OpenClaw AI Agent Verification | Audit AI agent configurations for security | `/skills/openclaw-ai-agent-verification/SKILL.md` |
| Private Data Verification | Zero-Knowledge Proofs for data integrity | `/skills/private-data-verification/SKILL.md` |
| Quantum Cryptography Verification | Quantum-resistant encryption | `/skills/quantum-cryptography-verification/SKILL.md` |
| Solana Token Verification | Solana token contract security analysis | `/skills/solana-token-verification/SKILL.md` |
| Solidity Code Verification | Solidity smart contract security analysis | `/skills/solidity-code-verification/SKILL.md` |
| Wallet Verification | Blockchain forensics and wallet risk assessment | `/skills/wallet-verification/SKILL.md` |
| Web Application Verification | OWASP security scanning for websites and dApps | `/skills/web-application-verification/SKILL.md` |

### 3. OpenClaw AI Agent Verification

**Purpose**: Audit AI agent configurations for security risks with Critical/High/Medium/Low assessment

**When to Use**:
- Validate agent tool access
- Check agent permissions
- Assess agent message safety
- Review agent skills
- Gate-check agents before deployment
- Detect prompt injection vulnerabilities
- Evaluate agent orchestration security

**Requirements**:
```json
{
  "tool": {
    "name": "tool_name",
    "args": {}
  },
  "config": {},
  "skills": "SKILL.md content or JSON",
  "message": "Message to validate",
  "sessionId": "session_id"
}
```

**Required Fields**:
- `tool.name` (string)
- `tool.args` (object, can be empty `{}`)
- `config` (object, can be empty `{}`)

**Optional Fields**:
- `skills` - Skills content for validation
- `message` - Message content to validate
- `sessionId` - Conversation context tracking

**Setup**: `/skills/openclaw-ai-agent-verification/SKILL.md`

---

### 4. Private Data Verification

**Purpose**: Zero-Knowledge Proofs for data integrity validation

**When to Use**:
- Verify identity claims without exposure
- Prove login status
- Create trustless proof of action
- Validate sensitive data authenticity
- Privacy-preserving verification in Web3
- Generate cryptographic proof receipts

**Requirements**:
```json
{
  "cpdv_data": "Your private data here"
}
```

**Response**: Returns `proof_id` and `proof_url` for verification retrieval

**Setup**: `/skills/private-data-verification/SKILL.md`

---

### 5. Quantum Cryptography Verification

**Purpose**: Quantum-resistant AES-256-GCM encryption for sensitive data

**When to Use**:
- Encrypt sensitive data
- Protect against future quantum attacks
- Store confidential information securely
- Archive restricted access data
- Create encrypted records for Web3
- Secure data with quantum-safe cryptography

**Requirements**:
```json
{
  "cqcv_data": "Data to encrypt"
}
```

**Response**: Returns `record_id` and `decrypt_url` for future data retrieval

**Encryption**: AES-256-GCM (quantum-resistant algorithm)

**Setup**: `/skills/quantum-cryptography-verification/SKILL.md`

---

### 6. Solana Token Verification

**Purpose**: Solana token contract security analysis with Rust Scan AI detection

**When to Use**:
- Verify Solana token legitimacy
- Scan for rug pulls
- Detect hidden taxes
- Assess liquidity risks
- Analyze holder distribution
- Gate-check tokens in automated pipelines

**Requirements**:
```json
{
  "contract_address": "Gx5dX1pM5aCQn8wtXEmEHSUia3W57Jq7qdu7kKsHvirt"
}
```

**Address Format**: Base58-encoded (32-44 characters, no `0x` prefix)

**Setup**: `/skills/solana-token-verification/SKILL.md`

---

### 7. Solidity Code Verification

**Purpose**: Security analysis of Solidity smart contracts with High/Medium/Low/Informational risk levels

**When to Use**:
- Audit Solidity contracts before deployment
- Identify re-entrancy bugs
- Detect access control issues
- Review unsafe external calls
- Gate-check contracts in transaction pipelines
- Perform security assessments

**Requirements**:
```json
{
  "solidity_code": "contract MyContract { ... }"
}
```

**Typical Execution Time**: < 2 minutes

**Setup**: `/skills/solidity-code-verification/SKILL.md`

---

### 8. Wallet Verification

**Purpose**: Blockchain forensics and wallet risk assessment across 30+ EVM chains

**When to Use**:
- Investigate wallet funding sources
- Sanctions compliance screening
- Detect money laundering patterns
- Identify bot automation
- Assess wallet trustworthiness
- Evaluate counterparty risk

**Requirements**:
```json
{
  "wallet_address": "0x1234567890abcdef..."
}
```

**Supported Networks**: 30+ EVM chains including Ethereum, BSC, Polygon, Avalanche, Arbitrum, Optimism, Sonic, and more

**Setup**: `/skills/wallet-verification/SKILL.md`

---

### 9. Web Application Verification

**Purpose**: OWASP security scanning for websites and dApps with XSS and API vulnerability detection

**When to Use**:
- Find XSS vulnerabilities
- Identify insecure APIs
- Assess frontend security
- Evaluate web application vulnerabilities
- Secure dApp frontends
- Perform OWASP compliance checks

**Requirements**:
```json
{
  "target_url": "https://example.com"
}
```

**Important**: URL must include protocol (`https://` or `http://`) and be publicly accessible

**Setup**: `/skills/web-application-verification/SKILL.md`

---

## Common Integration Pattern

```bash
# 1. Create Job
JOB_ID=$(acp job create 0x228F7097fB812828a2F08EE29bAC0c58f9e0Bb63 <skill-name> --requirements '<json-payload>' --json | jq -r '.jobId')

# 2. Pay for Job
acp job pay $JOB_ID --accept true --json

# 3. Poll Until Complete
while true; do
  STATUS=$(acp job status $JOB_ID --json | jq -r '.status')
  if [ "$STATUS" = "COMPLETED" ]; then
    acp job status $JOB_ID --json | jq '.result'
    break
  fi
  sleep 5
done
```

## Global Requirements

**Agent Wallet Address** (Fixed): `0x228F7097fB812828a2F08EE29bAC0c58f9e0Bb63`

**Common Gotchas** (across all skills):
- Always use `--json` flag for machine-readable output
- Parse `jobId` from the create job response
- Use the fixed wallet address - do not use `acp browse`
- Escape special characters in string values for valid JSON
- Numbers (chain_id, platform_id) should not be quoted in JSON
- Poll every 5 seconds for job status updates
- Most jobs complete within 30 seconds

## License

All skills are licensed under MIT. See individual SKILL.md files for details.

## Author

Cybercentry - Advanced Security & Verification Infrastructure

## Repository Structure

```
cybercentry-agent-skills/
├── LICENSE.md
├── README.md
└── skills/
    ├── cyber-security-consultant/
    │   ├── evals/
    │   │   └── evals.json
    │   └── SKILL.md
    ├── ethereum-token-verification/
    │   ├── evals/
    │   │   └── evals.json
    │   └── SKILL.md
    ├── openclaw-ai-agent-verification/
    │   ├── evals/
    │   │   └── evals.json
    │   └── SKILL.md
    ├── private-data-verification/
    │   ├── evals/
    │   │   └── evals.json
    │   └── SKILL.md
    ├── quantum-cryptography-verification/
    │   ├── evals/
    │   │   └── evals.json
    │   └── SKILL.md
    ├── solana-token-verification/
    │   ├── evals/
    │   │   └── evals.json
    │   └── SKILL.md
    ├── solidity-code-verification/
    │   ├── evals/
    │   │   └── evals.json
    │   └── SKILL.md
    ├── wallet-verification/
    │   ├── evals/
    │   │   └── evals.json
    │   └── SKILL.md
    └── web-application-verification/
        ├── evals/
        │   └── evals.json
        └── SKILL.md
```

## Getting Started

1. Choose a skill from the directory above
2. Read the corresponding `SKILL.md` file for detailed documentation
3. Follow the "General Job Workflow" pattern
4. Replace placeholders with your actual data
5. Parse JSON responses for results

---

For more information, visit individual skill documentation files in the `/skills` directory.
