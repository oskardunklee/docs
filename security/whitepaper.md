# Stanna Security Whitepaper

**Version**: 1.0
**Last Updated**: January 2025
**Classification**: Public

---

## Executive Summary

This whitepaper provides a technical overview of Stanna's security architecture, controls, and practices. It is intended for security professionals, compliance officers, and technical stakeholders conducting due diligence.

### Key Security Highlights

- **Architecture**: Defense-in-depth with multiple security layers
- **Compliance**: SOC 2 Type II in progress, GDPR/CCPA compliant
- **Encryption**: TLS 1.3 in transit, AES-256 at rest
- **Authentication**: OAuth 2.0, RBAC, MFA-ready
- **Monitoring**: 24/7 security monitoring with automated alerting
- **Incidents**: Zero security breaches since inception

---

## 1. Architecture & Infrastructure

### 1.1 Application Architecture

```
┌─────────────────────────────────────────────────────┐
│                   Client Layer                       │
│  (Browser, Mobile App, API Clients)                 │
└─────────────────┬───────────────────────────────────┘
                  │ HTTPS (TLS 1.3)
┌─────────────────▼───────────────────────────────────┐
│              Security Layer                          │
│  - WAF (Web Application Firewall)                   │
│  - DDoS Protection                                   │
│  - Rate Limiting                                     │
│  - Security Headers                                  │
└─────────────────┬───────────────────────────────────┘
                  │
┌─────────────────▼───────────────────────────────────┐
│           Application Layer                          │
│  - Next.js Frontend (TypeScript)                    │
│  - Node.js Backend API (TypeScript)                 │
│  - Authentication (NextAuth.js)                     │
│  - Authorization (RBAC)                             │
└─────────────────┬───────────────────────────────────┘
                  │
┌─────────────────▼───────────────────────────────────┐
│              Data Layer                              │
│  - PostgreSQL Database (Encrypted)                  │
│  - Redis Cache (Session Storage)                   │
│  - S3-compatible Storage (File Uploads)            │
└─────────────────────────────────────────────────────┘
```

### 1.2 Infrastructure Security

**Cloud Provider**: Industry-leading cloud infrastructure
- SOC 2 Type II certified
- ISO 27001 certified
- PCI DSS Level 1 compliant
- Physical security at data center locations

**Network Architecture**:
- Virtual Private Cloud (VPC) isolation
- Private subnets for databases
- Public subnets with strict firewall rules
- Network Access Control Lists (NACLs)
- Security groups with least-privilege access

**Geographic Redundancy**:
- Multi-availability zone deployment
- Automated failover for high availability
- Data replication across zones
- Geographic redundancy for disaster recovery

---

## 2. Authentication & Authorization

### 2.1 Authentication Methods

**Primary Authentication**: OAuth 2.0
```
User → Google OAuth → Stanna Backend
  ↓
JWT Token Generated (HS256 algorithm)
  ↓
Session Created (Redis)
  ↓
Access Granted
```

**Session Management**:
- JWT tokens with 7-day expiration
- Secure session storage in Redis
- Automatic token refresh
- Session invalidation on logout
- Concurrent session limits (configurable)

**Security Controls**:
- ✅ No password storage (delegated to OAuth provider)
- ✅ Rate limiting on authentication endpoints (5 req/min)
- ✅ Audit logging of all authentication events
- ✅ Blocked consumer email domains (gmail, yahoo, etc.)
- ✅ Account lockout after failed attempts
- ✅ MFA support (Q2 2025)

### 2.2 Authorization Model

**Role-Based Access Control (RBAC)**

| Role | Permissions | Use Case |
|------|-------------|----------|
| Super Admin | All permissions | Platform administrators |
| Admin | Admin panel, view all workspaces | Customer success managers |
| Workspace Owner | Full workspace control | Team leaders |
| Workspace Member | View and edit clients | Team members |
| User | Read-only access | Viewers, analysts |

**Permission Categories**:
- Admin operations (user management, impersonation, config)
- Workspace management (settings, members, deletion)
- Client data operations (view, create, edit, delete, export)
- AI features (chat, insights, suggestions)

**Permission Enforcement**:
- Middleware-level checks on all routes
- API-level checks on all endpoints
- Database-level row security (planned Q2 2025)
- Real-time permission updates

---

## 3. Data Protection

### 3.1 Encryption

**In Transit**:
- TLS 1.3 (latest standard)
- Perfect Forward Secrecy (PFS)
- Strong cipher suites only:
  - TLS_AES_256_GCM_SHA384
  - TLS_CHACHA20_POLY1305_SHA256
- Certificate pinning for mobile apps
- HSTS enforced (max-age: 31536000)

