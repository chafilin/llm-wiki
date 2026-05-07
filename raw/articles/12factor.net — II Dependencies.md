# The Twelve-Factor App: II. Dependencies

Source: https://12factor.net/dependencies

## Explicitly declare and isolate dependencies

"A twelve-factor app never relies on implicit existence of system-wide packages." Instead, applications must declare all dependencies explicitly through a dependency declaration manifest and use isolation tools during execution to prevent implicit system dependencies from being used.

## Key Requirements

Two essential practices:

1. **Dependency Declaration** — Explicitly list all required libraries using language-specific tools
2. **Dependency Isolation** — Use tools to ensure only declared dependencies are available

Examples across different languages:
- Ruby: Bundler uses `Gemfile` for declaration and `bundle exec` for isolation
- Python: Pip handles declaration while Virtualenv manages isolation
- C: Autoconf for declaration with static linking for isolation

## Benefits for Development

Explicit dependency declaration streamlines onboarding for new developers. They need only the language runtime and dependency manager installed, then can run a deterministic build command (like `bundle install` or `lein deps`) to establish their environment.

## System Tools and Dependencies

Applications should not assume system tools like ImageMagick or curl are available. "If the app needs to shell out to a system tool, that tool should be vendored into the app" to ensure consistent behavior across all deployment environments.
