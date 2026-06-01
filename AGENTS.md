# Codex SEO: Universal SEO Analysis Skill

## Project Overview

This repository contains **Codex SEO**, a Codex-first SEO analysis skill suite synced from `AgriciDaniel/claude-seo` v2.0.0 plus Codex packaging, runners, cache artifacts, and TOML agents.

The canonical skill tree lives under `skills/`. The main orchestrator is `skills/seo/SKILL.md`; the old top-level `seo/` folder is intentionally not used.

## Architecture

```text
codex-seo/
  .codex-plugin/plugin.json       # Codex plugin manifest
  skills/seo/SKILL.md             # Main orchestrator and routing
  skills/seo-*/SKILL.md           # Specialist SEO workflows
  skills/seo/references/          # Shared references, cache schemas, thresholds
  agents/seo-*.toml               # Codex specialist agent profiles
  scripts/                        # Deterministic Python runners and API helpers
  hooks/                          # Optional schema validation hooks
  schema/                         # Schema.org JSON-LD templates
  extensions/                     # Optional MCP extension install helpers
  tests/                          # Contract, manifest, wrapper, and runtime tests
```

## Development Rules

- Keep `SKILL.md` files under 500 lines.
- Reference files should stay focused and loaded on demand.
- Scripts must have docstrings, CLI help, and JSON output when used by wrappers.
- Follow kebab-case naming for skill directories.
- Python dependencies install into `~/.codex/skills/seo/.venv/`.
- All skills include a shared cache Step 0 and cache write guidance.
- New config paths use `~/.config/codex-seo/`; legacy `~/.config/claude-seo/` paths may be read only as migration fallback.
- Keep multi-platform frontmatter portable across Cursor, Gemini CLI, Codex, Cline, Aider, and Antigravity. Run `python scripts/portability_check.py` before release.
- Run `python -m pytest tests/` after changes.

## Tool Name Portability

| Claude tool | Codex equivalent | Cline/Aider note |
|---|---|---|
| Read | file read | Use local file reads. |
| Write | apply patch/write artifact | Prefer patchable file writes. |
| Edit | apply_patch | Keep diffs scoped. |
| Bash | shell command | Use repo scripts where possible. |
| Glob | file search | Prefer `rg --files`. |
| Grep | text search | Prefer `rg`. |
| WebFetch | browser/web fetch | Use platform web/browser tool when available. |

## Key Principles

1. **Codex-first packaging**: skills, `.toml` agents, and `.codex-plugin/plugin.json`.
2. **Progressive disclosure**: metadata always loaded, references on demand.
3. **Evidence over guesses**: do not fabricate crawl, SERP, API, or performance data.
4. **Cross-skill caching**: `.seo-cache/` enables reuse between workflows.
5. **Deterministic wrappers**: API/headless paths return structured artifacts and setup-required states.
6. **Footer gating**: promotional/community footer is disabled by default unless explicitly enabled.

## Shipping Rules

Follow `/home/agricidaniel/Desktop/shipping-rules.md`: read first, write second, verify third. Keep changes scoped, preserve rollback paths, and verify claims with tests or direct inspection.