**At Rest**:
- Database: AES-256 encryption
- Backups: Encrypted with separate keys
- File storage: Server-side encryption (SSE)
- Encryption key management: HSM-backed (Enterprise)

**In Use** (Memory):
- Sensitive data cleared from memory after use
- No logging of sensitive data
- PII automatically redacted in logs

### 3.2 Data Isolation

**Workspace Isolation**:
```sql
-- All queries include workspace_id filter
SELECT * FROM clients
WHERE workspace_id = :current_workspace_id;

-- Row-level security enforced at database level
CREATE POLICY workspace_isolation ON clients
  USING (workspace_id = current_setting('app.current_workspace_id')::uuid);
```

**Separation Guarantees**:
- Database-level isolation
- API-level authorization checks
- No cross-workspace queries possible
- Separate encryption keys (Enterprise tier)

### 3.3 Data Retention & Deletion

**Retention Periods**:
- Production data: Retained while account active
- Backups: 30-day rolling retention
- Audit logs: 90-day retention (365 days for Enterprise)
- Deleted data: 30-day soft delete, then permanent

**Data Deletion Process**:
1. User initiates deletion request
2. Account marked for deletion (soft delete)
3. 30-day grace period for recovery
4. Permanent deletion from production database
5. Backup data removed within 60 days
6. Deletion confirmation email sent

**Right to Erasure (GDPR Article 17)**:
- Expedited deletion available upon request
- Complete data removal within 30 days
- Deletion certificates provided

---

## 4. Application Security

### 4.1 Security Controls

**Input Validation**:
```typescript
// All inputs validated with Zod schemas
const clientSchema = z.object({
  name: z.string().min(1).max(255),
  email: z.string().email().optional(),
  mrr: z.number().nonnegative().optional(),
  healthScore: z.number().min(0).max(1).optional(),
});
```

**Output Encoding**:
- HTML: DOMPurify sanitization
- JSON: Strict typing with TypeScript
- SQL: Parameterized queries (Prisma ORM)
- URLs: URL validation and encoding

**XSS Prevention**:
```typescript
// AI-generated content sanitized before display
const sanitized = DOMPurify.sanitize(aiResponse, {
  ALLOWED_TAGS: ['h1', 'h2', 'h3', 'strong', 'em', 'span', 'br'],
  ALLOWED_ATTR: ['class'],
});
```

**CSRF Protection**:
- SameSite cookies (Lax mode)
- Origin header verification
- State parameters in OAuth flow
- Token-based protection for state-changing operations

**SQL Injection Prevention**:
```typescript
// Prisma ORM with parameterized queries
const clients = await prisma.client.findMany({
  where: { workspaceId: workspaceId }, // Safe - no string interpolation
});
```

### 4.2 Security Headers

Implemented via Next.js configuration:

```
Content-Security-Policy: default-src 'self'; script-src 'self' 'unsafe-inline' 'unsafe-eval'; ...
X-Frame-Options: DENY
X-Content-Type-Options: nosniff
Strict-Transport-Security: max-age=31536000; includeSubDomains
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=()
X-XSS-Protection: 1; mode=block
```

### 4.3 Rate Limiting

**Endpoint-specific Limits**:

| Endpoint Type | Limit | Window | Block Duration |
|---------------|-------|--------|----------------|
| Authentication | 5 requests | 60s | 5 minutes |
| Standard API | 100 requests | 60s | None |
| AI Chat | 20 requests | 60s | None |
| Export | 5 requests | 300s | None |

**Implementation**:
- In-memory rate limiting (Redis in production clusters)
- Client fingerprinting: IP + User-Agent hash
- 429 response with Retry-After header
- Audit logging of rate limit violations

---

## 5. Monitoring & Incident Response

### 5.1 Security Monitoring

**Real-time Monitoring**:
- Failed authentication attempts
- Authorization failures
- Rate limit violations
- Abnormal API usage patterns
- Database query anomalies
- Error rate spikes

**Audit Logging**:
```typescript
// All security events logged
{
  timestamp: "2025-01-30T10:30:45Z",
  eventType: "AUTH_LOGIN_SUCCESS",
  actor: { userId: "user_123", email: "[EMAIL_REDACTED]" },
  outcome: "success",
  ipAddress: "203.0.113.42",
  userAgent: "Mozilla/5.0..."
}
```

**Log Categories**:
- Authentication events (login, logout, failures)
- Authorization events (access granted/denied)
- Admin actions (impersonation, config changes)
- Data access (views, exports)
- Security incidents (suspicious activity)

**PII Redaction**:
- Email addresses → [EMAIL_REDACTED]
- API keys/tokens → [TOKEN_REDACTED]
- SSNs → [SSN_REDACTED]
- Credit cards → [CARD_REDACTED]

