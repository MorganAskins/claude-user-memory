---
name: audit
description: Quick command to invoke security-auditor for comprehensive security scanning. Checks OWASP Top 10, dependencies, secrets, and provides remediation guidance.
---

# /audit Command

Execute security audit using the security-auditor agent.

## Usage

```
/audit                           # Full security audit
/audit src/                      # Audit specific directory
/audit --deps                    # Focus on dependencies
/audit --secrets                 # Focus on secrets detection
/audit --owasp                   # OWASP Top 10 compliance
```

## What This Does

1. Invokes `@security-auditor` with your target
2. Performs comprehensive security analysis:
   - OWASP Top 10 compliance check
   - Dependency vulnerability scan
   - Secrets detection
   - Security configuration review
3. Classifies findings by severity
4. Provides remediation guidance

## Security Checks Performed

**OWASP Top 10**:
- A01: Broken Access Control
- A02: Cryptographic Failures
- A03: Injection
- A04: Insecure Design
- A05: Security Misconfiguration
- A06: Vulnerable Components
- A07: Authentication Failures
- A08: Integrity Failures
- A09: Logging Failures
- A10: SSRF

**Additional Checks**:
- Hardcoded secrets/credentials
- Dependency vulnerabilities (CVEs)
- Security headers
- Input validation
- Error handling

## Output

You'll receive:

- **Executive Summary**: Overall security posture
- **Critical Vulnerabilities**: Must fix immediately
- **High/Medium/Low Issues**: Prioritized findings
- **Dependency Report**: Vulnerable packages
- **Secrets Detection**: Exposed credentials
- **OWASP Compliance**: Category-by-category status
- **Remediation Guide**: How to fix each issue

## Severity Levels

| Severity | Response Time | Examples |
|----------|---------------|----------|
| Critical | Immediate | RCE, Auth bypass |
| High | 24-48 hours | Data exposure |
| Medium | 1-2 weeks | Limited exposure |
| Low | Next release | Hardening |

## Examples

```bash
# Full security audit
/audit

# Audit authentication code
/audit src/auth/

# Check only dependencies
/audit --deps

# Scan for secrets
/audit --secrets

# OWASP compliance check
/audit --owasp

# Pre-deployment audit
/audit --pre-deploy
```

## Common Findings

**Injection**:
```javascript
// ❌ Vulnerable
query(`SELECT * FROM users WHERE id = ${userId}`)

// ✅ Safe
query('SELECT * FROM users WHERE id = ?', [userId])
```

**Exposed Secrets**:
```javascript
// ❌ Vulnerable
const API_KEY = 'sk_live_abc123'

// ✅ Safe
const API_KEY = process.env.API_KEY
```

## Time

Typical completion: **3-10 minutes** depending on codebase size

## Next Steps

After `/audit` completes:
1. Address critical vulnerabilities immediately
2. Plan fixes for high-severity issues
3. Run dependency updates: `npm audit fix`
4. Rotate any exposed secrets
5. Re-audit to verify fixes

## Verification Commands

```bash
# Dependency audit
npm audit
pip-audit
govulncheck ./...

# Secrets scan
git secrets --scan

# Security headers check
curl -I https://your-app.com
```

---

**Executing command...**

Please invoke: `@security-auditor {args}`

The security-auditor will:
1. Perform reconnaissance of attack surface
2. Check OWASP Top 10 systematically
3. Scan dependencies for vulnerabilities
4. Detect exposed secrets
5. Generate remediation report
6. Provide executive summary
