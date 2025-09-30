# Stanna Compliance Documentation

**Last Updated**: January 2025

---

## Compliance Overview

Stanna is committed to meeting the highest standards of security and compliance. This document provides information about our compliance programs, certifications, and audit results.

---

## Current Compliance Status

### ✅ GDPR (General Data Protection Regulation)
**Status**: Fully Compliant
**Effective Date**: May 2024
**Scope**: All EU and EEA data processing

**Key Implementations**:
- Data Processing Agreements available
- Privacy by Design principles
- Right to access, rectification, erasure
- Data portability supported
- Breach notification procedures (72 hours)
- Data Protection Impact Assessment completed

**Documentation Available**:
- [Privacy Policy](./privacy-policy.md)
- [Data Processing Agreement](./dpa.md)
- Cookie Policy
- GDPR Compliance Statement

### ✅ CCPA (California Consumer Privacy Act)
**Status**: Fully Compliant
**Effective Date**: May 2024
**Scope**: California residents' data

**Key Implementations**:
- Consumer rights respected (know, delete, opt-out)
- Privacy policy disclosure
- "Do Not Sell My Info" option (we don't sell data)
- 45-day response time to requests
- Non-discrimination policy

**Consumer Rights Portal**: privacy.gostanna.com

### 🔄 SOC 2 Type II
**Status**: In Progress
**Expected Completion**: Q2 2025
**Audit Firm**: [To be announced]

**Trust Service Criteria**:
- Security (CC6.x, CC7.x)
- Availability (A1.x)
- Confidentiality (C1.x)
- Processing Integrity (PI1.x)
- Privacy (P1.x - optional)

**Audit Period**: 6 months minimum
**Report Available**: Upon request with NDA

### 📋 ISO 27001
**Status**: Planned
**Target Date**: Q3 2025
**Scope**: Information Security Management System (ISMS)

**Implementation Status**:
- Risk assessment: Complete
- Security policies: In development
- Control implementation: 75% complete
- Internal audit: Scheduled Q2 2025
- Management review: Ongoing

---

## Industry-Specific Compliance

### Healthcare (HIPAA)
**Status**: Not Currently Certified

Stanna is designed with HIPAA-compliant architecture:
- ✅ Encryption in transit and at rest
- ✅ Access controls and audit logs
- ✅ Business Associate Agreements available
- ⏳ Full HIPAA compliance: Q4 2025

**Note**: If you need to process Protected Health Information (PHI), please contact compliance@gostanna.com for our Healthcare offering.

### Financial Services
**Frameworks Supported**:
- PCI DSS Level 1 (infrastructure provider)
- SOX controls (for public company customers)
- GLBA (Gramm-Leach-Bliley Act)

**Note**: Stanna does not directly handle credit card data or financial transactions.

### Federal (FedRAMP, FISMA)
**Status**: Not Currently Authorized

We're evaluating FedRAMP authorization for Q4 2025. Current government customers use our standard enterprise tier with enhanced security controls.

---

## Data Protection & Privacy

### Data Residency

**Current Regions**:
- 🇺🇸 United States (Primary)
- 🇪🇺 European Union (Available for Enterprise)

**Coming Soon**:
- 🇬🇧 United Kingdom (Q3 2025)
- 🇸🇬 Singapore / APAC (Q4 2025)
- 🇦🇺 Australia (Q4 2025)

**Data Localization**:
- Data stored in customer's chosen region
- Cross-border data transfer uses SCCs
- Regional redundancy within selected region

### Privacy Shield & Standard Contractual Clauses

**EU-US Data Transfers**:
- Standard Contractual Clauses (SCCs) 2021 version
- Transfer Impact Assessment completed
- Additional safeguards implemented
- Data Processing Agreement includes SCCs

**UK Data Transfers**:
- UK International Data Transfer Agreement (IDTA)
- UK Addendum to EU SCCs
- ICO registration: [Registration number]

### Data Subject Rights

**GDPR Rights** (EU/EEA residents):
- Right to access (Article 15)
- Right to rectification (Article 16)
- Right to erasure / "Right to be forgotten" (Article 17)
- Right to restriction of processing (Article 18)
- Right to data portability (Article 20)
- Right to object (Article 21)

**CCPA Rights** (California residents):
- Right to know
- Right to delete
- Right to opt-out of sale (we don't sell data)
- Right to non-discrimination

**Request Process**:
1. Submit request via privacy.gostanna.com
2. Identity verification (2-factor)
3. Response within 30 days (GDPR) or 45 days (CCPA)
4. Data delivered in machine-readable format

---

## Security Certifications

### Infrastructure

Our cloud infrastructure provider maintains:
- ✅ SOC 2 Type II
- ✅ ISO 27001
- ✅ PCI DSS Level 1
- ✅ FedRAMP (infrastructure only)
- ✅ HIPAA eligible
- ✅ C5 (Germany)
- ✅ MTCS (Singapore)

### Third-Party Assessments

**Penetration Testing**:
- Frequency: Quarterly
- Provider: [Security firm name]
- Last Test: [Date]
- Next Test: [Date]
- Report: Available upon request with NDA

**Vulnerability Scanning**:
- Frequency: Continuous
- Tools: Automated SAST/DAST
- Last Scan: [Real-time]
- Findings: Tracked and remediated per SLA

**Bug Bounty Program**:
- Status: Launching Q2 2025
- Platform: TBD
- Scope: All production services
- Rewards: $100 - $10,000 USD

---

## Audit Reports & Documentation

### Available Documentation

**Security**:
- Security Overview (this document)
- Security Whitepaper
- Penetration Test Summary
- Vulnerability Disclosure Policy
- Incident Response Plan

**Privacy**:
- Privacy Policy
- Cookie Policy
- Data Processing Agreement (DPA)
- Standard Contractual Clauses
- Subprocessor List

**Compliance**:
- SOC 2 Report (when available)
- ISO 27001 Certificate (when available)
- Compliance Questionnaires (various frameworks)
- Vendor Security Assessment

### How to Request Documentation

**For Existing Customers**:
- Available in dashboard: Settings → Security & Compliance
- Email: compliance@gostanna.com

**For Prospects**:
- Contact: sales@gostanna.com
- Security questionnaire: security@gostanna.com
- NDA required for detailed reports

**Typical Turnaround**:
- Standard documents: Immediate (self-service)
- Audit reports: 2-3 business days (NDA required)
- Custom questionnaires: 5-7 business days

---

## Subprocessors & Third Parties

### Subprocessor List

| Subprocessor | Purpose | Data Processed | Location | Security |
|--------------|---------|----------------|----------|----------|
| Google Cloud | Authentication | Email addresses | Global | SOC 2, ISO 27001 |
| [Cloud Provider] | Infrastructure | All application data | US/EU | SOC 2, ISO 27001 |
| Groq | AI inference | Client data (encrypted) | US | Enterprise security |
| Resend | Email delivery | Email addresses | US | GDPR compliant |
| [Monitoring] | Observability | Logs (PII redacted) | US | SOC 2 |

**Subprocessor Changes**:
- 30-day advance notice for new subprocessors
- Email notification to compliance contacts
- Right to object to new subprocessors
- Updated list: help.gostanna.com/subprocessors

### Subprocessor Agreements

All subprocessors have signed:
- ✅ Data Processing Agreements
- ✅ Confidentiality agreements
- ✅ Security requirements acceptance
- ✅ Breach notification obligations
- ✅ Audit rights provisions

---

## Compliance Programs

### Information Security Management

**ISMS Framework**: Based on ISO 27001
- Policy management
- Risk assessment and treatment
- Asset management
- Access control
- Cryptography
- Physical security
- Operations security
- Communications security
- System development security
- Supplier relationships
- Incident management
- Business continuity
- Compliance

**Review Cycle**:
- Policies: Annual review
- Controls: Quarterly assessment
- Risk assessment: Semi-annual
- Management review: Quarterly
- Internal audit: Annual

### Security Awareness Training

**Employee Training**:
- Security fundamentals: Onboarding
- Phishing awareness: Quarterly
- Data protection: Annual
- Incident response: Annual
- Role-specific training: As needed

**Compliance Rate**: 100% (required)
**Last Training**: [Date]
**Next Training**: [Date]

### Vendor Risk Management

**Vendor Assessment Process**:
1. Initial security questionnaire
2. Evidence review (certifications, reports)
3. Risk scoring and classification
4. DPA execution
5. Ongoing monitoring
6. Annual reassessment

**Vendor Risk Tiers**:
- **Critical**: Quarterly reviews, on-site audits
- **High**: Semi-annual reviews
- **Medium**: Annual reviews
- **Low**: Biennial reviews

---

## Industry Standards & Frameworks

### Alignment with Standards

| Standard | Status | Alignment % | Gap Analysis |
|----------|--------|-------------|--------------|
| CIS Controls v8 | Implemented | 95% | Minor gaps in logging |
| NIST CSF | Implemented | 90% | Advancing to Tier 3 |
| NIST 800-53 | Partial | 75% | Federal controls planned |
| PCI DSS | N/A | - | No card data handled |
| COBIT | Reference | 70% | Governance framework |

### Framework Mapping

Available framework mappings:
- ✅ SOC 2 to GDPR
- ✅ ISO 27001 to NIST CSF
- ✅ NIST CSF to CIS Controls
- ✅ GDPR to CCPA
- ⏳ SOC 2 to FedRAMP (Q3 2025)

Request mapping documents: compliance@gostanna.com

---

## Breach Notification

### Commitment

In the event of a data breach:
- **Detection**: 24/7 monitoring with automated alerts
- **Assessment**: Severity and scope determined within 4 hours
- **Containment**: Immediate isolation of affected systems
- **Notification**: Customers notified within 24 hours of confirmation

### Notification Channels

**Customer Notification**:
- Email to compliance contacts
- In-app notification
- Status page update
- Dedicated incident page

**Regulatory Notification** (if required):
- GDPR: Supervisory authority within 72 hours
- CCPA: California AG as required
- Other: Per applicable law

### Historical Record

**Breaches Since Inception**: 0
**Security Incidents**: 0 affecting customer data
**Last Security Review**: January 2025

---

## Contact Information

### Compliance Team

**General Inquiries**: compliance@gostanna.com
**Privacy Requests**: privacy@gostanna.com
**Data Protection Officer**: dpo@gostanna.com
**Security Issues**: security@gostanna.com

### Mailing Address

Stanna Inc.
[Address]
[City, State ZIP]
United States

### Business Hours

**Support**: 24/7 for security issues
**Compliance Team**: Monday-Friday, 9 AM - 5 PM PST
**Emergency Contact**: +1 (XXX) XXX-XXXX

---

## Regulatory Registrations

**United States**:
- Delaware Corporation
- IRS EIN: [Number]
- State business licenses: [List]

**European Union**:
- GDPR Representative: [Name/Company]
- VAT ID: [Number]
- Data Protection Registration: [Number]

**United Kingdom**:
- ICO Registration: [Number]
- UK Representative: [Name/Company]

---

## Compliance Roadmap

### Q1 2025 ✅
- ✅ Security hardening complete
- ✅ GDPR/CCPA compliance review
- ✅ Documentation updates
- ✅ Subprocessor agreements renewed

### Q2 2025
- 🔄 SOC 2 Type II audit complete
- 📋 Bug bounty program launch
- 📋 MFA implementation
- 📋 Enhanced audit logging

### Q3 2025
- 📋 ISO 27001 certification
- 📋 EU data residency expansion
- 📋 SAML SSO implementation
- 📋 HIPAA compliance (Healthcare offering)

### Q4 2025
- 📋 FedRAMP authorization (in evaluation)
- 📋 APAC data residency
- 📋 SOC 2 Type II renewal
- 📋 PCI DSS (if handling payments)

---

## Updates & Changes

This compliance documentation is reviewed and updated quarterly. Subscribe to compliance updates: compliance@gostanna.com

**Last Updated**: January 2025
**Next Review**: April 2025
**Version**: 1.0

---

## Legal Disclaimer

This document provides an overview of Stanna's compliance programs and is not a substitute for legal or regulatory advice. Customers are responsible for determining whether Stanna meets their specific compliance requirements. For detailed compliance information, please contact our compliance team.

*For the most current compliance information, visit: help.gostanna.com/compliance*