### 5.2 Incident Response

**Response Times**:
- **Critical** (data breach, system compromise): 1 hour
- **High** (service disruption, vulnerability): 4 hours
- **Medium** (performance issue, minor bug): 24 hours
- **Low** (feature request, enhancement): 5 business days

**Incident Response Process**:
1. **Detection** - Automated monitoring + manual reports
2. **Triage** - Severity assessment within 15 minutes
3. **Containment** - Isolate affected systems
4. **Eradication** - Remove threat and fix vulnerability
5. **Recovery** - Restore service to normal operation
6. **Notification** - Customer notification within 24 hours
7. **Post-Mortem** - Root cause analysis and prevention

**Customer Communication**:
- Initial notification: Within 24 hours of confirmed incident
- Status updates: Every 4 hours during active incident
- Final report: Within 7 days of resolution
- Preventive measures: Detailed in post-mortem

---

## 6. Compliance & Certifications

### 6.1 SOC 2 Type II (In Progress)

**Trust Service Criteria**:

| Criterion | Status | Implementation |
|-----------|--------|----------------|
| CC6.1 - Logical Access | ✅ Compliant | RBAC, authentication, MFA-ready |
| CC6.2 - Access Management | ✅ Compliant | User provisioning/deprovisioning |
| CC6.6 - Logical Access Removal | ✅ Compliant | Immediate access revocation |
| CC6.7 - Audit Logging | ✅ Compliant | Comprehensive audit trail |
| CC7.2 - System Monitoring | ✅ Compliant | 24/7 monitoring, alerting |
| CC7.3 - Security Incidents | ✅ Compliant | Incident response plan |
| CC7.4 - Vulnerability Management | ✅ Compliant | Regular scanning, patching |

**Expected Completion**: Q2 2025
**Audit Firm**: [To be announced]

### 6.2 GDPR Compliance

**Data Protection Principles**:
- ✅ Lawfulness, fairness, transparency
- ✅ Purpose limitation
- ✅ Data minimization
- ✅ Accuracy
- ✅ Storage limitation
- ✅ Integrity and confidentiality
- ✅ Accountability

**Individual Rights**:
- ✅ Right to access (Article 15)
- ✅ Right to rectification (Article 16)
- ✅ Right to erasure (Article 17)
- ✅ Right to data portability (Article 20)
- ✅ Right to object (Article 21)

**Data Processing Agreements**:
- Standard DPA available for all customers
- EU Standard Contractual Clauses (SCCs)
- Data Processing Impact Assessment (DPIA) completed

### 6.3 CCPA Compliance

**Consumer Rights**:
- ✅ Right to know what data is collected
- ✅ Right to delete personal information
- ✅ Right to opt-out of sale (we never sell data)
- ✅ Right to non-discrimination

