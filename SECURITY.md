# Security Policy

## Reporting a vulnerability

If you believe you've found a security issue in a NovraScale-owned repository, a NovraScale-operated website, or a website NovraScale builds and manages for a client, please report it privately.

**Do not open a public GitHub issue for security reports.**

**Email:** matt@novrascale.com
**Subject line:** `[SECURITY] <one-line summary>`

Please include:

- A description of the issue and its impact.
- Steps to reproduce (URLs, payloads, screenshots, or a minimal proof-of-concept).
- The affected repo, domain, or endpoint.
- Your name and how you'd like to be credited (or "anonymous").

## What to expect

- **Acknowledgement:** within 3 business days.
- **Triage + severity assessment:** within 7 business days.
- **Fix timeline:** communicated after triage. Critical issues (auth bypass, RCE, data exposure) are prioritized immediately.
- **Disclosure:** coordinated. We'll agree on a public disclosure window with the reporter once a fix is deployed.

## Scope

**In scope**

- Any repository under the [`NovraScale`](https://github.com/NovraScale) GitHub organization.
- `novrascale.com` and its subdomains.
- Client sites built and hosted by NovraScale, where the vulnerability is in code or configuration NovraScale controls.

**Out of scope**

- Third-party services we integrate with (report those to the respective vendor).
- Client-controlled content (CMS text, uploaded media) on client sites.
- Findings that require physical access, social engineering of NovraScale staff, or already-disclosed CVEs on managed infrastructure.
- Best-practice suggestions with no demonstrated impact (missing headers on non-sensitive endpoints, verbose banners, etc.) — welcome as regular feedback, not security reports.

## Safe harbor

We will not pursue or support legal action against researchers who:

1. Make a good-faith effort to comply with this policy.
2. Do not intentionally access, modify, or destroy data beyond what is minimally necessary to demonstrate the issue.
3. Do not disrupt or degrade our services or our clients' services.
4. Give us reasonable time to remediate before public disclosure.

## Our automated posture

Reporting is the human channel. In parallel, we run GitHub-native supply-chain security (Dependabot alerts, dependency updates, and secret-scanning push protection) across our repositories, so known-vulnerable dependencies and committed credentials are caught automatically.

Thanks for helping keep NovraScale and our clients safe.
