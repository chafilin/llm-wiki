# The Twelve-Factor App: V. Build, Release, Run

Source: https://12factor.net/build-release-run

## Strictly separate build and run stages

A codebase transforms into a production deployment through three distinct phases:

## The Three Stages

**Build Stage**
Converts a code repository into an executable package called a build. It retrieves vendor dependencies and compiles binaries and assets based on a specific code commit.

**Release Stage**
Takes the build output and combines it with the deployment's current configuration. The resulting release contains both components and stands ready for immediate execution.

**Run Stage (Runtime)**
Executes the application by launching specified application processes against a selected release.

## Key Principles

"The twelve-factor app uses strict separation between the build, release, and run stages." Code changes cannot occur during runtime without a new build cycle.

## Release Management

Releases receive unique identifiers — either timestamps like `2011-04-06-20:32:17` or incrementing numbers such as `v100`. Tools like Capistrano facilitate rollbacks to previous releases. Releases remain immutable once created (append-only ledger).

## Complexity Distribution

The build stage tolerates greater complexity since developers actively monitor it. The run stage should minimize moving parts because runtime failures can occur unattended, potentially causing issues outside business hours.
