# Enterprise Hybrid Identity Infrastructure

## Novatech solutions - Microsoft Entra ID Implementation

A hybrid identity solution for a fictional 30-employee retail enterprise with offices in New York, London, and Singapore. This project demonstrates real-world implementation of Microsoft Entra ID, identity management aligned with NIST security frameworks.

---

## Project Overview

This project simulates an enterprise identity infrastructure deployment, covering the full spectrum of hybrid identity management from on-premises Active Directory through cloud synchronization and external collaboration.

**Scenario:** Novatech Solutions is expanding globally and needs a unified identity platform that enables secure access to cloud resources while maintaining their existing Active Directory investment.

### Business Requirements Addressed

- Centralized identity management across three geographic regions
- Delegated administration with regional autonomy (GDPR compliance for EU)
- Secure collaboration with external partners and vendors
- Single sign-on experience for end users
- Automated user lifecycle management
- Comprehensive audit and monitoring capabilities

---

## Architecture

```
┌────────────────────────────────────────────────────────────────────┐
│                      MICROSOFT ENTRA ID                            │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐                │
│  │ AU-NewYork  │  │ AU-London   │  │AU-Singapore │                │
│  │  15 users   │  │  8 users   │  │  7 users   │                │
│  └─────────────┘  └─────────────┘  └─────────────┘                │
│                                                                    │
│  Custom Roles: HelpDesk T1 | HelpDesk T2 | Security Analyst       │
│  External: PartnerCorp (SAML Federation) | Cross-Tenant Sync      │
└────────────────────────────┬───────────────────────────────────────┘
                             │
              ┌──────────────┴──────────────┐
              │                             │
              ▼                             ▼
     ┌─────────────────┐          ┌─────────────────┐
     │  Entra Connect  │          │   Cloud Sync    │
     │  • PHS          │          │  • Pilot OU     │
     │  • Seamless SSO │          │                 │
     └────────┬────────┘          └────────┬────────┘
              │                             │
              └──────────────┬──────────────┘
                             │
┌────────────────────────────▼───────────────────────────────────────┐
│                  ON-PREMISES ACTIVE DIRECTORY                      │
│                DC01-NYC (merchandisevault.local)                   │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐                   │
│  │OU:NewYork  │  │OU:London   │  │OU:Singapore│                   │
│  └────────────┘  └────────────┘  └────────────┘                   │
└────────────────────────────────────────────────────────────────────┘
```

---

## Technologies Implemented

| Component | Technology | Purpose |
|-----------|------------|---------|
| Cloud Identity | Microsoft Entra ID | Primary identity provider for cloud resources |
| On-Premises Directory | Windows Server 2022 AD DS | Source of truth for user identities |
| Hybrid Sync | Microsoft Entra Connect | Password hash sync + Seamless SSO |
| Pilot Sync | Microsoft Entra Cloud Sync | Lightweight agent-based synchronization |
| Monitoring | Entra Connect Health | Sync monitoring and alerting |

---

## Features Demonstrated

### Identity Management
- [x] Custom Microsoft Entra roles with least-privilege permissions
- [x] Administrative Units for geographic delegation
- [x] Bulk user provisioning with PowerShell automation
- [x] Dynamic group membership based on user attributes
- [x] License assignment automation by department

### Hybrid Identity
- [x] Password Hash Synchronization (PHS)
- [x] Seamless Single Sign-On for domain-joined devices
- [x] OU-based sync filtering (exclude service accounts)
- [x] UPN suffix routing for cloud authentication
- [x] Parallel Cloud Sync pilot deployment

### External Collaboration
- [x] B2B collaboration with domain restrictions
- [x] Cross-tenant access policies with MFA trust
- [x] Cross-tenant user synchronization
- [x] SAML identity provider federation

### Security & Compliance
- [x] NIST SP 800-63 aligned authentication
- [x] NIST SP 800-207 Zero Trust principles
- [x] Inactive user detection and reporting
- [x] Comprehensive audit logging
- [x] Role-based access control (RBAC)

---

## Screenshots
### Active Directory On-prem Organizational unit Structure
<img width="1024" height="768" alt="VirtualBox_DC01-NYC_12_12_2025_12_32_57" src="https://github.com/user-attachments/assets/82cb716e-58f7-4d53-a829-4413356879bf" />

### Tenant Configuration
<img width="3420" height="2214" alt="image" src="https://github.com/user-attachments/assets/17002a71-b026-44ce-837c-1375f7305930" />
Overview of tenant

---

#### Company Branding
<img width="1710" height="1107" alt="Screenshot 2025-12-16 at 3 12 59 PM" src="https://github.com/user-attachments/assets/7b63862f-e786-4a75-b963-4ad59480a7af" />

*Custom sign-in page with The Merchandise Vault branding*

---

#### Custom Domain Verification
<img width="3420" height="2214" alt="image" src="https://github.com/user-attachments/assets/cfe0ff00-32e2-44ab-b60d-61e4546898bc" />

