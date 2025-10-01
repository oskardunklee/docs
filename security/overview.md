# Stanna Security Overview

## Our Commitment to Security

Stanna implements enterprise security controls to protect your customer success data.

## Security Principles

### 1. Security by Design
Every feature is built with security considerations from the ground up, not added as an afterthought.

### 2. Defense in Depth
We employ multiple layers of security controls, ensuring that if one layer is compromised, others remain intact.

### 3. Continuous Improvement
Security is an ongoing process. We regularly update our systems and conduct security assessments.

### 4. Transparency
We're open about our security practices and quickly communicate any issues to our customers.

---

## How We Protect Your Data

### Authentication & Access Control

**Multi-Factor Authentication**
- Industry-standard OAuth 2.0 with Google authentication
- Secure session management with automatic timeout
- Role-based access control (RBAC) ensures users only see what they're authorized to access

**Strong Password Policies**
- Enterprise SSO support for seamless, secure access
- No shared accounts—every user has their own credentials
- Immediate access revocation when team members leave

### Data Protection

**Encryption**
- **In Transit**: All data is encrypted using TLS 1.3 (the latest security standard)
- **At Rest**: Database encryption ensures your data is protected even if physical storage is compromised
- **End-to-End**: From your browser to our servers, your data never travels unencrypted

**Data Isolation**
- Complete workspace isolation—your data is separate from other customers
- Database-level security ensures no cross-tenant data access
- Regular security audits of data access patterns

**Privacy Controls**
- Personally Identifiable Information (PII) is automatically redacted from logs
- No customer data is used for training AI models without explicit consent
- GDPR and CCPA compliant data handling practices

### Infrastructure Security

**Secure Hosting**
- Cloud infrastructure hosted on industry-leading platforms
- Automated security patching and updates
- Regular vulnerability scanning

**Network Security**
- Advanced DDoS protection to ensure service availability
- Rate limiting prevents abuse and ensures fair usage
- Content Security Policy (CSP) prevents XSS attacks

**Monitoring & Logging**
- Automated security monitoring for suspicious activity
- Comprehensive audit logs track all system access and changes
- Logs retained for 90 days

### Application Security

**Secure Development Practices**
- Regular security training for all engineers
- Code review process includes security checks
- Automated security scanning in our CI/CD pipeline
- Dependency vulnerability monitoring and automatic updates

**Input Validation**
- All user input is validated and sanitized
- Protection against SQL injection, XSS, and CSRF attacks
- Secure handling of file uploads

**AI Security**
- AI-generated content is sanitized before display
- No sensitive data sent to third-party AI providers without encryption
- Rate limiting on AI features prevents abuse

---

## Compliance & Certifications

### Current Status

**GDPR Compliant** ✅
- EU data protection regulation compliance
- User rights: access, deletion, portability
- Data processing agreements available

**CCPA Compliant** ✅
- California Consumer Privacy Act compliance
- Transparent data collection and usage practices

**SOC 2 Type II**
- Status: Not Certified
- Stanna has implemented SOC 2 controls but has not undergone independent audit

**ISO 27001**
- Status: Not Certified

### Security Standards We Follow

- OWASP Top 10 (web application security risks)
- CWE/SANS Top 25 (software weaknesses)
- NIST Cybersecurity Framework
- Cloud Security Alliance (CSA) guidelines

---

## Third-Party Security

### Vendors We Trust

We carefully select our service providers and ensure they meet our security standards:

**Stripe**
- PCI DSS Level 1 certified (highest level of payment security)
- SOC 1, SOC 2 Type II, ISO 27001 certified
- Used for: Payment processing and billing
- Stanna never handles or stores payment information

**Google Cloud Platform**
- Used for: Authentication (OAuth)

**Groq AI**
- Enterprise-grade AI inference
- Data processing agreements in place
- Used for: AI-powered insights

**Resend**
- Secure email delivery
- GDPR compliant
- Used for: Transactional emails

