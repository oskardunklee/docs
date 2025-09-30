# Security FAQ

Common questions about Stanna's security practices.

---

## General Security

### Is Stanna secure?

Yes. Stanna implements enterprise-grade security controls including:
- TLS 1.3 encryption for all data in transit
- AES-256 encryption for data at rest
- Role-based access control (RBAC)
- 24/7 security monitoring
- Regular security audits and penetration testing

We're currently pursuing SOC 2 Type II certification (expected Q2 2025).

### Has Stanna ever been breached?

No. Since our inception, we have had zero security breaches affecting customer data.

### Where is my data stored?

Your data is stored in secure, SOC 2 certified data centers. By default, data is stored in the United States. Enterprise customers can choose EU data residency.

---

## Data Protection

### Is my data encrypted?

Yes, always:
- **In Transit**: TLS 1.3 encryption (the latest standard)
- **At Rest**: AES-256 encryption in our database
- **Backups**: Encrypted with separate keys

### Can Stanna employees see my data?

Stanna employees have minimal access to customer data:
- **Support staff**: Only with explicit permission and for troubleshooting
- **Engineers**: Access only for debugging with approval and audit logging
- **All access**: Logged and monitored

### How is customer data isolated?

Each workspace is completely isolated:
- Database-level separation with workspace IDs
- No cross-workspace queries possible
- Separate encryption keys for Enterprise customers
- API-level authorization checks on every request

### Do you share my data with third parties?

No, we never sell or share your data with third parties except:
- **Service providers**: Minimal data shared with vendors (e.g., email delivery, AI processing) under strict DPAs
- **Legal requirements**: Only when required by valid court order

See our [Privacy Policy](./privacy-policy.md) for details.

---

## Authentication & Access

### How do I log in securely?

Stanna uses OAuth 2.0 with Google for secure authentication:
- No passwords stored by Stanna
- Delegated to Google's enterprise security
- Multi-factor authentication supported (Q2 2025)

### What if I lose my login credentials?

Since authentication is handled by Google, use Google's account recovery process. Stanna never stores your password.

### How do I control who has access to my workspace?

Workspace Owners can:
- Add/remove team members instantly
- Assign granular permissions (Owner, Member, Viewer)
- Review audit logs of all user actions
- Force logout of all sessions

### Can I use Single Sign-On (SSO)?

Yes, Enterprise customers can use:
- Google OAuth (available now)
- SAML-based SSO (Q3 2025)
- Azure AD, Okta, OneLogin (Q3 2025)

---

## Compliance

### Is Stanna GDPR compliant?

Yes. Stanna is fully GDPR compliant:
- Data Processing Agreements available
- Right to access, deletion, portability supported
- Privacy by Design principles
- EU data residency option for Enterprise
- Breach notification within 72 hours

### Is Stanna HIPAA compliant?

Not currently, but we're working on it (Q4 2025). If you need to process Protected Health Information (PHI), contact us at compliance@gostanna.com for our Healthcare offering timeline.

### What about SOC 2?

We're currently pursuing SOC 2 Type II certification:
- All controls implemented
- Audit in progress
- Expected completion: Q2 2025
- Report available upon request (with NDA)

### Can I get a copy of your security certifications?

Yes. Contact compliance@gostanna.com for:
- SOC 2 report (when available)
- Penetration test summaries
- Security questionnaire responses
- DPA and subprocessor list

Most documents require an NDA.

---

## Data Handling

### How long do you keep my data?

- **Active data**: Retained while your account is active
- **Deleted data**: 30-day grace period, then permanent deletion
- **Backups**: 30-day rolling retention (Enterprise: 1 year)
- **Audit logs**: 90 days (Enterprise: 365 days)

### Can I export my data?

Yes, at any time:
- CSV export for all data
- JSON export for API integration
- Full workspace export (Enterprise)
- No lock-in—your data is always accessible

### What happens if I cancel my account?

When you cancel:
1. Account marked for deletion (30-day grace period)
2. Access revoked immediately (can reactivate within 30 days)
3. Data permanently deleted after 30 days
4. Backup data removed within 60 days
5. Confirmation email sent

Request expedited deletion: privacy@gostanna.com

### Do you backup my data?

Yes:
- **Frequency**: Continuous replication + daily snapshots
- **Retention**: 30 days rolling (Enterprise: 1 year)
- **Testing**: Restore tested monthly
- **Encryption**: All backups encrypted

---

## AI & Data Processing

### How is AI used with my data?

Our AI assistant (Lars) provides insights by analyzing your customer data:
- Health score predictions
- Churn risk analysis
- Actionable recommendations

**Important**: AI processing is always within your workspace—no cross-customer training.

