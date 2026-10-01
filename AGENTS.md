# Gamify Life agent guide

## Source of truth

1. The user's current request and decisions in the active conversation.
2. `research/GAME_PRODUCT_PLAN.md`, when present locally. It is the full planning record and contains private context; never publish or quote its private details into public files without the user's explicit instruction.
3. `docs/PRODUCT_BRIEF.md`, the public subset available to every clone.
4. Accepted requirements in `openspec/specs/`. Changes in `openspec/changes/` are proposals until reviewed and accepted.
5. Code and observed application behavior, once implemented. When these conflict with accepted requirements, surface the conflict rather than silently changing product policy.

The game is in pre-production. Do not infer a web/mobile stack, game engine, AI provider, health intervention, or reward system from an example or a hypothesis.

## Working in this repository

- Use OpenSpec for substantial feature changes. Its Codex skills are in `.agents/skills/`; the pinned CLI is available through `npm exec -- openspec` after `npm ci`.
- Keep questions and plans proportional to the task. Record material game decisions and their evidence in the product plan when the local file is available.
- Preserve player choice: AI proposes missions, the player can accept, lighten, change, defer, or decline. Health-related suggestions must not diagnose or shame players.
- Protect the local `research/` directory. It is intentionally ignored by Git. Public product statements belong in `docs/PRODUCT_BRIEF.md` after review.
- Do not claim a feature works from a completed checklist alone. Use evidence appropriate to the change when implementation begins.
