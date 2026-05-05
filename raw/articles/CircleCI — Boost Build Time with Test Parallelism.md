# CircleCI — How to Boost Build Time With Test Parallelism

**Source:** https://www.amio.io/blog/circleci---how-to-boost-build-time-with-test-parallelism
**Author:** Matous Kucera

## Overview

How Amio reduced integration test build time from ~15 min to ~9 min using CircleCI test parallelism with Gradle/Grails.

## Setup

The `parallelism` key specifies how many independent containers execute job steps. Values >1 enable parallel execution. But setting parallelism alone runs ALL tests on each container — need splitting.

## CircleCI CLI Commands

**Glob test files:**
```bash
circleci tests glob "src/integration-test/**/*.groovy"
```

**Split by timing:**
```bash
circleci tests glob "src/integration-test/**/*.groovy" | circleci tests split --split-by=timings
```

`--split-by=timings` uses CircleCI's historical timing data to distribute tests evenly. Container indexing is automatic.

Example distribution:
- Container 0: Test1.groovy, Test3.groovy
- Container 1: Test2.groovy, Test4.groovy, Test5.groovy

## Gradle Integration

Pass split results as parameter:

```bash
./gradlew check -PtestFilter="`circleci tests glob "src/integration-test/**/*.groovy" | circleci tests split --split-by=timings`"
```

In `build.gradle`:
```groovy
integrationTest {
  if (project.hasProperty("testFilter")) {
    List<String> props = project.getProperties().get("testFilter").split("\\s+")
    props.each {
      include(it.replace("src/integration-test/groovy/com/", "**/").replace(".groovy", ".class"))
    }
  }
}
```

## Result

Build time: ~15 min → ~9 min
