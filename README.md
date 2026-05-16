# Wenhao's Codex Plugins

Personal collection of Codex skills, ported from the corresponding Claude Code marketplace at [wenhaochai/claude-plugins](https://github.com/wenhaochai/claude-plugins).

The repo follows Codex's plugin/marketplace layout (`plugins/<plugin>/skills/<skill>/SKILL.md`) so skills are grouped logically and could be promoted to full plugins later (with MCP servers, hooks, apps). For now they install as plain Codex skills.

## Install

The cleanest path is to ask Codex to install them via its built-in `skill-installer` skill — open `codex` and say:

> Install the writing skills (style, plot, review, paper-overleaf) and daily skills (todo, spawn-remote) from `wenhaochai/codex-plugins`.

Or do it directly with the install script:

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo wenhaochai/codex-plugins \
  --path plugins/daily/skills/todo plugins/daily/skills/spawn-remote \
         plugins/writing/skills/style plugins/writing/skills/plot \
         plugins/writing/skills/review plugins/writing/skills/paper-overleaf
```

This copies each `SKILL.md` (plus assets) into `~/.codex/skills/<name>/`, where Codex auto-discovers them. Restart `codex` to pick up new skills.

To pick only a subset, drop the corresponding `--path` entries. Example — just `plot`:

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo wenhaochai/codex-plugins --path plugins/writing/skills/plot
```

> `codex plugin marketplace add wenhaochai/codex-plugins` will register the marketplace metadata but does **not** install the skills — Codex's plugin-install step is gated behind the desktop app GUI for now. Use `skill-installer` for the actual install.

## Plugins

### `daily` — Personal daily tools

- **todo** — Manage `TODO.md` (show / add / complete / delete / update via natural language) in the current project. Also shows today's calendar if a Google Calendar MCP is connected.
- **spawn-remote** — Spawn a sibling Claude Code instance via detached tmux and return its `/remote-control` URL. Cross-tool helper (Codex → Claude Code), not a Codex-to-Codex spawner.

### `writing` — Academic / public-facing writing

- **style** — Default writing standards. 17 canonical English-prose rules + 18 page-cap additions (for page-constrained papers) + 2 audit-time rules.
- **plot** — Matplotlib templates for paper / blog / report figures with a Google-brand palette and Palatino body font (matches arxiv `mathpazo`). 10 templates: bar, boxplot, line, scatter variants.
- **review** — Pre-submission self-review of your own AI/ML paper Overleaf draft. Produces a reviewer-style critique simulating a top-tier ML venue reviewer (NeurIPS / ICML / ICLR / CVPR).
- **paper-overleaf** — Overleaf-synced LaTeX paper editing: section-level conventions for NeurIPS / ICML / ICLR / COLM, red-mark workflow with `\textcolor{red}`, bilingual zh/en review, claim-evidence and number / citation audit. Originally tuned for Claude Opus; on gpt-5.5 the taste / argument-quality output may be weaker.

## Notes

- All skills are model-agnostic instruction sets — the same SKILL.md works on any backend.
- Claude Code slash-command semantics (`/daily:todo …`) become natural-language triggers in Codex; the description fields are written to surface on relevant phrasings ("加一条 X", "X 完成了", etc.).
- The Claude Code edition at [wenhaochai/claude-plugins](https://github.com/wenhaochai/claude-plugins) remains the primary edit path for paper-overleaf, which depends on Opus's depth on academic prose.

## License

MIT
