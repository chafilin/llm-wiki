# Personal Knowledge Vault — Schema

## What this is

A personal wiki maintained by Claude. Raw sources go in `raw/`, the wiki lives in `wiki/`. I source and direct; Claude writes and maintains.

## Directory layout

```
raw/
  articles/     web clips, long reads, essays
  notes/        voice memos, quick thoughts, rough notes
  journal/      dated journal entries
  assets/       downloaded images referenced by raw docs

wiki/
  self/         who I am: values, goals, patterns, recurring themes
  people/       people who matter to me or I'm studying
  concepts/     mental models, ideas, frameworks
  domains/      areas of life: health, career, relationships, money, creativity
  sources/      one summary page per ingested raw doc
  synthesis/    analyses, comparisons, explorations born from queries

index.md        full catalog of wiki pages (Claude updates on every ingest)
log.md          append-only activity log (Claude appends on every operation)
```

## Page formats

### Source summary (`wiki/sources/`)
```markdown
---
title: <title>
type: source
raw: <path to raw file>
date_ingested: YYYY-MM-DD
tags: []
---

## Summary
2-4 sentence overview.

## Key takeaways
- Bullet list of the most important points.

## Connections
Links to wiki pages this source touches: [[page]], [[page]]

## Quotes
Notable verbatim quotes, sparingly.
```

### Entity page (`wiki/self/`, `wiki/people/`, `wiki/domains/`)
```markdown
---
title: <name>
type: entity
updated: YYYY-MM-DD
sources: <count>
---

## Overview
Current synthesis. Revised with every new source. Not a history — a current picture.

## Key claims
- Backed assertions with [[source]] citations.

## Open questions
Things I still don't know or haven't resolved.

## Connections
[[related pages]]
```

### Concept page (`wiki/concepts/`)
```markdown
---
title: <concept name>
type: concept
updated: YYYY-MM-DD
---

## Definition
Clear, opinionated definition in my terms.

## Why it matters
Concrete relevance to my life.

## Examples
Real instances from sources or experience.

## Connections
[[related pages]]
```

### Synthesis page (`wiki/synthesis/`)
```markdown
---
title: <title>
type: synthesis
date: YYYY-MM-DD
---

## Question
What prompted this.

## Answer
The synthesis itself.

## Sources consulted
[[pages]] used to generate this.
```

## Workflows

### Ingest
1. Read the raw source completely.
2. Discuss key takeaways with Vova before writing.
3. Write a source summary page in `wiki/sources/`.
4. Update or create entity/concept/domain pages the source touches.
5. Update `index.md` — add the new source and any new wiki pages.
6. Append to `log.md`: `## [YYYY-MM-DD] ingest | <title>`
7. Report: pages created, pages updated, any contradictions found.

### Query
1. Read `index.md` to find relevant pages.
2. Read those pages.
3. Synthesize an answer with [[citations]].
4. If the answer is non-trivial, offer to file it as a synthesis page.
5. Append to `log.md`: `## [YYYY-MM-DD] query | <question summary>`

### Lint
1. Scan all wiki pages for: contradictions, stale claims, orphan pages (no inbound links), concepts mentioned but lacking their own page, missing cross-references.
2. Report findings and ask Vova which to fix.
3. Append to `log.md`: `## [YYYY-MM-DD] lint | <summary>`

## Conventions

- Cross-link aggressively with `[[page title]]` (Obsidian wiki links).
- Never modify files under `raw/` — they are immutable.
- Overviews and key claims reflect the current best understanding, not a historical record. Revise in place.
- If a new source contradicts an existing claim, update the claim and note the tension in "Open questions".
- Keep source summaries factual. Put interpretation in entity/concept/domain pages.
- Dates in log entries must be absolute (YYYY-MM-DD), never relative.
