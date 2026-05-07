# The Twelve-Factor App: X. Dev/Prod Parity

Source: https://12factor.net/dev-prod-parity

## Keep development, staging, and production as similar as possible

## The Three Historical Gaps

Traditionally, substantial differences existed between development and production environments:

- **Time gap**: Code could take days, weeks, or months to reach production
- **Personnel gap**: Developers wrote code while operations engineers deployed it
- **Tools gap**: Development stacks (Nginx, SQLite, OS X) differed from production (Apache, MySQL, Linux)

## The Twelve-Factor Solution

| Aspect | Traditional App | Twelve-Factor App |
|--------|-----------------|-------------------|
| Time between deploys | Weeks | Hours |
| Code authors vs deployers | Different people | Same people |
| Dev vs production | Divergent | As similar as possible |

## Backing Services Matter

Backing services (databases, queues, caches) require special attention. Developers should resist using different services locally versus in production — such as SQLite in development with PostgreSQL in production. Incompatibilities between services cause failures in production despite passing local tests.

## Modern Solutions

Contemporary tools make dev/prod parity achievable:
- Package managers (Homebrew, apt-get)
- Provisioning tools (Chef, Puppet)
- Containerization (Docker, Vagrant)

All application deployments should use identical service types and versions.
