# Nx — Run Only Tasks Affected by a PR

**Source:** https://nx.dev/docs/features/ci-features/affected

## Core Concept

`nx affected` identifies and executes tasks exclusively on projects impacted by your changes. As the documentation explains, "re-testing, re-building, and re-linting all projects becomes too slow" in growing workspaces.

## How It Determines Affected Projects

1. Uses Git to identify modified files in your PR
2. Consults the project graph to determine which projects contain those files
3. Identifies any projects dependent on the modified ones

## Primary Commands

```shell
nx affected -t <task>
nx affected -t test
nx graph --affected
```

## CI Configuration

```shell
# Custom base and head
nx affected -t build --base=origin/main --head=$PR_BRANCH_NAME
nx affected -t build --base=origin/main~1 --head=origin/main

# Via environment variables
NX_BASE=origin/main~1
NX_HEAD=origin/main
```

## Dependency Update Handling

```json
// nx.json
{
  "pluginsConfig": {
    "@nx/js": {
      "projectsAffectedByDependencyUpdates": "auto"
    }
  }
}
```

## Additional Notes

- Patterns in `.gitignore` and `.nxignore` are excluded from affected analysis
- Use `--files` flag to specify changed files manually (non-Git scenarios)
- Best paired with remote caching and distributed task execution
