# Lab 02 – Endpoint Security & Device Trust Enforcement

## Objective
Reduce the risk of compromised or non-compliant endpoints accessing corporate resources by implementing continuous device trust evaluation and automated remediation tied to identity-based access controls.

This lab extends Zero Trust principles by treating endpoint posture as a dynamic signal rather than a static trust decision.

## Security Problem
Endpoints are a primary execution and persistence vector for attackers. Without strong endpoint posture enforcement, attackers can:
- Execute malicious code on user devices
- Disable security tooling
- Access corporate resources from compromised endpoints using valid credentials

This lab mitigates these risks by enforcing device compliance and integrating endpoint signals into access decisions.

## Environment
- Identity Provider: Microsoft Entra ID (Azure AD)
- Endpoint Platform: Windows 10/11 VM
- Endpoint Management: Microsoft Intune
- EDR: Microsoft Defender for Endpoint
- Devices:
  - Managed corporate Windows device
  - Unmanaged personal device
- Tools & Languages:
  - Python
  - PowerShell
  - Microsoft Graph API

## Implementation Summary
The following controls were implemented:
- Device compliance policies enforcing:
  - Disk encryption (BitLocker)
  - OS version and patch level
  - Secure boot and TPM presence
- Endpoint risk signals collected via EDR
- Conditional Access policies requiring compliant devices
- Automated risk evaluation using scripting
- Access restriction triggered for non-compliant or high-risk devices

Endpoint trust is continuously evaluated and directly influences identity-based access decisions.

## Threat Model Summary

| Threat | Impact | Likelihood | Notes |
|------|--------|-----------|------|
| Malicious code execution | High | High | Common initial execution vector |
| Disabled endpoint protections | High | Medium | Defense evasion |
| Compromised endpoint access | Critical | Medium | Valid credentials abused |
| Persistence via startup artifacts | High | Medium | Often missed without EDR |

## MITRE ATT&CK Mapping

| Tactic | Technique ID | Technique Name | How This Lab Addresses It |
|------|-------------|---------------|----------------------------|
| Execution | T1059 | Command and Scripting Interpreter | EDR visibility and enforcement |
| Defense Evasion | T1562 | Impair Defenses | Compliance checks detect disabled protections |
| Persistence | T1547 | Boot or Logon Autostart Execution | Endpoint monitoring |
| Initial Access | T1078 | Valid Accounts | Device compliance required for access |

## Controls Implemented

| Control | Prevents | Notes |
|------|--------|------|
| Device compliance policies | Rogue or outdated devices | Enforced via Intune |
| Disk encryption enforcement | Offline data access | BitLocker required |
| EDR integration | Undetected execution | Defender for Endpoint |
| Conditional Access | Compromised endpoint access | Identity + device posture |
| Automated remediation | Delayed response | Script-driven enforcement |

## Validation & Testing

- Test Case 1 – Unencrypted Device  
  Scenario: Device without disk encryption attempts SaaS access  
  Result: Access blocked due to non-compliance  

- Test Case 2 – Disabled Endpoint Protection  
  Scenario: Defender disabled on managed device  
  Result: Device marked non-compliant, access restricted  

- Test Case 3 – Automated Risk Evaluation  
  Scenario: Endpoint flagged high-risk by script  
  Result: Conditional Access policy enforced within minutes  

## Residual Risk
Zero-day malware and fileless attacks remain possible but are mitigated through:
- Continuous endpoint monitoring
- Rapid access revocation
- Layered identity-based enforcement

## Lessons Learned
- Endpoint trust must be continuously evaluated, not assumed
- Identity controls are significantly stronger when combined with device posture
- Automation reduces response time and human error
- Endpoint security is a prerequisite for Zero Trust, not an add-on
