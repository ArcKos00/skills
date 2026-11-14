Curated fork of `mattpocock/skills`, shipped to Claude Code as the plugin `mattpocock-skills@mattpocock` (marketplace = this repo).

- Skills live in `skills/engineering/` (code work) and `skills/productivity/` (non-code). There are no other buckets: a skill we stop using is deleted, not parked.
- Every skill must be listed in `.claude-plugin/plugin.json` (`skills` array) and in `README.md`, linked to its `SKILL.md`. Run `claude plugin validate . --strict` after touching either manifest, and bump `version` in `plugin.json` so installs pick the change up.
- Every `SKILL.md` is either user-invoked (`disable-model-invocation: true`) or model-invoked. A user-invoked skill may call model-invoked ones, never another user-invoked one through the Skill tool (reading its `SKILL.md` as a procedure is fine, as `chief-of-staff` does).
- `ask-matt` is the router over every user-reachable skill. Whenever a skill is added, renamed, removed, or changes how it fits the flows, update `ask-matt` in the same change.
- Specs and tickets go to the tracker chosen by `setup-matt-pocock-skills`; the default is local markdown under `.scratch/`. There is no issue triage in this fork.
- PR bodies are ECC's job (`/ecc:pr`); don't reintroduce a `pr` skill here.
- No em-dashes in prose. Rewrite the sentence with a comma, colon, period or parentheses instead.
- Every skill that dispatches a subagent says to start it with a fresh context window.
- Upstream is the `upstream` remote. When merging it, resolve modify/delete conflicts on removed skills with `git rm`, and re-check `ask-matt` and `plugin.json`.
