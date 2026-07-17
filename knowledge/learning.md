# Learning: The Symlink Trap

## What Happened

While rewriting `AGENTS.md` (universal) and `CLAUDE.md` (Claude-specific), I got stuck in a failing loop:

1. Wrote new content to `AGENTS.md` → verified → it had `CLAUDE.md` content
2. Wrote again → same result
3. Switched to `edit` tool → same result
4. Wrote `CLAUDE.md` → `AGENTS.md` changed again

I wasted ~6 tool calls debugging this before finding the root cause.

## Root Cause

`AGENTS.md` was a **symlink** pointing to `CLAUDE.md`:

```
AGENTS.md -> CLAUDE.md
```

So writing to `AGENTS.md` actually wrote to `CLAUDE.md`. When I "verified" `AGENTS.md`, the symlink resolved to the same file — of course it showed the wrong content.

## The Fix

```bash
rm AGENTS.md          # remove the symlink
# then write AGENTS.md as a real file
```

## Lesson for Future Sessions

**Before editing any file, check if it's a symlink.** One command saves 10+ wasted edits:

```bash
ls -la <file>
```

If it shows `->` in the output, it's a symlink. Break it first (`rm`), then create the real file.

## When to Apply This

- Edits to a file keep producing unexpected content
- Editing file A seems to change file B
- A file's content doesn't match what you just wrote
- Anytime you're working in a forked repo (symlinks are common in plugin/harness setups)

## Detection Pattern

The symptom is always the same: **"I wrote X but the file still shows Y."** Before retrying the write, run `ls -la`. If the file is a symlink, that's your answer.
