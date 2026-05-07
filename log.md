# Log

*Append-only. Format: `## [YYYY-MM-DD] <operation> | <title>`*

## [2026-05-04] init | vault created

## [2026-05-04] ingest | The Grug Brained Developer
Pages created: wiki/sources/the-grug-brained-developer.md, wiki/concepts/complexity.md, wiki/concepts/locality-of-behavior.md, wiki/concepts/chestertons-fence.md, wiki/concepts/fold.md, wiki/concepts/testing-philosophy.md, wiki/domains/software-development.md

## [2026-05-04] ingest | CI & flaky tests batch (5 articles)
Pages created: wiki/sources/successfully-merging-1000-developers.md, wiki/sources/keeping-developers-happy-fast-ci.md, wiki/sources/improving-productivity-flaky-test-management.md, wiki/sources/probabilistic-flakiness.md, wiki/sources/flaky-tests-at-google.md, wiki/concepts/flaky-tests.md, wiki/concepts/merge-queue.md
Pages updated: wiki/concepts/testing-philosophy.md (flaky tests section), wiki/domains/software-development.md (CI section)

## [2026-05-04] ingest | 69 articles (CI, testing quality, tooling batch)
Pages created: 69 source summaries in wiki/sources/; 6 new concept pages (CI Pipeline Speed, Test Coverage, Mutation Testing, Test Linting, Snapshot Testing, Developer Experience)
Pages updated: wiki/concepts/flaky-tests.md (tooling landscape, retry math, cascade data), wiki/concepts/merge-queue.md (stacked PRs, GitHub MQ limits, wrong-commit incident), wiki/concepts/testing-philosophy.md (snapshots, pre-commit, Vitest, DOM queries), wiki/domains/software-development.md (CI hierarchy, test quality, DX)
Clusters: flaky test tooling (17), merge queue (4), test coverage (5), CI speed (16), mutation testing (5), test linting (7), snapshot testing (3), testing standards/tools (5), developer experience (7)

## [2026-05-04] ingest | Your Brain on ChatGPT — Cognitive Debt (PDF)
Pages created: wiki/sources/Your Brain on ChatGPT — Cognitive Debt.md, wiki/concepts/Cognitive Debt.md
Pages updated: wiki/domains/Dev Setup & Tools.md (cognitive cost of AI tool use section)

## [2026-05-04] ingest | raw/notes (bulk — all notes)
Pages created: wiki/self/overview.md, wiki/self/goals.md, wiki/self/health.md, wiki/people/mahan.md, wiki/domains/barcelona-life.md, wiki/domains/finance.md, wiki/domains/entertainment.md, wiki/domains/home.md, wiki/domains/dev-setup.md, wiki/domains/dnd.md, wiki/sources/measure-what-matters.md, wiki/sources/mcp-explainer.md
Skipped (operational/one-off): visa docs, apartment docs, letter drafts, work messages, flight tickets, document scans, empty notes

## [2026-05-07] cleanup | removed personal notes
Deleted: raw/notes/ (entire directory), wiki/self/, wiki/people/, wiki/domains/Barcelona Life.md, wiki/domains/D&D Campaigns & Characters.md, wiki/domains/Entertainment.md, wiki/domains/Finance.md, wiki/domains/Home.md, wiki/sources/Measure What Matters — John Doerr.md
Kept: all research (raw/articles/, wiki/sources/, wiki/concepts/, wiki/domains/Software Development.md, wiki/domains/Dev Setup & Tools.md)

## [2026-05-07] ingest | 57 articles batch (MDN Security, OWASP 2021, web.dev Performance, Chrome DevTools Memory)
Added to raw/articles/:
MDN Security attacks (10): XSS, CSRF, Clickjacking, IDOR, Prototype Pollution, MITM, Phishing, SSRF, Subdomain Takeover, Supply Chain Attacks
MDN Security defenses (7): Same-Origin Policy, Mixed Content, TLS, Subresource Integrity, Certificate Transparency, Secure Contexts, User Activation
MDN Security authentication (5): Passkeys, Passwords, Session Management, OTP, Federated Identity
MDN Security practical guides (7): CSP Implementation, CORS Configuration, Cookie Configuration, MIME Type Verification, Referrer Policy, TLS Configuration, CORP
MDN Security threat modeling (1): Threat Modeling
OWASP 2021 (5): A06 Vulnerable Components, A07 Auth Failures, A08 Integrity Failures, A09 Logging Failures, A10 SSRF
web.dev Performance (16): User-Centric Metrics, LCP, CLS, INP, TTFB, FCP, TBT, Custom Metrics, Web Vitals, Stick to Compositor-Only Properties, Optimize LCP, Optimize CLS, Optimize INP, Getting Started Measuring Web Vitals, Defining Core Web Vitals Thresholds, Debug Layout Shifts
Chrome DevTools Memory (4): Fix Memory Problems, Memory Terminology, Heap Snapshots, Allocation Timeline
Other (2): ditdot JavaScript Memory Leaks, Interaction Design Foundation Adaptive vs Responsive Design
Skipped: sealights.io (404 after redirect), codingsans.com (402), sonarqube.org (no article content), restfulapi.net (403), OWASP 2021 A01-A05 (domain restriction), OWASP 2025 (404)

