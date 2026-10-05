# Security Policy

The 10xGraph maintainers take the security of our state-graph runtime, checkpointing layers, and self-hosted production servers very seriously. We appreciate the responsible disclosure of any security vulnerabilities.

---

## Supported Versions

Only the latest active minor release receives official security patches and updates.

| Version | Supported |
|---|---|
| 0.9.x | ✅ Yes |
| < 0.9.0 | ❌ No |

---

## Reporting a Vulnerability

**Please do NOT report security vulnerabilities through public GitHub issues.**

If you believe you have discovered a vulnerability, security flaw, or privilege escalation vector in any 10xGraph repository:

1. **GitHub Private Vulnerability Reporting (Preferred)**:
   Navigate to the **Security** tab of the relevant repository and click **"Report a vulnerability"** to submit an advisory draft directly to the maintainers.

2. **Email Security Team**:
   Send an encrypted or detailed report to:
   **security@10xgraph.com**

### What to Include in Your Report:

- **Component**: Affected module or package (e.g., `10xgraph.server`, `10xgraph.checkpoint.redis`, `10xgraph.rbac`).
- **Description**: Summary of the vulnerability and its potential impact.
- **Reproduction**: Step-by-step instructions or minimal Python reproduction script.
- **Proposed Fix**: Any suggested patch or remediation (if available).

---

## Response & Disclosure Timeline

- **Initial Response**: Within **48 hours** of receiving your report, a maintainer will acknowledge receipt and begin triage.
- **Assessment**: Within **5 business days**, we will confirm or clarify the severity and impact.
- **Remediation**: We target releasing a security patch and CVE advisory within **14 calendar days** of confirmation.
- **Public Disclosure**: Coordinated public disclosure will take place simultaneously with or shortly after the release of the patched version.

---

## Security Best Practices for Production Deployments

When running 10xGraph in production environments:

1. **Enforce Per-Tool RBAC**: Always annotate sensitive tools with explicit permission scopes (`@tool(permissions=["..."])`).
2. **Secure State Storage**: Enable TLS and strong authentication passwords for Redis and PostgreSQL backends.
3. **Rotate JWT Signing Keys**: Use asymmetric keys (`RS256` or `EdDSA`) with automated key rotation for production servers.
4. **Isolate Sandboxed Execution**: For arbitrary Python execution tools, run workers in isolated containerized environments (e.g. gVisor, Docker, or Firecracker microVMs).
5. **Rate Limiting**: Protect HTTP and SSE streaming endpoints behind API gateways or reverse proxies with rate limiting enabled.
