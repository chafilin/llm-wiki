# Building an Effective Test Pipeline in a Service Oriented World

**Source:** https://medium.com/airbnb-engineering/building-an-effective-test-pipeline-in-a-service-oriented-world-6968c513c6bd
**Author:** Joey Ye
**Published:** February 4, 2020

## Context

Airbnb migrated from a Rails monolith to service-oriented architecture (SOA). The monolithic "Deep Integration Tests" CI approach couldn't scale: long runtimes, high flakiness from complex dependencies, hard local setup, difficult debugging, violated Test Pyramid, no CD-phase verification.

## New Two-Phase Pipeline

**CI (Continuous Integration):**
- Unit tests and shallow integration tests
- Uses BuildKite + Private Development environment
- Light, fast feedback

**CD (Continuous Delivery):**
- Deep integration tests on reduced scope
- Uses Spinnaker with Automatic Canary Analysis
- Deploys through Staging pre-production environment

## Test Pyramid Framework

1. **Unit Tests:** Business logic within services
2. **Shallow Integration Tests:** Individual service behavior with mocked dependencies (YAML fixture data, no real network calls)
3. **Deep Integration Tests:** Complex multi-service interactions (reduced quantity)

**Key principle:** "If a higher-level test spots an error and there's no lower-level test failing, you need to write a lower-level test." Push tests as far down the pyramid as feasible.

## Results

- Each service maintains its own pipeline → independent parallel testing
- Pyramid structure encourages smaller, more reliable tests
- Faster CI, quicker failure detection
- Multiple layers covering business logic, endpoints, and inter-service behavior
