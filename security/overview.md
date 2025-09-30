# Stanna Security Overview

## Our Commitment to Security

At Stanna, security is not just a feature—it's a fundamental principle that guides everything we build. We understand that you're trusting us with your customer success data, and we take that responsibility seriously.

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
- Cloud infrastructure hosted on industry-leading platforms with SOC 2 Type II certification
- Automated security patching and updates
- Regular vulnerability scanning and penetration testing

**Network Security**
- Advanced DDoS protection to ensure service availability
- Rate limiting prevents abuse and ensures fair usage
- Content Security Policy (CSP) prevents XSS attacks

**Monitoring & Logging**
- 24/7 security monitoring for suspicious activity
- Comprehensive audit logs track all system access and changes
- Automated alerting for security events
- Logs retained for compliance requirements (30+ days)

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

**SOC 2 Type II** (In Progress)
- Expected completion: Q2 2025
- Independent audit of security controls
- Demonstrates commitment to security, availability, and confidentiality

**ISO 27001** (Planned)
- Information security management system
- International standard for security best practices

**GDPR Compliant**
- EU data protection regulation compliance
- User rights: access, deletion, portability
- Data processing agreements available

**CCPA Compliant**
- California Consumer Privacy Act compliance
- Transparent data collection and usage practices

### Security Standards We Follow

- OWASP Top 10 (web application security risks)
- CWE/SANS Top 25 (software weaknesses)
- NIST Cybersecurity Framework
- Cloud Security Alliance (CSA) guidelines

---

## Third-Party Security

### Vendors We Trust

We carefully select our service providers and ensure they meet our security standards:

**Google Cloud Platform**
- SOC 2/3, ISO 27001, PCI DSS certified
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

## Incident Response

### Our Commitment

In the unlikely event of a security incident:

1. **Detection** - 24/7 monitoring detects issues immediately
2. **Response** - Security team responds within 1 hour
3. **Containment** - Affected systems isolated to prevent spread
4. **Investigation** - Root cause analysis conducted
5. **Notification** - Affected customers notified within 24 hours
6. **Resolution** - Issue resolved and preventive measures implemented
7. **Post-Mortem** - Detailed report shared with affected customers

### How to Report Security Issues

Found a potential security issue? We appreciate responsible disclosure:

**Email**: security@gostanna.com
**Expected Response**: Within 24 hours
**Bug Bounty**: Contact us for details

We commit to:
- Acknowledging your report within 24 hours
- Keeping you informed of our progress
- Crediting you for the discovery (if desired)
- Not pursuing legal action for good-faith research

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

- ❌ Credit card information (handled by Stripe)
- ❌ Social security numbers or government IDs
- ❌ Personal health information
- ❌ Financial account details
- ❌ Biometric data

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

## Security Features for Administrators

### Admin Controls

**User Management**
- Add/remove users instantly
- Assign granular permissions
- View audit logs of all user actions
- Force password reset for all users

**Access Controls**
- IP whitelisting (Enterprise plan)
- Session timeout configuration
- Device management and logout
- API key management

**Audit & Compliance**
- Comprehensive audit logs
- Export logs for compliance review
- User activity reports
- Data access history

### Workspace Security

**Data Isolation**
- Complete separation between workspaces
- No cross-workspace data visibility
- Separate encryption keys per workspace (Enterprise)

**Backup & Recovery**
- Automated daily backups
- 30-day backup retention
- Point-in-time recovery available
- Disaster recovery procedures tested quarterly

---

## API Security

### Authentication

- API keys with fine-grained permissions
- OAuth 2.0 support for integrations
- Short-lived tokens with automatic refresh
- Ability to revoke API keys instantly

### Rate Limiting

To ensure fair usage and prevent abuse:
- Authentication endpoints: 5 requests/minute
- Standard API calls: 100 requests/minute
- AI endpoints: 20 requests/minute
- Export operations: 5 requests/5 minutes

### Best Practices

We recommend:
- Rotate API keys every 90 days
- Use separate keys for different integrations
- Never commit API keys to version control
- Use environment variables for key storage

---

## Security Roadmap

### Recently Completed (Q4 2024 - Q1 2025)

- ✅ Comprehensive security audit and hardening
- ✅ Implementation of rate limiting
- ✅ Advanced XSS protection
- ✅ PII redaction in logs
- ✅ Role-based access control (RBAC)
- ✅ Security headers implementation

### In Progress (Q1-Q2 2025)

- 🔄 SOC 2 Type II certification
- 🔄 Third-party penetration testing
- 🔄 Bug bounty program launch
- 🔄 Enhanced audit logging
- 🔄 Multi-factor authentication (MFA)

### Planned (Q2-Q3 2025)

- 📋 ISO 27001 certification
- 📋 SAML-based SSO
- 📋 Advanced threat detection
- 📋 Customer-managed encryption keys (CMEK)
- 📋 Data residency options (EU, US regions)

---

## Security Best Practices for Customers

### For Your Team

1. **Strong Passwords**: Use unique, complex passwords (or better yet, a password manager)
2. **Enable MFA**: Add an extra layer of security (available Q2 2025)
3. **Review Access**: Regularly audit who has access to your workspace
4. **Remove Inactive Users**: Disable accounts for team members who've left
5. **Secure API Keys**: Store them securely and rotate regularly

### For Your Workspace

1. **Configure Permissions**: Follow principle of least privilege
2. **Monitor Audit Logs**: Review regularly for suspicious activity
3. **Backup Important Data**: Export critical data regularly
4. **Train Your Team**: Ensure everyone understands security best practices
5. **Report Issues**: Contact us immediately if you notice anything suspicious

---

## Contact Our Security Team

**General Security Inquiries**: security@gostanna.com
**Privacy Questions**: privacy@gostanna.com
**Report a Vulnerability**: security@gostanna.com (encrypted PGP available)
**Compliance Questions**: compliance@gostanna.com

**Response Time Commitment**:
- Security vulnerabilities: 24 hours
- Privacy requests: 48 hours
- General inquiries: 3 business days

---

## Additional Resources

- [Security Whitepaper](./whitepaper.md) - Technical deep-dive
- [Compliance Documentation](./compliance.md) - Certifications and standards
- [Privacy Policy](./privacy-policy.md) - Detailed privacy practices
- [Terms of Service](./terms-of-service.md) - Service agreement
- [Data Processing Agreement](./dpa.md) - GDPR compliance

---

## Transparency Report

We publish an annual transparency report detailing:
- Security incidents and response
- Data requests from law enforcement
- Service uptime and reliability
- Security improvements made

**Latest Report**: [Coming Q2 2025]

---

**Last Updated**: January 2025
**Next Review**: April 2025

*Stanna is committed to maintaining the highest security standards. This document is regularly updated to reflect our current practices and capabilities.*
