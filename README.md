# Skills (curated fork)

Fork of [mattpocock/skills](https://github.com/mattpocock/skills), cut down to the skills actually used.
Installed in Claude Code as the plugin `mattpocock-skills@mattpocock` from this repo (see `~/.claude/settings.base.json`).

Upstream is kept as the `upstream` remote: `git fetch upstream && git merge upstream/main`, then resolve
modify/delete conflicts on removed skills with `git rm`.

Differences from upstream:

- No issue workflow: `triage` removed, `setup-matt-pocock-skills` defaults to a local markdown tracker in `.scratch/`.
- `pr` removed: its PR-body format (visual summary, before/after evidence, merge danger) lives in ECC's `/pr` instead.
- `chief-of-staff` promoted and merged with ECC loop mechanics (`continuous-agent-loop`, `/loop-start`, `/loop-status`).
- `setup-ts-deep-modules` promoted.
- Dropped: `misc/`, writing skills, `loop-me`, `software-factory`, `claude-handoff`, docs site, Codex `openai.yaml`, release tooling.

## Engineering

User-invoked (`/name`):

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)**: router: which skill or flow fits the situation.
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)**: once per repo: tracker (local by default) and domain doc layout.
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)**: relentless interview that also maintains `GLOSSARY.md` and ADRs.
- **[to-spec](./skills/engineering/to-spec/SKILL.md)**: turn the conversation into a spec.
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)**: split a spec into tracer-bullet tickets with blocking edges.
- **[implement](./skills/engineering/implement/SKILL.md)**: build a spec or ticket via `tdd`, close with `code-review`.
- **[implement-spec](./skills/engineering/implement-spec/SKILL.md)**: build a whole spec as a task graph with parallel implementer subagents.
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)**: chart a multi-session effort as a map of decision tickets.
- **[chief-of-staff](./skills/engineering/chief-of-staff/SKILL.md)**: long-running goal: stop condition, managed loop, checkpoints, wiki.
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)**: find deepening opportunities, HTML report, grill the chosen one.
- **[setup-ts-deep-modules](./skills/engineering/setup-ts-deep-modules/SKILL.md)**: dependency-cruiser rules so each TS package is a deep module.
- **[retro](./skills/engineering/retro/SKILL.md)**: after a session, suggest improvements to the agent's environment.

Model-invoked:

- **[tdd](./skills/engineering/tdd/SKILL.md)**: red-green-refactor, one vertical slice at a time.
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)**: feedback loop first, then minimise, hypothesise, instrument, fix, regression-test.
- **[code-review](./skills/engineering/code-review/SKILL.md)**: two-axis review (Standards + Spec) in parallel subagents.
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)**: deep-module vocabulary: module, interface, seam, depth.
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)**: sharpen domain terms, maintain glossary and ADRs.
- **[prototype](./skills/engineering/prototype/SKILL.md)**: throwaway prototype for a logic or UI question.
- **[research](./skills/engineering/research/SKILL.md)**: background research against primary sources, cited markdown.
- **[wizard](./skills/engineering/wizard/SKILL.md)**: interactive bash wizard for steps only a human can do.

## Productivity

User-invoked: **[grill-me](./skills/productivity/grill-me/SKILL.md)** (stateless interview), **[handoff](./skills/productivity/handoff/SKILL.md)** (handoff doc for another agent), **[teach](./skills/productivity/teach/SKILL.md)** (multi-session learning workspace), **[to-questionnaire](./skills/productivity/to-questionnaire/SKILL.md)** (questions for someone else), **[wait-what](./skills/productivity/wait-what/SKILL.md)** (re-pitch a message that didn't land).

Model-invoked: **[grilling](./skills/productivity/grilling/SKILL.md)** (the interview primitive), **[writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md)** (how to write skills and CLAUDE.md).

License: MIT, see [LICENSE](./LICENSE).
