# Creating a Culture of Quality

**Source:** https://tech.trivago.com/post/2015-08-31-culture_of_quality
**Author:** Jan Van Thoor
**Date:** August 31, 2015

## The Problem: "Trunk Is Broken"

Developers could push directly to trunk without running tests → staging and production used as test environments.

## Initial Solutions (Didn't Work)

Weekly release cycle, code freezes, dedicated QA resources, release managers. Created stress without improving stability — the process wasn't the real problem.

## 2012 Relaunch

Complete rebuild with Symfony 2 and SPA. But rapid team growth + explosion of A/B tests (5-10 → 100+) caused the same problems to resurface.

## What Actually Worked

**Tooling & process:**
- CI servers with automated testing
- Git migration from SVN
- Standardized dev environments (Vagrant)
- Acceptance testing frameworks
- Service-oriented architecture

**Culture (the real lever):**
- Team ownership of code quality
- Agile processes and cross-disciplinary teams
- Feature branch development with peer reviews
- Core competency guilds
- Balancing speed-to-market vs. sustainable development

## Core Lesson

> "Tooling and processes will continue to change, but the culture is here to stay!"

Success required moving from individual contributor focus → team-based ownership. Environment where developers feel trusted and empowered to make quality decisions.

**The tension:** Trivago's startup mentality demands rapid delivery, yet quality must be maintained. Neither side wins completely — the key is navigating the balance consciously.