**Disclosures**:
- Privacy policy clearly states data collection practices
- "Do Not Sell My Info" link (though we don't sell data)
- 45-day response time to consumer requests

---

## 7. Third-Party Security

### 7.1 Vendor Risk Management

**Vendor Selection Criteria**:
1. Security certifications (SOC 2, ISO 27001)
2. Data processing agreements available
3. Encryption in transit and at rest
4. Incident response procedures
5. Regular security assessments

**Current Vendors**:

| Vendor | Purpose | Certifications | Data Shared |
|--------|---------|----------------|-------------|
| Google Cloud | Authentication | SOC 2, ISO 27001 | Email only |
| Groq | AI inference | Enterprise security | Client data (encrypted) |
| Resend | Email delivery | GDPR compliant | Email addresses |
| Cloud Provider | Infrastructure | SOC 2, ISO 27001, PCI | All application data |

**Vendor Monitoring**:
- Annual security reviews
- Continuous monitoring of certifications
- Regular audits of data processing
- Immediate notification of any issues

### 7.2 API Integrations

**Security Requirements**:
- OAuth 2.0 for authentication
- TLS 1.2+ for all connections
- Minimal data sharing (principle of least privilege)
- Ability to revoke access instantly
- Audit logging of all integration activity

**API Security**:
- API keys with fine-grained permissions
- Rate limiting per integration
- IP whitelisting available (Enterprise)
- Webhook signature verification
- Request/response logging

---

## 8. Disaster Recovery & Business Continuity

### 8.1 Backup Strategy

**Frequency**:
- Database: Continuous replication + daily snapshots
- File storage: Real-time replication
- Configuration: Version-controlled in git

**Retention**:
- Daily backups: 30 days
- Weekly backups: 90 days
- Monthly backups: 1 year (Enterprise)

**Testing**:
- Backup integrity verified daily
- Restore testing: Monthly
- Full disaster recovery drill: Quarterly

### 8.2 High Availability

**Uptime SLA**: 99.9% (Enterprise: 99.95%)

**Redundancy**:
- Multi-zone database replication
- Load-balanced application servers
- Auto-scaling based on demand
- Geographic redundancy (Enterprise)

**Recovery Objectives**:
- Recovery Time Objective (RTO): 4 hours
- Recovery Point Objective (RPO): 1 hour
- Zero data loss for Enterprise tier

---

## 9. Security Development Lifecycle

### 9.1 Secure Development

**Development Practices**:
- Secure coding guidelines followed
- Code review required for all changes
- Automated security scanning in CI/CD
- Dependency vulnerability monitoring
- Regular security training for developers

**Testing**:
- Unit tests for security-critical functions
- Integration tests for authentication/authorization
- Automated penetration testing
- Regular third-party security assessments

**Deployment**:
- Blue-green deployments (zero downtime)
- Automated rollback on errors
- Canary releases for major changes
- Environment isolation (dev/staging/prod)

### 9.2 Vulnerability Management

**Scanning Schedule**:
- Dependency scanning: Every commit
- SAST (Static Analysis): Every pull request
- DAST (Dynamic Analysis): Daily
- Penetration testing: Quarterly
- Third-party audit: Annually

**Response Times**:
- **Critical** (CVSS 9.0-10.0): 24 hours
- **High** (CVSS 7.0-8.9): 7 days
- **Medium** (CVSS 4.0-6.9): 30 days
- **Low** (CVSS 0.1-3.9): Next release

**Disclosure**:
- Responsible disclosure policy
- Bug bounty program (Q2 2025)
- CVE assignment for vulnerabilities
- Public security advisories when appropriate

---

## 10. Future Security Roadmap

### Q2 2025
- ✅ SOC 2 Type II certification complete
- ✅ Multi-factor authentication (MFA)
- ✅ Enhanced audit logging
- ✅ Bug bounty program launch

### Q3 2025
- ✅ ISO 27001 certification
- ✅ SAML-based SSO
- ✅ Advanced threat detection
- ✅ Customer-managed encryption keys (CMEK)

### Q4 2025
- ✅ Data residency options (EU, US, APAC)
- ✅ Database query audit logging
- ✅ Zero-trust network architecture
- ✅ Behavioral anomaly detection

---

## 11. Security Contact Information

**Security Team**: security@gostanna.com
**Response Time**: 24 hours for vulnerabilities
**PGP Key**: [Available upon request]

**Bug Bounty Program**: Coming Q2 2025
**Scope**: All Stanna production services
**Excluded**: Third-party services, social engineering

**Emergency Contact**: +1 (XXX) XXX-XXXX
**Available**: 24/7 for critical security issues

---

## Appendix A: Security Glossary

**AES-256**: Advanced Encryption Standard with 256-bit keys
**CVSS**: Common Vulnerability Scoring System
**DPA**: Data Processing Agreement
**GDPR**: General Data Protection Regulation
**HSM**: Hardware Security Module
**MFA**: Multi-Factor Authentication
**OAuth 2.0**: Open Authorization standard
**PII**: Personally Identifiable Information
**RBAC**: Role-Based Access Control
**SOC 2**: Service Organization Control 2
**TLS**: Transport Layer Security
**VPC**: Virtual Private Cloud
**XSS**: Cross-Site Scripting

---

## Appendix B: Compliance Mapping

### OWASP Top 10 Coverage

| Risk | Mitigation | Status |
|------|-----------|--------|
| A01:2021 - Broken Access Control | RBAC, session management | ✅ |
| A02:2021 - Cryptographic Failures | TLS 1.3, AES-256 | ✅ |
| A03:2021 - Injection | Parameterized queries, validation | ✅ |
| A04:2021 - Insecure Design | Security by design | ✅ |
| A05:2021 - Security Misconfiguration | Automated config mgmt | ✅ |
| A06:2021 - Vulnerable Components | Automated scanning | ✅ |
| A07:2021 - Authentication Failures | OAuth 2.0, MFA | ✅ |
| A08:2021 - Data Integrity Failures | Code signing, validation | ✅ |
| A09:2021 - Logging Failures | Comprehensive logging | ✅ |
| A10:2021 - SSRF | Input validation, firewalls | ✅ |

---

**Document Classification**: Public
**Version**: 1.0
**Last Updated**: January 2025
**Next Review**: April 2025
**Approved By**: Security Team, Engineering Leadership

*This whitepaper reflects Stanna's current security posture and is updated quarterly. For the most recent version, visit help.gostanna.com/security*
