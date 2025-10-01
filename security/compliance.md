# Stanna Compliance Documentation

---

## Compliance Overview

Stanna is committed to meeting the highest standards of security and compliance. This document provides information about our compliance programs, certifications, and audit results.

---

## Compliance Status

### ✅ GDPR (General Data Protection Regulation)
**Status**: Compliant

**Implementations**:
- Data Processing Agreements available
- User rights: access, deletion, portability
- Data encryption (TLS 1.3 in transit, AES-256 at rest)
- Audit logging of data access
- Workspace data isolation

### ✅ CCPA (California Consumer Privacy Act)
**Status**: Compliant

**Implementations**:
- Consumer rights (know, delete, opt-out)
- Privacy policy disclosure
- We don't sell data
- Data deletion available

### SOC 2 Type II
**Status**: Not Certified

Stanna is not currently SOC 2 certified. We have implemented many SOC 2 controls but have not undergone an independent audit.

### ISO 27001
**Status**: Not Certified

Stanna is not currently ISO 27001 certified.

---

## Industry-Specific Compliance

### Healthcare (HIPAA)
**Status**: Not HIPAA Compliant

Do not use Stanna to process Protected Health Information (PHI).

### Financial Services (PCI DSS)
Stanna does not directly handle credit card data or financial transactions. All payment processing is handled by **Stripe**, which maintains:
- PCI DSS Level 1 certification (highest level of payment security)
- SOC 1 and SOC 2 Type II compliance
- ISO 27001 certification

Your payment information never touches Stanna's servers and is protected by Stripe's industry-leading security infrastructure.

### Government (FedRAMP, FISMA)
**Status**: Not Authorized

Stanna is not authorized for FedRAMP or FISMA compliance.

---

## Data Protection & Privacy

### Data Residency

Data is stored in the United States by default.

### International Data Transfers

Standard Contractual Clauses (SCCs) are available for EU-US data transfers as part of our Data Processing Agreement.

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
1. Submit request to privacy@gostanna.com
2. Identity verification
3. Response within 30 days (GDPR) or 45 days (CCPA)
4. Data delivered in machine-readable format

---

## Security Practices

### Vulnerability Scanning

Continuous automated scanning of dependencies and code for security vulnerabilities.

### Security Assessments

Regular internal security assessments and code reviews.

---

## Available Documentation

**Security**:
- Security Overview
- Security FAQ
- Data Processing Agreement (DPA)
- Subprocessor List

**How to Request**:
Email compliance@gostanna.com with your specific requirements.

---

## Subprocessors & Third Parties

### Subprocessor List

| Subprocessor | Purpose | Data Processed | Location | Certifications |
|--------------|---------|----------------|----------|----------------|
| Stripe | Payment processing | Payment information | Global | PCI DSS L1, SOC 2, ISO 27001 |
| Google Cloud | Authentication | Email addresses | Global | - |
| Groq | AI inference | Client data (encrypted) | US | - |
| Resend | Email delivery | Email addresses | US | GDPR compliant |

Updated subprocessor list available at: help.gostanna.com/subprocessors

---

## Security Standards

We align with industry-standard security frameworks:
- OWASP Top 10 (web application security)
- CWE/SANS Top 25 (software weaknesses)
- NIST Cybersecurity Framework

---

## Security History

**Last Security Review**: January 2025

---

## Contact Information

**General Inquiries**: compliance@gostanna.com
**Privacy Requests**: privacy@gostanna.com
**Security Issues**: security@gostanna.com

---

**Last Updated**: January 2025

This document provides an overview of Stanna's compliance status. For specific compliance questions, please contact compliance@gostanna.com.
