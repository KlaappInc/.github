# Security Policy

This is the organization-wide default policy for **KlaappInc**. It applies to
every repository unless a repo defines its own `SECURITY.md`.

## Reporting a vulnerability

Please **do not** open a public issue for security problems.

- Email **security@klaapp.io** with a description, affected repo/service, and
  reproduction steps.
- Or, on a per-repo basis, use **GitHub → Security → Report a vulnerability**
  (private vulnerability reporting) when enabled.

We aim to acknowledge reports within **72 hours** and to provide a remediation
timeline after triage. Please give us a reasonable disclosure window before going public.

## Supported versions

Only the latest released version of each service/app is supported. Releases are
cut via release-please; see the repo's `CHANGELOG.md` and GitHub Releases.

## Handling of secrets

- Secrets never belong in the repository. Use the platform secret store
  (Cloudflare `wrangler secret put`, GitHub Actions secrets, EAS secrets).
- Pushes and PRs are scanned by **gitleaks** (and native secret scanning +
  push protection on public repos). A flagged secret must be **rotated**, not just removed.
