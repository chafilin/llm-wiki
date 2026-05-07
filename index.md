# Index

*Updated by Claude on every ingest. Read this first when answering queries.*

## Concepts
| Page | Summary |
|------|---------|
| [[Complexity]] | The invisible accumulation of interdependencies that makes systems hard to change; central enemy of good software |
| [[Locality of Behavior]] | Put code on the thing that does the thing; prefer understanding-in-place over SoC file-splitting |
| [[Chesterton's Fence]] | Don't remove what you don't understand yet |
| [[FOLD]] | Fear of Looking Dumb — a complexity multiplier; senior devs naming it give others permission |
| [[Testing Philosophy]] | Integration tests are the sweet spot; write after prototyping; avoid mocks; regression test first on bugs; flaky test quarantine; snapshot discipline; pre-commit hooks |
| [[Flaky Tests]] | Non-deterministic tests; spectrum not binary; quarantine not delete; Google/Microsoft/Meta/Slack/Atlassian approaches; tooling landscape; retry math |
| [[Merge Queue]] | Serializes PRs through a predictive branch; catches soft conflicts; protects master-always-green invariant; stacked PRs problem; GitHub MQ limits |
| [[CI Pipeline Speed]] | Skip > select > parallelize > cache > optimize infrastructure; measure first; test selection; remote caching; Nx affected |
| [[Test Coverage]] | Patch coverage > project coverage; direction over position; quality gates; carryforward flags for monorepos |
| [[Mutation Testing]] | Tests the tests; StrykerJS incremental mode; TypeScript checker; weekly runs; ceiling from missing E2E support |
| [[Test Linting]] | ESLint rules for structural test bugs: expect-expect, no-conditional-expect, prefer-screen-queries, prefer-presence-queries, no-debugging-utils, no-large-snapshots |
| [[Snapshot Testing]] | Valid for error messages/AST/CSS-in-JS; never for full component trees; keep small and deterministic |
| [[Developer Experience]] | DX as business function; 10% principle; CI as a service (SRE); test ownership; Backstage software catalog; Soundcheck tech health |
| [[Cognitive Debt]] | Accumulation of cognitive disengagement from habitual LLM use; degrades memory, brain connectivity, ownership; compounds across sessions; germane load is what LLMs reduce most |

## Domains
| Page | Summary |
|------|---------|
| [[Software Development]] | Principles for building maintainable software; complexity-reduction as the through-line; CI hierarchy; test quality |
| [[Dev Setup & Tools]] | Apps (Things 3, Bear, Zed, Ghostty), AI tools, MCP notes |

## Sources
| Page | Raw file | Date |
|------|----------|------|
| [[The Grug Brained Developer]] | raw/articles/The Grug Brained Developer.md | 2026-05-04 |
| [[MCP — Model Context Protocol]] | raw/notes/MCP.md | 2026-05-04 |
| [[Successfully Merging the Work of 1000+ Developers]] | raw/articles/Successfully Merging the Work of 1000+ Developers.md | 2026-05-04 |
| [[Keeping Developers Happy with a Fast CI]] | raw/articles/Keeping Developers Happy with a Fast CI.md | 2026-05-04 |
| [[Improving Developer Productivity via Flaky Test Management]] | raw/articles/Improving Developer Productivity via Flaky Test Management.md | 2026-05-04 |
| [[Probabilistic Flakiness]] | raw/articles/Probabilistic Flakiness.md | 2026-05-04 |
| [[Flaky Tests at Google and How We Mitigate Them]] | raw/articles/Flaky Tests at Google and How We Mitigate Them.md | 2026-05-04 |
| [[Handling Flaky Tests at Scale — Slack]] | raw/articles/Handling Flaky Tests at Scale — Slack.md | 2026-05-04 |
| [[Balancing Safety and Velocity in CI-CD at Slack]] | raw/articles/Balancing Safety and Velocity in CI-CD at Slack.md | 2026-05-04 |
| [[Taming Test Flakiness — Atlassian]] | raw/articles/Taming Test Flakiness — Atlassian.md | 2026-05-04 |
| [[Understand and Manage Flaky Tests in Bitbucket Pipelines]] | raw/articles/Understand and Manage Flaky Tests in Bitbucket Pipelines.md | 2026-05-04 |
| [[The Unreasonable Effectiveness of Test Retries — Shopify]] | raw/articles/The Unreasonable Effectiveness of Test Retries — Shopify.md | 2026-05-04 |
| [[Quarantine a Flaky Test — GitLab MR]] | raw/articles/Quarantine a Flaky Test — GitLab MR.md | 2026-05-04 |
| [[Creating a Culture of Quality — Trivago]] | raw/articles/Creating a Culture of Quality — Trivago.md | 2026-05-04 |
| [[Datadog — Working with Flaky Tests]] | raw/articles/Datadog — Working with Flaky Tests.md | 2026-05-04 |
| [[CircleCI — Test Insights]] | raw/articles/CircleCI — Test Insights.md | 2026-05-04 |
| [[CircleCI — Fix Flaky Tests with Chunk]] | raw/articles/CircleCI — Fix Flaky Tests with Chunk.md | 2026-05-04 |
| [[Buildkite Test Engine]] | raw/articles/Buildkite Test Engine.md | 2026-05-04 |
| [[Cypress — Experimental Features]] | raw/articles/Cypress — Experimental Features.md | 2026-05-04 |
| [[Playwright — Test Sharding]] | raw/articles/Playwright — Test Sharding.md | 2026-05-04 |
| [[Vitest — Retry Config]] | raw/articles/Vitest — Retry Config.md | 2026-05-04 |
| [[Wix — jest-retry-all-hooks]] | raw/articles/Wix — jest-retry-all-hooks.md | 2026-05-04 |
| [[TestDino — Flaky Test Benchmark Report 2026]] | raw/articles/TestDino — Flaky Test Benchmark Report 2026.md | 2026-05-04 |
| [[TestDino — Playwright Flaky Tests]] | raw/articles/TestDino — Playwright Flaky Tests.md | 2026-05-04 |
| [[Introducing the Merge Queue — Shopify]] | raw/articles/Introducing the Merge Queue — Shopify.md | 2026-05-04 |
| [[Graphite — The First Stack-Aware Merge Queue]] | raw/articles/Graphite — The First Stack-Aware Merge Queue.md | 2026-05-04 |
| [[Trunk — Outgrowing GitHub Merge Queue]] | raw/articles/Trunk — Outgrowing GitHub Merge Queue.md | 2026-05-04 |
| [[Trunk — What Happens If a Merge Queue Builds on the Wrong Commit]] | raw/articles/Trunk — What Happens If a Merge Queue Builds on the Wrong Commit.md | 2026-05-04 |
| [[Beyond Numbers — Test Coverage Culture at Apollo]] | raw/articles/Beyond Numbers — Test Coverage Culture at Apollo.md | 2026-05-04 |
| [[Codecov — Why Patch Coverage Matters More]] | raw/articles/Codecov — Why Patch Coverage Matters More.md | 2026-05-04 |
| [[Codecov — Commit Status Checks]] | raw/articles/Codecov — Commit Status Checks.md | 2026-05-04 |
| [[Compass — Code Coverage and Carryforward Flags]] | raw/articles/Compass — Code Coverage and Carryforward Flags.md | 2026-05-04 |
| [[SonarQube — Introduction to Quality Gates]] | raw/articles/SonarQube — Introduction to Quality Gates.md | 2026-05-04 |
| [[Test Budget — Time Constrained CI Feedback — Shopify]] | raw/articles/Test Budget — Time Constrained CI Feedback — Shopify.md | 2026-05-04 |
| [[Spark Joy by Running Fewer Tests — Shopify]] | raw/articles/Spark Joy by Running Fewer Tests — Shopify.md | 2026-05-04 |
| [[Building an Effective Test Pipeline — Airbnb]] | raw/articles/Building an Effective Test Pipeline — Airbnb.md | 2026-05-04 |
| [[Pre-Submit UI Tests at Pinterest]] | raw/articles/Pre-Submit UI Tests at Pinterest.md | 2026-05-04 |
| [[Lessons Learned Migrating to Bazel — Wix]] | raw/articles/Lessons Learned Migrating to Bazel — Wix.md | 2026-05-04 |
| [[Turborepo Remote Cache — Mercari]] | raw/articles/Turborepo Remote Cache — Mercari.md | 2026-05-04 |
| [[How Remote Caching Decreased Publish Times by 80% — Vercel]] | raw/articles/How Remote Caching Decreased Publish Times by 80% — Vercel.md | 2026-05-04 |
| [[How GitLab Used Parallel CI-CD Jobs to Increase Productivity]] | raw/articles/How GitLab Used Parallel CI-CD Jobs to Increase Productivity.md | 2026-05-04 |
| [[GitLab — CI-CD Analytics]] | raw/articles/GitLab — CI-CD Analytics.md | 2026-05-04 |
| [[How We Reduced GitLab CI Pipeline Duration by 70% — PION]] | raw/articles/How We Reduced GitLab CI Pipeline Duration by 70% — PION.md | 2026-05-04 |
| [[CircleCI — Boost Build Time with Test Parallelism]] | raw/articles/CircleCI — Boost Build Time with Test Parallelism.md | 2026-05-04 |
| [[Speeding Up CircleCI for Nx Monorepo Using Nx Affected]] | raw/articles/Speeding Up CircleCI for Nx Monorepo Using Nx Affected.md | 2026-05-04 |
| [[Nx — Run Only Tasks Affected by a PR]] | raw/articles/Nx — Run Only Tasks Affected by a PR.md | 2026-05-04 |
| [[Knapsack Pro — Cypress Parallelization]] | raw/articles/Knapsack Pro — Cypress Parallelization.md | 2026-05-04 |
| [[Buildkite — Speed Up Builds with bktec]] | raw/articles/Buildkite — Speed Up Builds with bktec.md | 2026-05-04 |
| [[Bazel — Who's Using Bazel]] | raw/articles/Bazel — Who's Using Bazel.md | 2026-05-04 |
| [[Mutation Testing Our JavaScript SDKs — Sentry]] | raw/articles/Mutation Testing Our JavaScript SDKs — Sentry.md | 2026-05-04 |
| [[StrykerJS — Announcing Incremental Mode]] | raw/articles/StrykerJS — Announcing Incremental Mode.md | 2026-05-04 |
| [[StrykerJS — Incremental Mode Docs]] | raw/articles/StrykerJS — Incremental Mode Docs.md | 2026-05-04 |
| [[StrykerJS — TypeScript Checker]] | raw/articles/StrykerJS — TypeScript Checker.md | 2026-05-04 |
| [[StrykerJS — Incremental Mode (GitHub)]] | raw/articles/StrykerJS — Incremental Mode (GitHub).md | 2026-05-04 |
| [[eslint-plugin-jest — expect-expect Rule]] | raw/articles/eslint-plugin-jest — expect-expect Rule.md | 2026-05-04 |
| [[jest — no-conditional-expect (OXC)]] | raw/articles/jest — no-conditional-expect (OXC).md | 2026-05-04 |
| [[eslint-plugin-playwright — no-conditional-expect]] | raw/articles/eslint-plugin-playwright — no-conditional-expect.md | 2026-05-04 |
| [[eslint-plugin-testing-library — prefer-screen-queries]] | raw/articles/eslint-plugin-testing-library — prefer-screen-queries.md | 2026-05-04 |
| [[eslint-plugin-testing-library — prefer-presence-queries]] | raw/articles/eslint-plugin-testing-library — prefer-presence-queries.md | 2026-05-04 |
| [[eslint-plugin-testing-library — no-debugging-utils]] | raw/articles/eslint-plugin-testing-library — no-debugging-utils.md | 2026-05-04 |
| [[eslint-plugin-jest — no-large-snapshots Rule]] | raw/articles/eslint-plugin-jest — no-large-snapshots Rule.md | 2026-05-04 |
| [[Effective Snapshot Testing — Kent C. Dodds]] | raw/articles/Effective Snapshot Testing — Kent C. Dodds.md | 2026-05-04 |
| [[The Case Against React Snapshot Testing — ezCater]] | raw/articles/The Case Against React Snapshot Testing — ezCater.md | 2026-05-04 |
| [[Making the Most of Snapshot Testing]] | raw/articles/Making the Most of Snapshot Testing.md | 2026-05-04 |
| [[GitLab — Frontend Testing Standards]] | raw/articles/GitLab — Frontend Testing Standards.md | 2026-05-04 |
| [[GitLab — Unit Test Reports]] | raw/articles/GitLab — Unit Test Reports.md | 2026-05-04 |
| [[Vitest — Coverage Config]] | raw/articles/Vitest — Coverage Config.md | 2026-05-04 |
| [[Vitest — Features]] | raw/articles/Vitest — Features.md | 2026-05-04 |
| [[Running Jest Tests Before Each Git Commit]] | raw/articles/Running Jest Tests Before Each Git Commit.md | 2026-05-04 |
| [[Atlassian Developer Experience — LinearB]] | raw/articles/Atlassian Developer Experience — LinearB.md | 2026-05-04 |
| [[Buildkite — Test Ownership Docs]] | raw/articles/Buildkite — Test Ownership Docs.md | 2026-05-04 |
| [[Buildkite — Applying SRE Principles to CI-CD]] | raw/articles/Buildkite — Applying SRE Principles to CI-CD.md | 2026-05-04 |
| [[Spotify Backstage — Software Catalog]] | raw/articles/Spotify Backstage — Software Catalog.md | 2026-05-04 |
| [[Spotify Backstage — Soundcheck]] | raw/articles/Spotify Backstage — Soundcheck.md | 2026-05-04 |
| [[Buildkite — Case Studies]] | raw/articles/Buildkite — Case Studies.md | 2026-05-04 |
| [[Frontend Case Studies Index]] | raw/articles/Frontend Case Studies Index.md | 2026-05-04 |
| [[Your Brain on ChatGPT — Cognitive Debt]] | raw/articles/2506.08872v2.pdf | 2026-05-04 |

## Synthesis
| Page | Question | Date |
|------|----------|------|
