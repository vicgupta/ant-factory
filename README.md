# create-ant-factory

A skill that builds a software factory: label a GitHub issue with `ready`, a coding agent implements it inside an Upstash Box, and a pull request comes back for review.

## Contents

- `SKILL.md` — the full workflow (Stages 0–9): interview, scaffold, secrets, smoke test, trigger dry run, worker image, first run, scale test, handover.
- `assets/template/` — working factory implementation to copy into a new factory repo: `factory.config.json`, `scripts/`, `src/`, `.github/workflows/factory.yml`, `templates/`, `worker/setup.sh`.
- `references/` — `architecture.md`, `config.md`, `agents.md`, `upstash-box.md`, `worker-image.md`, `pitfalls.md`.
- `.env.example` — the three secrets every factory needs (values stay local, never committed).

## Use

Copy this folder into your agent's skills directory (e.g. `.opencode/skills/create-ant-factory`) or point your agent at this repo. The skill tells the agent to adapt the template instead of inventing a pipeline, to work stage by stage, and to keep notes under `docs/` in the factory repo.

Requires on the user's machine: Node 20.6+, git, GitHub CLI `gh` with `repo` + `workflow` scopes.

## The three tokens

See `.env.example`. The user creates each one and puts values in a local `.env` (ignored by git):

1. `UPSTASH_BOX_API_KEY` — Upstash console, Box section.
2. `FACTORY_GITHUB_TOKEN` — fine-grained token covering the factory repo and every app repo (Contents, Pull requests, Issues: read + write).
3. `CLAUDE_CODE_OAUTH_TOKEN` — from `claude setup-token` (subscription) or `ANTHROPIC_API_KEY`. Other agents (Codex, OpenCode) use their own secret per `references/agents.md`.

`node --env-file=.env scripts/check-setup.mjs` verifies setup without printing values.

## Docs

Upstash Box: https://upstash.com/docs/box/overall/quickstart — Claude Code: https://code.claude.com/docs — Codex: https://developers.openai.com/codex
