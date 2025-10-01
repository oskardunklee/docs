# Stanna Security Whitepaper

**Version**: 1.0
**Last Updated**: January 2025
**Classification**: Public

---

## Executive Summary

This whitepaper provides a technical overview of Stanna's security architecture, controls, and practices. It is intended for security professionals, compliance officers, and technical stakeholders conducting due diligence.

### Key Security Highlights

- **Architecture**: Defense-in-depth with multiple security layers
- **Compliance**: GDPR/CCPA compliant
- **Encryption**: TLS 1.3 in transit, AES-256 at rest
- **Authentication**: OAuth 2.0 with Google, RBAC implemented
- **Monitoring**: Automated security monitoring with audit logging
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

**Cloud Provider**: Industry-leading cloud infrastructure with enterprise-grade security

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

### 3.3 Data Retention & Deletion

**Retention Periods**:
- Production data: Retained while account active
- Backups: 30-day rolling retention
- Audit logs: 90-day retention
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

## 5. Security Monitoring

### 5.1 Audit Logging

**What We Log**:
- Authentication events (login, logout, failures)
- Authorization events (access granted/denied)
- Admin actions (impersonation, config changes)
- Data access (views, exports)

**Audit Log Format**:
```typescript
{
  timestamp: "2025-01-30T10:30:45Z",
  eventType: "AUTH_LOGIN_SUCCESS",
  actor: { userId: "user_123", email: "[EMAIL_REDACTED]" },
  outcome: "success",
  ipAddress: "203.0.113.42"
}
```

**PII Redaction**:
- Email addresses → [EMAIL_REDACTED]
- API keys/tokens → [TOKEN_REDACTED]
- Sensitive data automatically redacted from logs

**Retention**: 90 days

---

## 6. Compliance

### 6.1 GDPR Compliance

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

### 6.2 CCPA Compliance

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

| Vendor | Purpose | Data Shared | Certifications |
|--------|---------|-------------|----------------|
| Stripe | Payment processing | Payment information (never stored by Stanna) | PCI DSS L1, SOC 1, SOC 2, ISO 27001 |
| Google Cloud | Authentication | Email only | - |
| Groq | AI inference | Client data (encrypted) | - |
| Resend | Email delivery | Email addresses | GDPR compliant |

**Payment Security**: All billing and payment processing is handled exclusively by Stripe. Stanna never stores, processes, or has access to credit card information. Stripe maintains the highest level of payment security certification (PCI DSS Level 1) along with SOC 1, SOC 2 Type II, and ISO 27001 compliance.

**Vendor Monitoring**:
- Regular security reviews
- Continuous monitoring of security posture
- Data processing audits

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

**Testing**:
- Backup integrity verified daily
- Restore testing: Monthly

### 8.2 High Availability

**Infrastructure**:
- Multi-zone database replication
- Load-balanced application servers
- Auto-scaling based on demand

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

**Scanning**:
- Dependency scanning: Automated on every commit
- Static analysis: On every pull request
- Continuous vulnerability monitoring

**Disclosure**:
- Responsible disclosure policy
- Security advisories for significant issues

---

## 10. Contact

**Security**: security@gostanna.com
**Compliance**: compliance@gostanna.com
**Privacy**: privacy@gostanna.com

Report security vulnerabilities to security@gostanna.com

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
**Last Updated**: September 2024

*This whitepaper reflects Stanna's current security implementation. For questions, contact security@gostanna.com*
