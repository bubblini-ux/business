# Security Policy

## Supported Versions

Only the latest state of the protected `main` branch is actively maintained and supported with security updates.

| Branch / Version | Supported          |
| :--------------- | :----------------- |
| `main` (0.1.x)   | :white_check_mark: |
| Legacy branches  | :x:                |

---

## Security Best Practices

1. **Secrets & Credentials Management**
   - Never commit `.env` files, API tokens, database passwords, or payment gateway keys (`STRIPE_SECRET_KEY`, `STRIPE_WEBHOOK_SECRET`).
   - Use [`.env.example`](./.env.example) strictly for placeholder templates.
2. **Payment Compliance**
   - All payment flows must use tokenized client SDKs (such as Stripe Elements / Stripe Checkout) so raw cardholder data never touches application servers.
   - Verify webhook signatures on every incoming payment event.
3. **Branch Protection**
   - The `main` branch enforces protection against force-pushes and accidental deletion.

---

## Reporting a Vulnerability

If you discover a security vulnerability or accidental credential exposure within this repository:

1. **Do not** open a public GitHub issue containing sensitive exploit details.
2. Report the issue privately via GitHub Security Advisories (`Security` tab -> `Report a vulnerability`) or contact the repository owner (`@bubblini-ux`) directly.
3. Include steps to reproduce, affected files/components, and potential impact.
