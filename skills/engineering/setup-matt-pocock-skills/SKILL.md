---
name: setup-matt-pocock-skills
description: "Configure this repo for the engineering skills: set up where specs and tickets live (local markdown by default) and the domain doc layout. Run once before first use of the other engineering skills."
disable-model-invocation: true
---

# Setup Matt Pocock's Skills

Scaffold the per-repo configuration that the engineering skills assume:

- **Issue tracker**: where specs and tickets live. **Local markdown under `.scratch/` by default**; GitHub Issues only when the user explicitly asks for it.
- **Domain docs**: where `GLOSSARY.md` and ADRs live, and the consumer rules for reading them

This is a prompt-driven skill, not a deterministic script. Explore, present what you found, confirm with the user, then write.

## Process

### 1. Explore

Look at the current repo to understand its starting state. Read whatever exists; don't assume:

- `AGENTS.md` and `CLAUDE.md` at the repo root: does either exist? Is there already an `## Agent skills` section in either?
- `GLOSSARY.md` and `GLOSSARY-MAP.md` at the repo root, and the legacy `CONTEXT.md` / `CONTEXT-MAP.md`. If a legacy file exists, offer to `git mv` it to its `GLOSSARY` name and rewrite those names in `docs/agents/domain.md`.
- `docs/adr/` and any `src/*/docs/adr/` directories
- `docs/agents/`: does this skill's prior output already exist?
- `.scratch/`: a sign that the local-markdown tracker is already in use
- `.gitignore`: does it already mention `.scratch/`?
- Monorepo signals: a `pnpm-workspace.yaml`, a `workspaces` field in `package.json`, a `.sln` with several projects, or a populated `packages/*` with its own `src/`. Their absence means single-context, which is almost every repo.

### 2. Present findings and ask

Summarise what's present and what's missing. Then take the sections in order. One section, one answer, then the next.

Lead each section with the recommended answer so the user can accept it in a word. Skip a section entirely when exploration already settled it.

**Section A: Issue tracker.**

> Explainer: specs and tickets from `to-spec`, `to-tickets`, `wayfinder` and `implement-spec` have to live somewhere. Recommended: **local markdown** under `.scratch/<feature>/` in this repo.

Offer:

- **Local markdown** (recommended, default): specs and tickets live as files under `.scratch/<feature>/`. Ask one follow-up: commit `.scratch/` with the repo, or add it to `.gitignore`? (recommended: **commit**, so the spec travels with the branch.)
- **GitHub**: tickets live in the repo's GitHub Issues (uses the `gh` CLI). Only when the user asks for it.
- **Other** (Jira, Linear, a wiki, etc.): ask the user to describe the workflow in one paragraph; record it as freeform prose.

Record the choice in `docs/agents/issue-tracker.md`.

A GitHub tracker needs a reachable repo: done when `gh repo view` prints the project from inside this directory; if it can't, stop and tell the user what's missing.

**Section B: Domain docs.** Default to **single-context** (one `GLOSSARY.md` + `docs/adr/` at the repo root). This fits almost every repo; write it without asking.

Offer **multi-context** (a root `GLOSSARY-MAP.md` pointing to per-context `GLOSSARY.md` files) only when exploration found monorepo signals. Then confirm which layout they want.

### 3. Confirm and edit

Show the user a draft of:

- The `## Agent skills` block to add to whichever of `CLAUDE.md` / `AGENTS.md` is being edited (see step 4 for selection rules)
- The contents of `docs/agents/issue-tracker.md` and `docs/agents/domain.md`

Let them edit before writing.

### 4. Write

**Pick the file to edit:**

- If `CLAUDE.md` exists, edit it.
- Else if `AGENTS.md` exists, edit it.
- If neither exists, ask the user which one to create; don't pick for them.

Never create `AGENTS.md` when `CLAUDE.md` already exists (or vice versa); always edit the one that's already there.

If an `## Agent skills` block already exists in the chosen file, update its contents in-place rather than appending a duplicate. Don't overwrite user edits to the surrounding sections.

The block:

```markdown
## Agent skills

### Issue tracker

[one-line summary of where specs and tickets live]. See `docs/agents/issue-tracker.md`.

### Domain docs

[one-line summary of layout: "single-context" or "multi-context"]. See `docs/agents/domain.md`.
```

Then write the docs files using the seed templates in this skill folder as a starting point:

- [issue-tracker-local.md](./issue-tracker-local.md): local-markdown tracker (default)
- [issue-tracker-github.md](./issue-tracker-github.md): GitHub issue tracker
- [domain.md](./domain.md): domain doc consumer rules + layout

For "other" trackers, write `docs/agents/issue-tracker.md` from scratch using the user's description.

### 5. Done

Tell the user the setup is complete and which engineering skills will now read from these files. Mention they can edit `docs/agents/*.md` directly later; re-running this skill is only necessary if they want to switch trackers or restart from scratch.
