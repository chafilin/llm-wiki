# The Twelve-Factor App: I. Codebase

Source: https://12factor.net/codebase

## One codebase tracked in revision control, many deploys

A twelve-factor application must be maintained in a version control system like Git, Mercurial, or Subversion.

A **codebase** refers to either:
- Any single repository in centralized version control systems (like Subversion)
- Any set of repositories sharing a root commit in decentralized systems (like Git)

## Key Principles

**One-to-One Codebase-to-App Relationship:**

- "If there are multiple codebases, it's not an app – it's a distributed system."
- Multiple applications sharing identical code violates twelve-factor principles; instead, shared code should be extracted into libraries and included via dependency management.

**Many Deploys from One Codebase:**

A **deploy** is a running application instance (production site, staging environment, or local developer copy). While the codebase remains consistent across all deploys, different versions may be active in each environment.

For example, developers may have uncommitted changes, staging may contain undeployed commits, and production runs a different version — yet all represent deploys of the same application.
