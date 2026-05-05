# Obsidian Vault Setup Wizard — Claude Code Edition
#productivity #ai

> This is a step-by-step guide for Claude Code to help a user build a personal Obsidian vault from scratch. Place this file in your vault root or `.claude/` directory, open Claude Code, and say "let's start" or reference this file.
> 
> Based on a real multi-session vault build. The process works — but only if Claude asks, not assumes.

---

## How to use this file

**For the human:** Put this file in your Obsidian vault directory. Open Claude Code there. Say something like: "I want to set up my vault. Follow the wizard in `Obsidian Vault Setup Wizard.md`." Claude will guide you through each phase as a conversation.

**For Claude Code:** This is your playbook. Follow the phases in order. Each phase has a goal, questions to ask, and artifacts to create. Do NOT skip the discovery phase — the entire vault structure depends on understanding the person first.

---

## Prerequisites

Before starting, make sure:

1. **Obsidian** is installed and a vault is created (even if empty)
2. **Claude Code** is installed and working
3. **Git** is initialized in the vault directory (`git init` if not)
4. **kepano/obsidian-skills** are installed — copy them to `.claude/skills/` in the vault. These teach Claude correct Obsidian syntax (wikilinks, callouts, frontmatter, Bases, Canvas). Get them from: https://github.com/kepano/obsidian-skills
5. **Obsidian CLI** (v1.12+) is installed for vault interaction from terminal (optional but recommended)
6. Allocate **2-3 hours** for the first session. You won't finish everything, but you'll have a working foundation.

---

## Phase 0: Technical Foundation

**Goal:** Set up the files that make Claude Code effective across sessions.

### 0.1 — Create `.claude/` directory structure

```
.claude/
├── skills/           # kepano/obsidian-skills go here
├── settings.json     # Claude Code settings (auto-created)
└── ...
```

### 0.2 — Create a starter CLAUDE.md in vault root

This is the most important file. It tells Claude Code how to behave in this vault. Start minimal — you'll expand it as the vault takes shape.

```markdown
# [Vault Name] — Project Context

## Vault Purpose
[Will be filled after Phase 1]

## Language
[Primary language for notes. Can be mixed.]

## Conventions
- Use [[wiki links]] for internal references
- Frontmatter is YAML, always preserve existing fields
- Dates in ISO format: YYYY-MM-DD
- Never modify files inside .obsidian/
- Never delete files without explicit confirmation

## Git Workflow
- Commit messages: "type: description" (e.g., "add: weekly review", "edit: goals update")
- Do NOT commit .obsidian/ config changes
- Add .obsidian/ to .gitignore
```

### 0.3 — Create a global `~/.claude/CLAUDE.md` (if doesn't exist)

This file applies to ALL projects, not just the vault. Include:
- Your name and short name (so Claude addresses you naturally)
- Communication style preferences (direct? detailed? challenge assumptions?)
- Language preferences
- What you never want (generic advice? process narration? asking permission for reads?)

### 0.4 — Set up `.gitignore`

```
.obsidian/
.trash/
.DS_Store
```

### 0.5 — Set up auto-memory

Claude Code has persistent memory at `~/.claude/projects/<project-path>/memory/`. Create a `MEMORY.md` there. Claude will update it across sessions to remember context, decisions, and patterns. Keep it under 200 lines (Claude sees the first 200 lines automatically).

---

## Phase 1: Discovery — Who Are You?

**Goal:** Understand the person deeply enough to build a structure that fits THEM, not a template.

**Critical principle:** The vault structure must emerge from the person's actual life, not from a productivity framework. Frameworks (PARA, Zettelkasten, Life Capitals) are tools, not answers. Ask first, categorize later.

### Questions to ask (conversational, not interrogation)

**Identity & context:**
- What do you do? (work, role, industry)
- What matters to you outside of work?
- What are you trying to figure out or improve right now?
- Do you have a partner? Kids? Dependents?
- Where do you live? Is location stable or changing?

**Knowledge management history:**
- Have you used any note systems before? (Notion, Evernote, Apple Notes, paper)
- What worked? What didn't?
- Do you have existing notes/content to import? How much?
- What's the main pain point that brought you to Obsidian?

**How you think:**
- Do you think in categories or in connections?
- Do you prefer structure (folders, hierarchies) or flat + search?
- Are you a collector (save everything) or a curator (save selectively)?
- Do you journal or reflect regularly?

**Goals & aspirations:**
- Do you have explicit goals? Written down?
- Do you track habits or routines?
- Are there people in your life you want to track notes about?

### What to listen for

