# Enterprise Hybrid Identity Infrastructure

## The Merchandise Vault - Microsoft Entra ID Implementation

A complete hybrid identity solution for a fictional 100-employee retail enterprise with offices in New York, London, and Singapore. This project demonstrates real-world implementation of Microsoft Entra ID (formerly Azure AD) identity management aligned with NIST security frameworks.

---

## Project Overview

This project simulates an enterprise identity infrastructure deployment, covering the full spectrum of hybrid identity management from on-premises Active Directory through cloud synchronization and external collaboration.

**Scenario:** The Merchandise Vault is expanding globally and needs a unified identity platform that enables secure access to cloud resources while maintaining their existing Active Directory investment.

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
│  │  50 users   │  │  30 users   │  │  20 users   │                │
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
| Automation | PowerShell + Microsoft Graph | Bulk operations and reporting |

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

## Repository Structure

```
├── README.md
├── docs/
│   ├── implementation-guide.md      # Step-by-step deployment guide
│   ├── design-decisions.md          # Architecture rationale + NIST alignment
│   └── troubleshooting-runbook.md   # Common issues and resolutions
├── scripts/
│   ├── environment-setup/
│   │   ├── Install-ADForest.ps1     # AD DS deployment
│   │   ├── New-OUStructure.ps1      # Organizational unit creation
│   │   └── New-SampleUsers.ps1      # Test user population
│   ├── entra-config/
│   │   ├── New-CustomRoles.ps1      # Custom role definitions
│   │   ├── New-AdminUnits.ps1       # Administrative unit setup
│   │   └── Set-TenantSettings.ps1   # Tenant configuration
│   ├── automation/
│   │   ├── New-BulkUsers.ps1        # Bulk user creation from CSV
│   │   ├── Set-LicensesByDept.ps1   # Automated license assignment
│   │   └── Get-GroupAudit.ps1       # Group membership audit
│   └── reports/
│       ├── Get-LicenseUtilization.ps1
│       ├── Get-InactiveUsers.ps1
│       └── Get-EffectivePermissions.ps1
├── templates/
│   ├── user-import-template.csv     # CSV template for bulk imports
│   └── custom-roles.json            # Role definition exports
└── screenshots/
    └── [see Screenshots section below]
```

---

## Screenshots

### Tenant Configuration

#### Company Branding
![Company Branding](screenshots/company-branding.png)
*Custom sign-in page with The Merchandise Vault branding*

#### Custom Domain Verification
![Custom Domain](screenshots/custom-domain.png)
*Verified custom domain configuration*

---

### Administrative Structure

#### Administrative Units
![Administrative Units](screenshots/admin-units.png)
*Geographic administrative units for delegated management*

#### Custom Roles
![Custom Roles](screenshots/custom-roles.png)
*Least-privilege role definitions for Help Desk tiers*

#### Role Assignments
![Role Assignments](screenshots/role-assignments.png)
*Scoped role assignments to administrative units*

---

### Hybrid Identity

#### Entra Connect Configuration
![Entra Connect](screenshots/entra-connect-config.png)
*Synchronization configuration with OU filtering*

#### Sync Status Dashboard
![Sync Status](screenshots/sync-status.png)
*Microsoft Entra Connect Health monitoring*

#### Seamless SSO Configuration
![Seamless SSO](screenshots/seamless-sso.png)
*Kerberos-based single sign-on setup*

---

### External Collaboration

#### Cross-Tenant Access Settings
![Cross-Tenant Access](screenshots/cross-tenant-access.png)
*Partner organization trust configuration*

#### External Collaboration Settings
![External Collab](screenshots/external-collab-settings.png)
*B2B collaboration restrictions and allowed domains*

---

### Automation & Reporting

#### PowerShell Bulk Operations
![Bulk Operations](screenshots/powershell-bulk-ops.png)
*Automated user creation script execution*

#### License Utilization Report
![License Report](screenshots/license-report.png)
*Weekly license utilization dashboard*

#### Connect Health Alerts
![Health Alerts](screenshots/connect-health-alerts.png)
*Proactive monitoring and alerting configuration*

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

### Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/enterprise-hybrid-identity.git
   ```

2. **Set up on-premises environment**
   ```powershell
   # Run from elevated PowerShell on Windows Server
   .\scripts\environment-setup\Install-ADForest.ps1
   .\scripts\environment-setup\New-OUStructure.ps1
   .\scripts\environment-setup\New-SampleUsers.ps1
   ```

3. **Configure Entra ID tenant**
   ```powershell
   # Connect to Microsoft Graph
   Connect-MgGraph -Scopes "Directory.ReadWrite.All"
   
   .\scripts\entra-config\Set-TenantSettings.ps1
   .\scripts\entra-config\New-AdminUnits.ps1
   .\scripts\entra-config\New-CustomRoles.ps1
   ```

4. **Install Entra Connect**
   - Download from Microsoft
   - Follow implementation guide in `/docs/implementation-guide.md`

---

## Skills Demonstrated

This project showcases proficiency in:

- **Microsoft Entra ID** administration and configuration
- **Hybrid Identity** design and implementation
- **PowerShell** automation with Microsoft Graph API
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
  
- **AZ-104: Microsoft Azure Administrator**
  - Manage Azure identities and governance (20-25%)

---

## Resources

- [Microsoft Entra Documentation](https://learn.microsoft.com/en-us/entra/)
- [NIST SP 800-63 Digital Identity Guidelines](https://pages.nist.gov/800-63-3/)
- [NIST SP 800-207 Zero Trust Architecture](https://csrc.nist.gov/publications/detail/sp/800-207/final)
- [Microsoft Graph PowerShell SDK](https://learn.microsoft.com/en-us/powershell/microsoftgraph/)

---

## Author

**[Nadia Kroduah]**

Aspiring Identity and Access Management Professional

- Currently pursuing SC-300 certification
- Active Security Clearance
- CompTIA A+ | CompTIA Network+

[LinkedIn](www.linkedin.com/in/nadia-kroduah) | [Email](nadiakrodua20@gmail.com)

---

## License

This project is for educational and portfolio demonstration purposes. Scripts and documentation may be freely used and adapted for learning.

---

*Last Updated: [December 2025*
