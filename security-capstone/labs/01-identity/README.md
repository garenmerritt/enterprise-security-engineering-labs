# Lab 01 – Identity-First Zero Trust & Conditional Access

## Objective
Reduce the risk of account compromise and unauthorized SaaS access by implementing identity-driven Zero Trust controls using conditional access, strong authentication, and modern identity protocols.

## Security Problem
Modern enterprise attacks overwhelmingly target identity rather than network infrastructure. Without strong identity controls, attackers can reuse stolen credentials, abuse OAuth tokens, and bypass perimeter defenses using valid accounts.

## Environment
- Identity Provider: Microsoft Entra ID (Azure AD)
- Users: Employee, Contractor, Privileged Admin
- Devices: Managed Windows VM, Unmanaged personal device
- SaaS Apps: Test SAML and OAuth applications
- Protocols: SAML 2.0, OAuth 2.0, SCIM, WebAuthn
- Tools & Languages: Entra Conditional Access, Microsoft Authenticator

## Implementation Summary
The following controls were implemented:
- Multi-Factor Authentication enforced for all users
- Legacy authentication fully blocked
- Conditional Access policies using user risk, device compliance, and location context
- SAML-based SSO for SaaS applications
- OAuth authorization code flow with scoped permissions
- SCIM provisioning for automated lifecycle management
- WebAuthn-based passwordless authentication

## Threat Model Summary
| Threat | Impact | Likelihood | Notes |
|------|--------|-----------|------|
| Credential phishing | High | High | Primary initial access vector |
| Token replay | High | Medium | OAuth abuse risk |
| Privilege escalation | Critical | Medium | Admin accounts targeted |
| Orphaned accounts | Medium | Low | Lifecycle gaps |

## MITRE ATT&CK Mapping
| Tactic | Technique ID | Technique Name | How This Lab Addresses It |
|------|-------------|---------------|----------------------------|
| Initial Access | T1078 | Valid Accounts | MFA and risk-based conditional access |
| Credential Access | T1110 | Brute Force | MFA + sign-in throttling |
| Defense Evasion | T1556 | Modify Auth Process | Legacy authentication blocked |
| Lateral Movement | T1550 | Use Alternate Auth Material | Token lifetime restrictions |
| Persistence | T1098 | Account Manipulation | SCIM deprovisioning |

## Controls Implemented
| Control | Prevents | Notes |
|------|--------|------|
| MFA for all users | Credential replay | Required for every sign-in |
| Conditional Access | Rogue access | Device + risk signals |
| Legacy auth block | Protocol downgrade | No exceptions |
| OAuth scope control | Token abuse | Least-privilege scopes |
| SCIM provisioning | Orphaned access | Automated removal |
| WebAuthn | Phishing attacks | Passwordless authentication |

## Validation & Testing
- Test Case 1 – Unmanaged Device Access  
  Scenario: User attempts SaaS access from unmanaged device  
  Result: Access blocked due to non-compliant device  

- Test Case 2 – Phished Credentials  
  Scenario: Valid credentials used without MFA  
  Result: MFA challenge enforced, access denied  

- Test Case 3 – Deprovisioned User  
  Scenario: User removed via SCIM  
  Result: SaaS access revoked within minutes  

## Residual Risk
MFA fatigue attacks remain possible but are mitigated through number matching and risk-based prompts. OAuth tokens remain valid until expiration and are mitigated through short token lifetimes and scope restrictions.

## Lessons Learned
- Identity controls are most effective when layered
- OAuth governance is as critical as user authentication
- Automation significantly reduces lifecycle risk
- Passwordless authentication improves both security and user experience