### Is my data used to train AI models?

**No.** Your data is never used to train AI models (ours or third-party providers). AI processes your data in real-time to provide insights, but doesn't learn from it.

### What AI providers do you use?

Currently:
- **Groq**: AI inference with Llama 3.3 70B model
- Data Processing Agreement in place
- End-to-end encryption
- No data retention by Groq

### Can I opt out of AI features?

Yes. Contact support@gostanna.com to disable AI features for your workspace. Note: Some features (health predictions, insights) will be unavailable.

---

## Security Features

### Do you have rate limiting?

Yes, to protect against abuse:
- Authentication: 5 attempts/minute
- API: 100 requests/minute
- AI Chat: 20 messages/minute
- Exports: 5 per 5 minutes

Contact us if you need higher limits.

### What security headers do you use?

All recommended security headers:
- Content-Security-Policy (CSP)
- Strict-Transport-Security (HSTS)
- X-Frame-Options (clickjacking protection)
- X-Content-Type-Options (MIME sniffing protection)
- And more...

Rate us: securityheaders.com

### How do you prevent XSS attacks?

Multiple layers of protection:
- Input validation on all data
- Output encoding with DOMPurify
- Content Security Policy (CSP)
- Regular security scanning

### Do you log security events?

Yes, comprehensive audit logging:
- All authentication attempts
- Permission checks and denials
- Data access and exports
- Admin actions
- Security incidents

Logs available in your dashboard (Admin → Audit Logs).

---

## Incident Response

### What if there's a security incident?

Our incident response process:
1. **Detection**: Automated monitoring (24/7)
2. **Response**: Security team alerted within minutes
3. **Containment**: Affected systems isolated
4. **Notification**: Customers notified within 24 hours
5. **Resolution**: Issue fixed and preventive measures implemented
6. **Post-Mortem**: Detailed report shared

### How will I be notified?

Multiple channels:
- Email to workspace admin and compliance contacts
- In-app notification
- Status page update (status.gostanna.com)
- Dedicated incident page with updates

### What's your uptime guarantee?

**SLA**: 99.9% uptime (Enterprise: 99.95%)
**Current uptime**: Check status.gostanna.com
**Credits**: Automatic for SLA violations (Enterprise)

---

## Best Practices

### How can I make my account more secure?

1. **Use a work email** (not personal Gmail/Yahoo)
2. **Enable MFA** when available (Q2 2025)
3. **Review permissions** regularly
4. **Remove inactive users** promptly
5. **Monitor audit logs** for suspicious activity
6. **Use strong, unique passwords** for Google account
7. **Don't share credentials** with team members

### What should I do if I suspect a security issue?

Immediately:
1. **Don't panic** - document what you observed
2. **Contact us**: security@gostanna.com or (XXX) XXX-XXXX
3. **Don't publicize** until we've investigated
4. **Change credentials** if compromised
5. **Review audit logs** for unauthorized access

We respond within 1 hour for critical issues.

### How do I report a vulnerability?

**Email**: security@gostanna.com
**Subject**: "Security Vulnerability Report"

Include:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Your contact information

We commit to:
- Response within 24 hours
- Regular updates on progress
- Credit for discovery (if desired)
- No legal action for good-faith research

---

## Enterprise Features

### What additional security do Enterprise customers get?

Enterprise tier includes:
- Customer-managed encryption keys (CMEK)
- EU/US data residency choice
- Extended audit log retention (365 days)
- Advanced threat detection
- Dedicated security contact
- Priority incident response
- Custom security controls
- IP whitelisting

### Do you offer custom security controls?

Yes, Enterprise customers can request:
- Custom authentication flows
- Additional audit logging
- Enhanced encryption
- Dedicated infrastructure
- Custom data retention policies
- Private cloud deployment (case-by-case)

Contact sales@gostanna.com for details.

---

## Getting Help

### Where can I learn more about security?

- [Security Overview](./overview.md) - Customer-facing overview
- [Security Whitepaper](./whitepaper.md) - Technical details
- [Compliance Documentation](./compliance.md) - Certifications
- Help Center: help.gostanna.com/security

### Who do I contact for security questions?

**General**: security@gostanna.com
**Compliance**: compliance@gostanna.com
**Privacy**: privacy@gostanna.com
**Support**: support@gostanna.com
**Emergency**: +1 (XXX) XXX-XXXX (24/7)

### Can I get a demo of security features?

Yes! Contact sales@gostanna.com to schedule a security-focused demo covering:
- Authentication and access control
- Audit logging
- Data encryption
- Compliance features
- Admin security controls

---

**Last Updated**: January 2025

*For the most current information, visit help.gostanna.com/security*
