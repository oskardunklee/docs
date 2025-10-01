# Security FAQ

Common questions about Stanna's security practices.

---

## General Security

### Is Stanna secure?

Yes. Stanna implements enterprise-grade security controls including:
- TLS 1.3 encryption for all data in transit
- AES-256 encryption for data at rest
- Role-based access control (RBAC)
- Automated security monitoring
- Regular security assessments

### Has Stanna ever been breached?

No. Since our inception, we have had zero security breaches affecting customer data.

### Where is my data stored?

Your data is stored in secure data centers in the United States.

---

## Data Protection

### Is my data encrypted?

Yes, always:
- **In Transit**: TLS 1.3 encryption (the latest standard)
- **At Rest**: AES-256 encryption in our database
- **Backups**: Encrypted with separate keys

### How is payment information secured?

All payment processing is handled by **Stripe**, not Stanna. Stripe maintains:
- PCI DSS Level 1 certification (highest level of payment security)
- SOC 1 and SOC 2 Type II compliance
- ISO 27001 certification
- Advanced fraud detection
- End-to-end encryption

Stanna never stores, processes, or has access to your credit card information. Your payment data is protected by Stripe's industry-leading security infrastructure.

### Can Stanna employees see my data?

Stanna employees have minimal access to customer data:
- **Support staff**: Only with explicit permission and for troubleshooting
- **Engineers**: Access only for debugging with approval and audit logging
- **All access**: Logged and monitored

### How is customer data isolated?

Each workspace is completely isolated:
- Database-level separation with workspace IDs
- No cross-workspace queries possible
- API-level authorization checks on every request

### Do you share my data with third parties?

No, we never sell or share your data with third parties except:
- **Payment processing**: Stripe handles all billing (PCI DSS Level 1 certified - Stanna never stores payment info)
- **Service providers**: Minimal data shared with vendors (e.g., email delivery, AI processing) under strict DPAs
- **Legal requirements**: Only when required by valid court order

See our [Privacy Policy](./privacy-policy.md) for details.

---

## Authentication & Access

### How do I log in securely?

Stanna uses OAuth 2.0 with Google for secure authentication:
- No passwords stored by Stanna
- Delegated to Google's enterprise security
- Use MFA on your Google account for additional security

### What if I lose my login credentials?

Since authentication is handled by Google, use Google's account recovery process. Stanna never stores your password.

### How do I control who has access to my workspace?

Workspace Owners can:
- Add/remove team members instantly
- Assign granular permissions (Owner, Member, Viewer)
- Review audit logs of all user actions
- Force logout of all sessions

### Can I use Single Sign-On (SSO)?

Yes, Stanna uses Google OAuth for authentication. All users authenticate via their Google account.

---

## Compliance

### Is Stanna GDPR compliant?

Yes. Stanna is GDPR compliant:
- Data Processing Agreements available
- Right to access, deletion, portability supported
- Breach notification within 72 hours

### Is Stanna HIPAA compliant?

No. Do not use Stanna to process Protected Health Information (PHI).

### What about SOC 2?

Stanna is not currently SOC 2 certified. We have implemented many SOC 2 controls but have not completed an independent audit.

### Can I get security documentation?

Contact compliance@gostanna.com for:
- Security overview and FAQ
- Data Processing Agreement (DPA)
- Subprocessor list
- Security questionnaire responses

---

## Data Handling

### How long do you keep my data?

- **Active data**: Retained while your account is active
- **Deleted data**: 30-day grace period, then permanent deletion
- **Backups**: 30-day rolling retention
- **Audit logs**: 90 days

### Can I export my data?

Yes, at any time:
- CSV export for all data
- JSON export for API integration
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
- **Retention**: 30 days rolling
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

Contact support@gostanna.com to discuss disabling AI features for your workspace. Note: Some features (health predictions, insights) will be unavailable.

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

## Security Status

### Has Stanna had any security incidents?

No. We have had zero security breaches since inception.

### Where can I check system status?

Check status.gostanna.com for current system status and uptime.

---

## Best Practices

### How can I make my account more secure?

1. **Use a work email** (not personal Gmail/Yahoo)
2. **Enable MFA on Google** for additional security
3. **Review permissions** regularly
4. **Remove inactive users** promptly
5. **Monitor audit logs** for suspicious activity
6. **Use strong, unique passwords** for Google account
7. **Don't share credentials** with team members

### What should I do if I suspect a security issue?

Contact us at security@gostanna.com with details about what you observed.

### How do I report a vulnerability?

Email security@gostanna.com with:
- Description of the vulnerability
- Steps to reproduce
- Potential impact

We appreciate responsible disclosure.

---

## Custom Requirements

### Do you offer custom security controls?

For enterprise customers with specific security requirements, contact sales@gostanna.com to discuss custom solutions.

---

## Getting Help

### Where can I learn more about security?

- [Security Overview](./overview.md) - Customer-facing overview
- [Security Whitepaper](./whitepaper.md) - Technical details
- [Compliance Documentation](./compliance.md) - Compliance status

### Who do I contact for security questions?

**General**: security@gostanna.com
**Compliance**: compliance@gostanna.com
**Privacy**: privacy@gostanna.com
**Support**: support@gostanna.com

---

**Last Updated**: September 2024