- **Life domains** — the natural categories of their life (work, health, family, hobbies, finances...). These become areas.
- **Recurring themes** — what keeps coming up? These become priority areas.
- **Decision points** — what are they actively deciding? These become projects.
- **Knowledge gaps** — what do they want to learn? These feed the learning area.
- **Pain points** — what's causing friction? This informs what to build first.

### Artifact: `_meta/Me.md`

After the conversation, create a "self-portrait" note. This is the vault's anchor — everything connects back to who they are.

```markdown
---
created: YYYY-MM-DD
origin: session
tags:
  - meta
---

# Me

## Who I am
[2-3 paragraphs: role, identity, what defines them beyond their job]

## What matters to me
[Values, priorities — in their own words, not abstracted]

## What I'm working on
[Current focus areas, active questions, things in flux]

## Related files
- [[Areas]]
- [[Goals YYYY]]
```

---

## Phase 2: Framework — Life Architecture

**Goal:** Map the person's life into 5-10 areas that cover everything important without overlap.

### How to derive areas

Do NOT copy someone else's framework. Instead:

1. Take everything from Phase 1 and list all distinct domains
2. Merge overlapping ones (e.g., "gym" and "diet" → Health)
3. Separate ones that feel different (e.g., "career development" vs "personal brand" — internal vs external)
4. Check: does every important thing in their life fit into exactly one area?
5. Check: are there areas with nothing in them? Remove those.
6. Aim for 5-10 areas. Less than 5 = too broad, more than 10 = cognitive overload.

### Common patterns (not prescriptions)

These are areas that tend to emerge. Use only the ones that are real for this person:

| Pattern | When it applies |
|---------|----------------|
| Health / Energy | Almost always relevant |
| Relationships / People | If they care about tracking relationships |
| Finance / Wealth | If money management is active, not on autopilot |
| Career / Professional | If work identity matters beyond daily tasks |
| Learning / Growth | If they're actively building knowledge |
| Home / Environment | If physical space matters to them |
| Creative / Culture | If hobbies, art, travel are significant |
| Inner Work / Reflection | If they do therapy, coaching, meditation |
| Public Identity / Influence | If they speak, write, build a brand |

### The "People" question

People are cross-cutting — a person might be relevant to work, health (gym buddy), and social life simultaneously. Two valid approaches:

1. **People as a cross-layer** — a separate `People/` folder with profiles that link to areas via tags. Works well if you track 10+ people.
2. **People within areas** — each person lives in their primary area. Works if you have few people notes.

Ask the user which feels more natural.

### Artifact: `_meta/Areas.md`

```markdown
---
created: YYYY-MM-DD
origin: session
tags:
  - meta
  - nav
---

# Areas

[Short explanation of what areas are and how they map to this person's life]

| # | Area | What it covers | Tag |
|---|------|---------------|-----|
| 11 | Learning & Growth | ... | `learning` |
| 12 | Health & Energy | ... | `health` |
| ... | ... | ... | ... |

## Related files
- [[Me]]
- [[Goals YYYY]]
```

### Folder structure

Create numbered area folders + system folders:

```
00 — Inbox/                    # Unsorted captures
11 — [Area 1 Name]/
12 — [Area 2 Name]/
...
20 — People/                   # If using cross-layer approach
Reflections/                   # Daily notes, journaling
Goals/                         # Goals, OKRs, reviews
  Session Logs/                # Claude session logs
Projects/                      # Active cross-area projects
Templates/                     # Obsidian templates
_meta/                         # Foundation files (Me, Areas, values)
_attachments/                  # Images, PDFs, non-markdown
_inputs/                       # Raw material for import
_claude/                       # Claude's workspace
  drafts/                      # Draft notes before they move to vault
  extracts/                    # Structured data from external sources
```

**Why numbered folders:** They sort predictably in the file explorer. The numbering is semantic, not sequential — gaps are fine. `00` for Inbox (always first), `11-19` for areas, `20` for People.

**Why underscored folders:** `_meta/`, `_attachments/`, `_inputs/`, `_claude/` sort to the bottom and signal "infrastructure, not content."

---

## Phase 3: Conventions — The Rules

**Goal:** Establish consistent rules so every note is findable and connected.

### 3.1 — Frontmatter standard

Every note created by Claude should include:

```yaml
---
created: YYYY-MM-DD
updated: YYYY-MM-DD
origin: claude | [username] | session
tags:
  - [area-tag]
  - [optional topic tags]
---
```

- `origin` tracks who created the note: `claude` (autonomous), the user's name (they wrote it), or `session` (collaborative)
- `tags` are always in frontmatter as a YAML array, never inline
- Tags are lowercase English even if content is in another language