All third-party integrations:
- ✅ Security review before integration
- ✅ Data processing agreements signed
- ✅ Regular security assessments
- ✅ Minimal data sharing (only what's necessary)

---

## Reporting Security Issues

Found a potential security issue? Report it to:

**Email**: security@gostanna.com

We appreciate responsible disclosure and will work to address valid security concerns.

---

## Data Handling & Privacy

### What Data We Collect

**Account Information**
- Email address (for authentication)
- Company name
- User roles and permissions

**Customer Success Data**
- Client names and contact information
- Interaction history
- Health scores and metrics
- Custom fields you configure

**Usage Data**
- Feature usage analytics
- Performance metrics
- Error logs (PII redacted)

### What We Don't Collect

- ❌ Credit card information (handled securely by Stripe)
- ❌ Social security numbers or government IDs
- ❌ Personal health information
- ❌ Financial account details
- ❌ Biometric data

### Payment Processing

All billing and payment processing is handled by **Stripe**, a PCI DSS Level 1 certified payment processor. Stanna never stores or processes credit card information. Stripe maintains:
- PCI DSS Level 1 certification (highest level of payment security)
- SOC 1 and SOC 2 Type II compliance
- ISO 27001 certification
- Advanced fraud detection
- End-to-end encryption for all payment data

Your payment information is protected by Stripe's industry-leading security infrastructure.

### How We Use Your Data

- ✅ Provide the Stanna service to you
- ✅ Improve our product and features
- ✅ Send important service updates
- ✅ Provide customer support
- ❌ Never sold to third parties
- ❌ Never used for advertising
- ❌ Never shared without your consent (except as required by law)

### Your Data Rights

**Access**: Request a copy of all your data
**Deletion**: Delete your account and data at any time
**Portability**: Export your data in standard formats
**Correction**: Update or correct any information
**Opt-out**: Control communication preferences

Contact privacy@gostanna.com to exercise your rights.

---

## Security Features

### Admin Controls

**User Management**
- Add/remove users
- Assign granular permissions (RBAC)
- View audit logs of all user actions

**Access Controls**
- Session timeout configuration
- API key management

**Audit Logging**
- Comprehensive audit logs
- Export logs for compliance
- 90-day retention

### Workspace Security

**Data Isolation**
- Complete separation between workspaces
- No cross-workspace data visibility
- Database-level isolation

**Backup & Recovery**
- Automated daily backups
- 30-day backup retention

---

## API Security

### Authentication

- API keys with fine-grained permissions
- Ability to revoke API keys instantly

### Rate Limiting

To prevent abuse:
- Authentication endpoints: 5 requests/minute
- Standard API calls: 100 requests/minute
- AI endpoints: 20 requests/minute
- Export operations: 5 requests/5 minutes

---

## What We've Built

- ✅ Comprehensive security hardening
- ✅ Rate limiting on all endpoints
- ✅ XSS protection with content sanitization
- ✅ PII redaction in logs
- ✅ Role-based access control (RBAC)
- ✅ Security headers (CSP, HSTS, etc.)
- ✅ OAuth 2.0 authentication
- ✅ TLS 1.3 encryption
- ✅ AES-256 database encryption
- ✅ Audit logging (90-day retention)

---

## Security Best Practices

### For Your Team

1. **Enable MFA on Google**: Use multi-factor authentication on your Google account
2. **Strong Passwords**: Use unique, complex passwords
3. **Review Access**: Regularly audit who has access to your workspace
4. **Remove Inactive Users**: Disable accounts for team members who've left
5. **Secure API Keys**: Store them securely and rotate regularly

---

## Contact

**Security**: security@gostanna.com
**Privacy**: privacy@gostanna.com
**Compliance**: compliance@gostanna.com

---

**Last Updated**: January 2025

For technical security details, see the [Security Whitepaper](./whitepaper.md).
