# Guide for agents

This file explains how to change Rubber Duck without breaking its package or its prompt.

## What this repo contains

Rubber Duck is an agent skill written in Markdown. `SKILL.md` is the prompt that agents read. There is no build step and no code.

Keep the skill portable. Do not write instructions that only work in one agent tool. Name tools (Claude Code, Codex, Cursor) only as examples.

## Key files

- `SKILL.md`: the source of truth and the only skill file.
- `README.md`: what the skill does, installation, usage. Its Before/After example must follow the map format in `SKILL.md`.
- `docs/DECISIONS.md`: why the skill is shaped the way it is, including the options that were rejected. Add an entry for every design change.
- `CHANGELOG.md`: release notes, newest first.
- `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json`: the Claude plugin and marketplace entry. The skill loader points at the root `SKILL.md`.
- `.cursor-plugin/plugin.json`: the Cursor plugin.
- `agents/openai.yaml`: display name, short description, and default prompt for OpenAI-compatible agents.

## Rules for changes

- **Keep `SKILL.md` and `README.md` in sync.** If a rule, tag, or map section changes, update the README tables and the example.
- **Version:** keep the same version in `SKILL.md` under `metadata.version`, the first `CHANGELOG.md` heading, `.claude-plugin/plugin.json`, and `.cursor-plugin/plugin.json`.
- **Description:** the plugin manifests use the first sentence of the `SKILL.md` description.
- **Length:** every word of `SKILL.md` is read on every use. Keep the body (everything below the frontmatter) under 1,600 words. A change that adds words has to earn them, and a new rule should replace an old one where it can.
- **Instructions, not decoration:** every line in `SKILL.md` should tell the agent to do something specific at a specific moment. "Be thoughtful" is not an instruction. "Ask at most one question per reply" is.
- **Evidence:** a new rule needs a reason in `docs/DECISIONS.md`: an observed failure, a user's reaction, or a source.