### 3.2 — Tag system

Three layers:

| Layer | Purpose | Examples |
|-------|---------|----------|
| Area tags | Required on every content note | `health`, `finance`, `learning` |
| System tags | For infrastructure | `meta`, `nav`, `goals`, `project/name` |
| Topic tags | Optional cross-area filtering | `travel`, `books`, `cooking` |

Rules:
- Every content file MUST have at least one area or system tag
- Tags are lowercase English
- Projects use hierarchical tags: `project/vault-setup`
- No proliferation — before creating a new tag, check if an existing one fits

### 3.3 — Linking

- Use `[[wiki links]]` everywhere, never `[markdown](links)` for internal references
- Every note should have a `## Related files` section at the bottom with links to connected notes
- Session logs link to all artifacts created in that session
- Goal: the Obsidian graph view should show meaningful clusters, not isolated nodes

### 3.4 — File naming

- File and folder names: user's preferred language, but English is recommended for compatibility
- No date prefixes except for logs and journal entries
- Avoid special characters that break across OS: `/ \ : * ? " < > |`

### 3.5 — What goes where

| Content type | Location |
|-------------|----------|
| New unsorted note | `00 — Inbox/` |
| Area-specific note | Respective area folder |
| Person profile | `People/` (or area folder) |
| Daily reflection | `Reflections/` |
| Goal or review | `Goals/` |
| Active project | `Projects/` |
| Foundation/identity | `_meta/` |
| Images, PDFs | `_attachments/` |
| Import material | `_inputs/` |
| Claude drafts | `_claude/drafts/` |
| Claude extracts | `_claude/extracts/` |

### Update CLAUDE.md

After establishing conventions, expand the vault's CLAUDE.md with all of the above. This is the file future Claude sessions will read — make it comprehensive.

---

## Phase 4: Foundation — The First Notes

**Goal:** Create the seed notes that give the vault its identity.

### Must-have foundation files

1. **`_meta/Me.md`** — self-portrait (from Phase 1)
2. **`_meta/Areas.md`** — area map with descriptions (from Phase 2)
3. **`Goals/Goals [YEAR].md`** — current year goals (from Phase 5)
4. **`Projects/Vault and Workflow.md`** — meta-project tracking vault development itself

### Optional but valuable

- **`_meta/Values.md`** — what they believe in, principles they live by
- **`_meta/My History.md`** — chronological skeleton of their life (see Phase 6)
- **`People/index.md`** — people model + directory of key people
- **`_meta/Psychometrics.md`** — if they've done MBTI, Clifton, DISC, etc.

### Create index files

Each area folder should have an `index.md` that explains what goes there and links to key notes. Keep them minimal — they grow over time.

---

## Phase 5: Goals — What Are You Working Toward?

**Goal:** Capture the user's goals in a structured, connected way.

### How to approach this

This is a conversation, not a form. Don't ask "what are your goals?" — that gets generic answers. Instead:

1. **Start with vision:** "If you could wave a magic wand, what would your life look like in 2-3 years?"
2. **Identify gaps:** "What's the biggest difference between that vision and today?"
3. **Find the theory of change:** "What would need to happen for that gap to close?"
4. **Get specific:** "What could you actually do this year toward that?"
5. **Challenge:** "Is this something you genuinely want, or something you think you should want?"

### Structure the goals doc

```markdown
---
created: YYYY-MM-DD
updated: YYYY-MM-DD
origin: session
tags:
  - goals
---

# Goals [YEAR]

## Vision
[What they're ultimately working toward — not a goal, but a direction]

## Theory of change
[The key levers — what actually drives progress toward the vision]

## By area
### [Area 1]
- [Specific, actionable goals]

### [Area 2]
- ...

## Open questions
[Things they haven't figured out yet — these are valuable to track]

## Related files
- [[Me]]
- [[Areas]]
```

### Key insight from experience

Goals docs are living documents, not contracts. Include an "Open questions" section — the things they're still figuring out are just as important as the things they've decided. Claude should revisit and challenge these in future sessions.

---

## Phase 6: History — Where You Come From

**Goal:** Build a personal timeline that connects past experiences to present identity.

### Why this matters

History isn't nostalgia — it's pattern recognition. Understanding where you've lived, who you've been with, what you've done helps identify patterns that inform current decisions.

### Approach

1. **Start with a skeleton** — `_meta/My History.md` with major life phases
2. **Branch into area timelines** — detailed histories in specific areas (health, relationships, career, housing)
3. **Link them** — use a `timeline` tag to connect all history files

### Structure

