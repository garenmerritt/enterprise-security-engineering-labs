# Zero Trust Security Engineering Capstone

## Overview
This repository contains a progressive security engineering capstone focused on designing and implementing a **prevention-first Zero Trust architecture** for a modern, SaaS-first enterprise.

The goal of this project is to demonstrate:
- Technical credibility across identity, endpoint, data, mobile, and SaaS security
- Practical use of security automation (Python & PowerShell)
- Real-world application of IAM protocols (SAML, OAuth, SCIM, WebAuthn)
- Threat modeling and mitigation using MITRE ATT&CK

## Enterprise Scenario
- Remote-first workforce
- BYOD + managed devices
- SaaS-heavy environment
- Cloud-native identity provider

## Architecture Principles
- Identity is the new control plane
- Never trust, always verify
- Prevention over detection
- Least privilege everywhere
- Automation for scale

## Repository Structure
security-capstone/

├── docs/
│ ├── architecture/
│ ├── threat-models/
│ └── decisions/

├── labs/
│ ├── 01-identity/
│ ├── 02-endpoint/
│ ├── 03-data/
│ ├── 04-mdm/
│ ├── 05-saas/
│ └── 06-automation/

├── scripts/
│ ├── python/
│ └── powershell/
└── README.md


## Threat Modeling & MITRE ATT&CK
Each lab includes:
- Threat scenarios
- ATT&CK technique mapping
- Preventative controls and residual risk

## Disclaimer
This project uses test tenants and simulated data only. No production systems or real user data are involved.
