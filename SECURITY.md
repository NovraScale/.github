# Security Policy

## Reporting a vulnerability

If you believe you've found a security issue in a repository in this organization, a Brevard Booked website, or a website Brevard Booked builds and manages for a client, please report it privately. (Brevard Booked is a d/b/a of NovraScale LLC.)

**Do not open a public GitHub issue for security reports.**

**Email:** security@brevardbooked.com
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
- `brevardbooked.com` and its subdomains, including the client portal at `my.brevardbooked.com`.
- `novrascale.com` and its subdomains (they redirect to brevardbooked.com).
- Client sites built and hosted by Brevard Booked, where the vulnerability is in code or configuration we control.

**Out of scope**

- Third-party services we integrate with (report those to the respective vendor).
- Client-controlled content (CMS text, uploaded media) on client sites.
- Findings that require physical access, social engineering of our staff, or already-disclosed CVEs on managed infrastructure.
- Best-practice suggestions with no demonstrated impact (missing headers on non-sensitive endpoints, verbose banners, and similar). These are welcome as regular feedback, not security reports.

## Safe harbor

We will not pursue or support legal action against researchers who:

1. Make a good-faith effort to comply with this policy.
2. Do not intentionally access, modify, or destroy data beyond what is minimally necessary to demonstrate the issue.
3. Do not disrupt or degrade our services or our clients' services.
4. Give us reasonable time to remediate before public disclosure.

## Our automated posture

Reporting is the human channel. Alongside it, every commit runs a secret scan (gitleaks) before it can land, and dependency advisories are reviewed deliberately with `npm audit` on each shipping project rather than through automated update bots.

Thanks for helping keep Brevard Booked and our clients safe.