**`_meta/My History.md`** — the skeleton:
```markdown
## [Phase name] (YYYY—YYYY)
Where: [location]
Key: [1-2 sentence summary]
See also: [[Area-specific timeline]]
```

**Area timelines** (e.g., `12 — Health & Energy/Health Timeline.md`):
- Detailed chronological notes within one area
- Connected to the main skeleton via links

### Don't force this

Not everyone has a strong historical orientation. If the user isn't interested in building their history, skip this phase. It's valuable but not essential.

---

## Phase 7: People — Your Network

**Goal:** Create a system for tracking important people and relationships.

### When to build this

Only if the user has 5+ people they want to track notes about. Otherwise, people notes can live ad hoc in area folders.

### People model

Ask the user to think about the roles people play in their life. Common categories:
- People they learn from / admire
- People who work for them (personal context — coaches, assistants, doctors)
- Close relationships (partner, family, close friends)
- Professional peers
- Mentors

### Profile template

```markdown
---
created: YYYY-MM-DD
updated: YYYY-MM-DD
origin: session
tags:
  - people
  - [relevant area tags]
---

# [Person Name]

## Context
[Who they are, how you know them, why they matter]

## Notes
[Running notes — things to remember, conversation topics, observations]

## Related files
- [[relevant notes]]
```

---

## Phase 8: Import — Bringing In Existing Content

**Goal:** Migrate existing notes without creating a mess.

### The cardinal rule

**The vault is a working model, not an archive.** Not everything deserves to be imported. A note enters the vault only if:

1. It contains an original thought (not just a bare link or screenshot)
2. It connects to something alive (goals, people, an active area)
3. It's a personal artifact (biography, values, something uniquely yours)

Everything else stays in `_inputs/` as raw material.

### The process

```
Source (Notion, Apple Notes, Evernote, etc.)
  ↓ export
_inputs/[source-name]/          # raw dump
  ↓ triage
Tier 1: Import now              # original thoughts, active references
Tier 2: Enrich later            # good raw material, needs work
Tier 3: Leave as reference      # context only, don't import
  ↓ import tier 1
Respective area folders         # with proper frontmatter, tags, links
```

### Triage tips

