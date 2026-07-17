# Session Handoff: AGENTS.md Rewrite & Handoff Skill Update

- **Date**: 2026-07-17
- **Project**: mattpocock-skills (`~/Developer/skills-journal/mattpocock-skills/`)
- **Next session focus**: Continue cleaning up the fork for universal use, explore more skills

## What We Did

### AGENTS.md / CLAUDE.md Rewrite
- Discovered `AGENTS.md` was a **symlink to `CLAUDE.md`** — both contained identical Claude-specific content
- Broke the symlink, rewrote both files:
  - `AGENTS.md` → universal instructions only (bucket structure, promoted rules, invocation model, `ask-matt` router, `~/.agents/skills` linking). Zero Claude references.
  - `CLAUDE.md` → Claude-specific overrides only (`.claude-plugin/` sync, `claude plugin validate`, docs conventions, `~/.claude/skills` linking)
- Added `## Knowledge` section to AGENTS.md pointing to `knowledge/` folder

### Symlink Trap Lesson
- Wasted ~6 tool calls editing a symlink thinking it was a real file
- Created `knowledge/learning.md` documenting the root cause and fix
- Key rule added to AGENTS.md: always `ls -la` before editing to check for symlinks

### Handoff Skill Update
- Updated `skills/productivity/handoff/SKILL.md` to save handoffs to `.agents/handoffs/` with naming convention `YYYY-MM-DD-HHMMSS-[slug].md`
- Created `.agents/skills/handoff` symlink → `../../skills/productivity/handoff`

### Audit
- Confirmed `skills/productivity/` is clean — zero Claude references across all 5 skills and README.md

## State of the Repo

### Files Modified
| File | Status |
|------|--------|
| `AGENTS.md` | Rewritten — universal, no Claude refs |
| `CLAUDE.md` | Rewritten — Claude-specific overrides only |
| `knowledge/learning.md` | Created — symlink trap lesson |
| `skills/productivity/handoff/SKILL.md` | Updated — new output location + naming convention |
| `.agents/skills/handoff` | Created — symlink to handoff skill |

### Key Facts
- `AGENTS.md` was originally a symlink to `CLAUDE.md` — now independent files
- The fork's purpose: universal `.agents/` optimized, no provider lock-in
- `skills-lock.json` tracks installed skills with source hashes
- `.claude-plugin/plugin.json` version (1.2.0) is out of sync with `package.json` (1.1.0) — known issue from original repo

## Suggested Skills
- `wiki-capture` — capture the symlink trap lesson to Obsidian wiki if user has one set up
- `wiki-lint` — audit the knowledge folder structure if needed

## Open Questions
1. How to populate `adapted/` — fork & customize workflow not yet exercised
2. When to write first ADR (universal format choice?)
3. What additional repos to explore on skills.sh
4. Should `CLAUDE.md` be symlinked back to `AGENTS.md` for the original repo's benefit? (Currently independent)

## Next Steps
- Explore more packages on skills.sh and add to `registry.md` in the skills-journal parent repo
- Consider forking awesome-copilot to shuvrobhai/ for the full skillset
- Continue cleaning other skill buckets (`engineering/`, `misc/`) for Claude references if needed
