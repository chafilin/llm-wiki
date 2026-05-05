# eslint-plugin-jest — no-large-snapshots Rule

**Source:** https://github.com/LitoMore/eslint-plugin-jest/blob/main/docs/rules/no-large-snapshots.md

## Rule

`jest/no-large-snapshots`

## What It Enforces

Limits snapshot size to keep them reviewable and maintainable. Default maximum: **50 lines** per snapshot.

"A stored snapshot is only as good as its review and as such keeping it short, sweet, and readable is important to allow for thorough reviews."

## Why Large Snapshots Are Problematic

- Impede code review quality
- Make version control diffs hard to assess
- Encourage rubber-stamping updates without real review

## Configuration Options

```json
{
  "jest/no-large-snapshots": ["warn", {
    "maxSize": 50,
    "inlineMaxSize": 10,
    "allowedSnapshots": {
      "/path/to/file.test.js": ["snapshot name", /regex/]
    }
  }]
}
```

- `maxSize`: line limit for external `.snap` files (default: 50)
- `inlineMaxSize`: line limit for inline snapshots (defaults to `maxSize`)
- `allowedSnapshots`: per-file allowlist by snapshot name or regex

## Note

Requires `ecmaVersion: 2015` in parser options (snapshots use template literals).