- Do triage in batches, not all at once (cognitive fatigue kills quality)
- Claude can help categorize — show it a batch, let it propose tier assignments, you approve
- Create `_inputs/index.md` to track what's been imported and what's pending
- Historical artifacts get an `archive` tag and their own note (don't embed in other files — better for graph connectivity)

---

## Phase 9: Session Workflow — Continuity Across Conversations

**Goal:** Set up patterns that make every Claude session build on previous ones.

### Session logs

Create a session log at the START of every session:

```
Goals/Session Logs/YYYY-MM-DD — Session.md
```

Structure:
```markdown
---
created: YYYY-MM-DD
origin: session
tags:
  - goals
  - project/vault-setup
---

# YYYY-MM-DD — Session

## What we did
- ...

## Key decisions
- ...

## Artifacts created
| File | What it is |
|------|-----------|
| ... | ... |

## What's next
- ...

## Related files
- [[...]]
```

Rename the file when the theme becomes clear (e.g., `2026-03-01 — Goals Deep Dive.md`).

### Memory system

Claude Code's auto-memory (`~/.claude/projects/.../memory/MEMORY.md`) is the key to continuity. After each session, update it with:

- Vault structure decisions (what folders exist, why)
- Key files and what they contain
- User preferences discovered during the session
- Open questions and next steps
- Conventions that were established

Keep MEMORY.md under 200 lines. For detailed notes, create separate files in the memory directory and link from MEMORY.md.

### What makes sessions productive

1. **Read context first** — at session start, Claude should read CLAUDE.md, MEMORY.md, and the last session log
2. **Create the session log early** — don't wait until the end
3. **Commit after meaningful changes** — don't let work pile up uncommitted
4. **Update memory at session end** — capture what was learned
5. **Leave breadcrumbs** — the "what's next" section in session logs is the most valuable part

---

## Phase 10: Multi-Vault Architecture (Optional)

**Goal:** If the user needs separate vaults (personal vs work, or different sensitivity levels), set up isolation and cross-vault communication.

### When to use multiple vaults

- Different sensitivity levels (personal vs work vs private)
- Different git repos / sharing rules
- Content that should never mix (e.g., work HR data and personal journal)

### Cross-vault protocol

If using multiple vaults, create a `Shared/` directory:

```
~/Obsidian/
├── Personal/           # Personal vault
├── Work/               # Work vault
├── Shared/             # NOT a vault — shared directory
│   ├── Personal Context.md    # Owner: Personal vault
│   ├── Work Context.md        # Owner: Work vault
│   └── _claude/               # Inter-Claude messaging
│       ├── from-personal--topic.md
│       └── from-work--topic.md
└── CLAUDE.md           # Top-level rules
```

Each vault symlinks to Shared:
- Personal: `Reference-Shared/` → `~/Obsidian/Shared/`
- Work: `Reference-Work/` or similar

Rules:
- Each vault's Claude Code only edits ITS OWN context file
- Messages between Claudes go through `_claude/` in Shared
- Never copy content between vaults without explicit instruction

### Skip this if

The user only needs one vault. Don't over-engineer. A single vault with good folder structure covers most people.

---

## Lessons Learned — From Real Experience

Things that worked:

1. **Structure follows life, not theory.** Don't start with a framework and force-fit. Start with "what matters to you?" and let structure emerge.

2. **Vault = working model, not archive.** The biggest mistake is importing everything. Be ruthless about what earns a place in the vault.

3. **Frontmatter is non-negotiable.** Every note needs `created`, `tags`, `origin` at minimum. Without this, the vault becomes unsearchable chaos within weeks.

4. **Links are the point.** The graph view is what makes Obsidian more than a folder of markdown files. Every note should link to related notes. A `## Related files` section at the bottom is the simplest habit to enforce.

5. **Session logs are the backbone.** They provide continuity across Claude sessions and serve as a decision journal. Creating them at the START (not end) of sessions captures context that would otherwise be lost.

6. **Memory keeps Claude useful.** Without MEMORY.md, every session starts from zero. With it, Claude knows your vault, your conventions, your preferences, and your open questions.

7. **Conventions before content.** Spending 30 minutes on frontmatter rules and tag taxonomy saves hours of cleanup later.

8. **Git keeps you safe.** Commit after every meaningful change. Claude sometimes makes mistakes. Git lets you roll back.

9. **Don't build everything at once.** Foundation first (Me, Areas, Goals), then fill in organically as topics come up in conversation.

10. **Challenge, don't just organize.** The best Claude sessions aren't just "file these notes" — they're "here's what I'm thinking, push back on the weak parts."

---

## Quick Start Checklist

For the impatient — the minimum viable setup:

- [ ] Git init + .gitignore (exclude .obsidian/)
- [ ] Install kepano/obsidian-skills in .claude/skills/
- [ ] Create minimal CLAUDE.md in vault root
- [ ] Create ~/.claude/CLAUDE.md with personal preferences
- [ ] Run Phase 1 discovery conversation with Claude
- [ ] Create _meta/Me.md
- [ ] Create _meta/Areas.md + folder structure
- [ ] Establish frontmatter + tag conventions (update CLAUDE.md)
- [ ] Create Goals/Goals [YEAR].md
- [ ] Create first session log
- [ ] Commit everything
- [ ] Start using the vault

Everything else can be built incrementally across sessions.

---

## Recommended Obsidian Plugins

Core (built-in, just enable):
- **Templates** — for note templates
- **Daily notes** — for reflections
- **Backlinks** — essential for graph navigation
- **Graph view** — visual connections
- **Tags** — tag pane for browsing
- **Outgoing links** — see what a note links to

Community (install via Community Plugins):
- **Dataview** — query notes like a database (powerful with good frontmatter)
- **Templater** — advanced templates with dynamic content
- **Calendar** — visual calendar for daily notes
- **Obsidian Git** — auto-commit and backup (alternative to CLI git)

---

## Recommended Claude Code Setup

### CLAUDE.md structure (final state)

```
CLAUDE.md (vault root)
├── Vault Purpose
├── Structure (folder tree with descriptions)
├── Tag System (layers, rules, examples)
├── Frontmatter Conventions
├── Session Logs (format, triggers)
├── Graph Connectivity (linking rules)
├── Language Rules
├── Git Workflow
├── Claude Workspace (_claude/ usage)
└── Conventions (naming, inbox, attachments)
```

### Memory structure

```
~/.claude/projects/<path>/memory/
├── MEMORY.md          # Main memory (< 200 lines)
├── vault-setup.md     # Detailed vault structure notes
└── [topic].md         # Topic-specific deep notes
```

### Hooks and skills

- **kepano/obsidian-skills** — Obsidian syntax (wikilinks, callouts, frontmatter, Bases, Canvas)
- **Obsidian CLI skill** — if using Obsidian CLI for vault interaction
- **Session start hook** — can auto-display date, last session info

---

*This wizard was distilled from building a real personal vault over multiple sessions. The process is iterative — don't try to finish in one sitting. Build the foundation, then grow organically.*