*Verified custom domain configuration*

---

### Administrative Structure

#### Administrative Units
<img width="1710" height="1107" alt="Screenshot 2025-12-15 at 8 56 31 PM" src="https://github.com/user-attachments/assets/bdc5457f-a813-4c66-bf1e-dcfb86507956" />

*Geographic administrative units for delegated management*

---

#### Custom Roles
<img width="1710" height="1107" alt="Screenshot 2025-12-17 at 4 14 22 PM" src="https://github.com/user-attachments/assets/2df6819e-1cca-4705-a216-f87fe74f439b" />

*Least-privilege role definitions for Help Desk tiers*

#### Role Assignments
<img width="3420" height="2214" alt="image" src="https://github.com/user-attachments/assets/146fb7e9-ffd2-4719-a229-3c2f0f8a0f9f" />


---

### Hybrid Identity

#### Entra Connect Configuration

<img width="1710" height="1107" alt="Screenshot 2025-12-17 at 11 09 27 AM" src="https://github.com/user-attachments/assets/c675031f-4800-4e15-9b7f-25b2760f000e" />

*Synchronization configuration with OU filtering*

---

### External Collaboration

#### Cross-Tenant Access Settings
<img width="1710" height="1107" alt="Screenshot 2025-12-17 at 8 07 54 PM" src="https://github.com/user-attachments/assets/4ef361fa-8230-42a5-ac78-3e5eb1cef2e0" />

*Partner organization trust configuration*

#### External Collaboration Settings
<img width="1710" height="1107" alt="Screenshot 2025-12-17 at 4 43 54 PM" src="https://github.com/user-attachments/assets/eff33ee9-4326-446b-8057-aec6dee205c0" />

*B2B collaboration restrictions and allowed domains*

---

## Key Design Decisions

### Why Password Hash Synchronization?

| Factor | PHS | Pass-Through Auth | AD FS |
|--------|-----|-------------------|-------|
| Cloud resilience | ✓ High | ✗ Requires on-prem | ✗ Requires on-prem |
| Identity Protection | ✓ Full support | ✗ Limited | ✗ Limited |
| Operational complexity | ✓ Low | Medium | High |
| Leaked credential detection | ✓ Yes | ✗ No | ✗ No |

**Decision:** PHS selected for resilience and security feature enablement.

### Why Administrative Units?

- **GDPR Compliance:** London user data managed by EU-based administrators
- **Blast Radius:** Compromised regional admin can't affect other regions
- **Operational Efficiency:** Regional teams handle local user management

### Why Custom Roles?

Built-in roles are either too broad (User Administrator) or too narrow (Password Administrator). Custom roles provide:

- **Tier 1:** Password reset only—safe for junior help desk
- **Tier 2:** Full user management without role assignment capability
- **Security Analyst:** Read-only audit access—separation of duties

---

## NIST Framework Alignment

| NIST Document | Implementation |
|---------------|----------------|
| SP 800-63A (Identity Proofing) | Structured enrollment via OU-based provisioning |
| SP 800-63B (Authentication) | PHS with double-hashing meets memorized secret requirements |
| SP 800-63C (Federation) | Cross-tenant trust implements FAL2 assertions |
| SP 800-207 (Zero Trust) | Least-privilege roles, device trust, continuous verification |

---

## Getting Started

### Prerequisites

- Windows Server 2022 (VM or physical)
- Microsoft 365 E3/E5 license or Entra ID P1/P2 trial
- PowerShell 7.x with Microsoft Graph module
- Domain registered for custom domain verification

---

## Skills Demonstrated

This project showcases proficiency in:

- **Microsoft Entra ID** administration and configuration
- **Hybrid Identity** design and implementation
- **Security Architecture** aligned with NIST frameworks
- **Technical Documentation** for enterprise environments
- **Troubleshooting** identity synchronization issues

---

## Certification Alignment

This project covers objectives from:

- **SC-300: Microsoft Identity and Access Administrator**
  - Implement and manage user identities (20-25%)
  - Implement authentication and access management (25-30%)
  - Plan and implement workload identities (20-25%)
  
---

## Resources

- [Microsoft Entra Documentation](https://learn.microsoft.com/en-us/entra/)
- [NIST SP 800-63 Digital Identity Guidelines](https://pages.nist.gov/800-63-3/)
- [NIST SP 800-207 Zero Trust Architecture](https://csrc.nist.gov/publications/detail/sp/800-207/final)

---

## Author

**[Nadia Kroduah]**

Aspiring Identity and Access Management Professional

- Currently pursuing SC-300 certification
- Active Security Clearance
- CompTIA A+ | CompTIA Network+

[LinkedIn](www.linkedin.com/in/nadia-kroduah) 
---

## License

This project is for educational and portfolio demonstration purposes. Scripts and documentation may be freely used and adapted for learning.

---

*Last Updated: [December 2025]