## [2026-05-07] ingest | 57 articles ingested (MDN Security, OWASP 2021, web.dev Performance, Chrome DevTools Memory)
Source summaries created (57 pages in wiki/sources/):
  MDN Security attacks: XSS, CSRF, Clickjacking, IDOR, Prototype Pollution, MITM, Phishing, SSRF, Subdomain Takeover, Supply Chain Attacks
  MDN Security defenses: Same-Origin Policy, Mixed Content, TLS, Subresource Integrity, Certificate Transparency, Secure Contexts, User Activation
  MDN Security authentication: Passkeys, Passwords, Session Management, OTP, Federated Identity
  MDN Security practical guides: CSP Implementation, CORS Configuration, Cookie Configuration, MIME Type Verification, Referrer Policy, TLS Configuration, CORP
  MDN Security threat modeling: Threat Modeling
  OWASP 2021: A06 Vulnerable Components, A07 Auth Failures, A08 Integrity Failures, A09 Logging Failures, A10 SSRF
  web.dev Performance: User-Centric Metrics, LCP, CLS, INP, TTFB, FCP, TBT, Custom Metrics, Web Vitals, Stick to Compositor-Only Properties, Optimize LCP, Optimize CLS, Optimize INP, Getting Started Measuring Web Vitals, Defining Core Web Vitals Thresholds, Debug Layout Shifts
  Chrome DevTools Memory: Fix Memory Problems, Memory Terminology, Heap Snapshots, Allocation Timeline
  Other: JavaScript Memory Leaks (ditdot), Adaptive vs Responsive Design (IDF)
New domain pages: wiki/domains/Web Security.md, wiki/domains/Web Performance.md
New concept pages: wiki/concepts/Core Web Vitals.md, wiki/concepts/JavaScript Memory Management.md, wiki/concepts/Responsive Design.md
Index updated: added 3 concepts, 2 domains

## [2026-05-07] ingest | 19 articles batch (12factor.net, Typecraft, Evil Martians, Infrequently Noted, freeCodeCamp, Harvard)
Added to raw/articles/:
  12factor.net (13): index + all 12 individual factors (Codebase through Admin Processes)
  Typecraft — When Technical Debt is the Right Answer
  Evil Martians — Better Web Video with AV1 Codec
  Infrequently Noted — If Not React Then What
  freeCodeCamp — Learn System Design Principles
  Harvard — Exercising Leadership Foundational Principles
Index updated: 19 new raw article entries

## [2026-05-07] ingest | When Technical Debt is the Right Answer — Typecraft
Pages created: wiki/sources/Typecraft — When Technical Debt is the Right Answer.md, wiki/concepts/Technical Debt.md
Pages updated: wiki/domains/Software Development.md (technical debt section)

## [2026-05-07] ingest | Better Web Video with AV1 Codec — Evil Martians
Pages created: wiki/sources/Evil Martians — Better Web Video with AV1 Codec.md
Pages updated: wiki/domains/Web Performance.md (media optimization section)

## [2026-05-07] ingest | If Not React, Then What? — Infrequently Noted
Pages created: wiki/sources/Infrequently Noted — If Not React Then What.md, wiki/concepts/Frontend Architecture.md
Pages updated: wiki/domains/Software Development.md (frontend section expanded)

## [2026-05-07] ingest | The Twelve-Factor App — 12factor.net
Pages created: wiki/sources/12factor.net — The Twelve-Factor App.md, wiki/concepts/Twelve-Factor App.md
Pages updated: wiki/domains/Software Development.md (application architecture section added)
