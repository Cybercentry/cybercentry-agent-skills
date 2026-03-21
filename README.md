# Cybercentry Agent Skills

A comprehensive collection of security and verification skills for AI agents integrating with the Cybercentry platform via the Virtuals Protocol ACP (Agent Commerce Protocol) CLI.

## Overview

This repository contains 9 specialized skills designed to provide AI agents with access to advanced security analysis, blockchain forensics, code verification, and cryptographic services. All skills are executed through the Cybercentry ACP infrastructure and follow a consistent job-based workflow pattern.

## Quick Start

1. Install ACP CLI: `git clone https://github.com/Virtual-Protocol/openclaw-acp && cd openclaw-acp && npm install && npm link`
2. Run `acp setup` (one-time only)
3. Run `acp browse "Cybercentry"` to find the provider wallet address
4. Run `acp job create <wallet> <skill-name> --requirements '{"param": "value"}'` with skill-specific parameters
5. Poll `acp job status <jobId>` until status is `COMPLETED`

Each skill's SKILL.md contains the exact workflow and required parameters.

## Skills

| # | Skill | Purpose | Documentation |
|---|-------|---------|-----------------|
| 1 | Cyber Security Consultant | General security expertise and threat analysis | `/skills/cyber-security-consultant/SKILL.md` |
| 2 | Ethereum Token Verification | EVM token contract security analysis | `/skills/ethereum-token-verification/SKILL.md` |
| 3 | OpenClaw AI Agent Verification | Audit AI agent configurations for security | `/skills/openclaw-ai-agent-verification/SKILL.md` |
| 4 | Private Data Verification | Zero-Knowledge Proofs for data integrity | `/skills/private-data-verification/SKILL.md` |
| 5 | Quantum Cryptography Verification | Quantum-resistant encryption | `/skills/quantum-cryptography-verification/SKILL.md` |
| 6 | Solana Token Verification | Solana token contract security analysis | `/skills/solana-token-verification/SKILL.md` |
| 7 | Solidity Code Verification | Solidity smart contract security analysis | `/skills/solidity-code-verification/SKILL.md` |
| 8 | Wallet Verification | Blockchain forensics and wallet risk assessment | `/skills/wallet-verification/SKILL.md` |
| 9 | Web Application Verification | OWASP security scanning for websites and dApps | `/skills/web-application-verification/SKILL.md` |

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

## License

All skills are licensed under MIT. See individual SKILL.md files for details.

## Author

Cybercentry - Advanced Security & Verification Infrastructure

For more information, visit individual skill documentation files in the `/skills` directory.
