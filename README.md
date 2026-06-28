<p align="center">
  <strong>English</strong> | <a href="README_ZH.md">中文</a>
</p>

# Vibe Coding Launch Security Checklist

> Before an AI-built MVP meets real users, ask the security questions that can prevent account abuse, data leaks, payment mistakes, content incidents, runaway cloud bills, and AI prompt exposure.

**Vibe Coding Launch Security Checklist** is an AI-readable pre-launch security checklist for MVPs built with vibe coding, web coding, low-code tools, and AI-assisted development.

It is made for founders, product owners, operators, indie hackers, and AI agents who need to answer one urgent question before launch:

> "This product works. Is it safe enough to face real users?"

## Why This Exists

Vibe coding makes it possible to ship a working product faster than ever. But a product that works locally can still fail badly in public:

- SMS verification can be abused until the bill explodes.
- User-generated avatars, nicknames, comments, and posts can create moderation or legal incidents.
- Payment amounts, order status, or user roles can be tampered with from the frontend.
- A normal user may see another user's data by changing an ID.
- An AI assistant may leak its system prompt, internal rules, or sensitive context.
- Admin panels may launch without MFA, role-based access, or audit logs.
- Backups may exist but never have been restored.
- Cloud services may have no budget alerts, rate limits, or emergency shutdown path.

This project turns those risks into a practical launch-readiness checklist that non-engineers and AI tools can both use.

## Highlights

- **20 security domains and 100 checklist items**  
  Covers login, permissions, input handling, Web, apps, mini programs, AI, UGC, payments, privacy, cloud services, backups, APIs, admin panels, monitoring, release safety, legal risk, incident response, supply chain, and user-facing safety boundaries.

- **Designed for people who do not write code**  
  Every item includes plain-language checks and questions to ask a developer or AI coding assistant.

- **Focused on real vibe coding launch risks**  
  Goes beyond traditional web vulnerabilities and includes AI chat, prompt leakage, SMS cost abuse, content moderation, cloud billing, payment callbacks, admin operations, rollback, and incident handling.

- **AI-readable by design**  
  The core checklist lives in [`data/checklist.json`](data/checklist.json). The web page can copy filtered JSON, Markdown summaries, and AI review prompts for ChatGPT, Codex, Claude, or other agents.

- **Static and easy to deploy**  
  No backend required. Deploy to GitHub Pages, Vercel, Netlify, or any static host.

## Live Demo

```text
https://lay-quq.github.io/vibe-coding-launch-security-checklist/
```

Run locally:

```bash
npm run build
npm run serve
```

Then open the local URL printed by the terminal.

## Who Should Use This

Use this checklist if you are:

- Building an MVP with AI tools such as Cursor, Claude, Codex, Bolt, Lovable, v0, or similar products.
- Preparing to expose a demo to real users.
- Launching a fan community, AI companion, content platform, tool site, mini program, SaaS dashboard, or mobile app.
- Responsible for a product that has no dedicated security engineer.
- Asking an AI agent to review whether your project is ready for public launch.

## Not an Exploit Guide

This project intentionally avoids attack instructions. It keeps only the information a product owner needs to recognize and reduce risk:

- Why the issue is dangerous.
- How a non-technical person can perform a basic check.
- What to ask a developer or AI assistant.
- What industry practice usually looks like.
- Which red flags mean the product should not launch yet.

## Checklist Data Structure

Each checklist item is structured for both humans and AI agents:

```json
{
  "id": "auth-001",
  "category_id": "auth",
  "priority": "P0",
  "severity": "high",
  "title": "Weak passwords and credential stuffing",
  "risk": "User accounts or admin accounts may be attacked through repeated login attempts...",
  "nontechnical_check": "Try common weak-password scenarios and review whether login failure is rate limited...",
  "ask_dev_or_ai": "Are failed logins rate limited by account, IP, and device?",
  "best_practice": "Use salted password hashing, rate limits, MFA for sensitive accounts...",
  "red_flags": ["Unlimited password attempts"],
  "tags": ["login", "password", "mfa"]
}
```

Priority levels:

- `P0`: Must be handled before launch.
- `P1`: Should be handled before launch, or must have a clear compensating control.
- `P2`: Can be scheduled shortly after launch, but should not be ignored long term.

## AI Review Prompt

The web page includes a one-click AI review prompt. You can also use this template directly:

```text
You are a senior application security and product risk reviewer. Use data/checklist.json to review this vibe coding MVP.

Product information:
- Product name:
- Product URL or repository:
- Product type:
- Target users:
- Current stage:
- Review goal:

Review requirements:
1. Do not give generic comments. Base findings on observable evidence.
2. For each finding, include: issue, evidence, impact, recommendation, priority, related checklist item id, and confidence.
3. If evidence is missing, list what needs to be checked instead of assuming the product is safe.
4. Prioritize P0 issues and anything that could cause data leakage, financial loss, content incidents, runaway cloud costs, or admin takeover.
5. If reviewing a code repository, first locate real user flows, backend APIs, admin panels, configuration, and third-party services. Do not only inspect the UI.
```

## Project Structure

```text
.
├── index.html                   # Static web app
├── data/
│   └── checklist.json            # AI-readable security checklist data
├── scripts/
│   └── generate-checklist.mjs     # Checklist data generator
├── package.json
├── LICENSE
├── README.md                     # English README
└── README_ZH.md                  # Chinese README
```

## Development

```bash
npm run build
npm run validate
npm run serve
```

## Reference Baselines

The checklist adapts industry guidance for MVP and vibe coding launch scenarios:

- [OWASP ASVS](https://owasp.org/www-project-application-security-verification-standard/)
- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [OWASP Top 10](https://owasp.org/Top10/2021/)
- [OWASP API Security Top 10](https://owasp.org/API-Security/editions/2023/en/0x00-header/)
- [OWASP File Upload Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/File_Upload_Cheat_Sheet.html)
- [OWASP LLM Top 10](https://owasp.org/www-project-top-10-for-large-language-model-applications/)
- [NIST SP 800-63B](https://pages.nist.gov/800-63-4/sp800-63b.html)
- [CISA Secure by Design](https://www.cisa.gov/securebydesign)

## License

MIT
