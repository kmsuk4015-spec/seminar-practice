# CLAUDE.md

Guidance for Claude Code and other AI assistants working in this repository.

## What this repository is

`seminar-practice` is a **git practice repository** used for a seminar. It is
not an application: there is no source code, no build system, no package
manifest, no test suite, and no CI configuration.

Current contents in full:

```
.
└── test.rtf     # scratch file, Rich Text Format, mixed English + Korean text
```

History (2 commits, both on `main`):

- `80d1b2c` — "Hello. My First Commit" — created `test.rtf`
- `7da2206` — "Update test.rtf with additional content" — appended a Korean line

**Treat the small size as the real state, not as a sign that files are
missing.** Before assuming a framework or tooling exists, check with
`ls -a` and `git ls-files`. Do not invent a project structure, add a
`package.json`, or scaffold a framework unless explicitly asked.

## Environment and commands

There is nothing to install, build, lint, or test. The only meaningful
commands are git and ordinary file inspection:

```bash
git status
git log --oneline
git ls-files          # authoritative list of tracked files
cat test.rtf          # RTF is plain text; read it directly
```

If a future task asks you to "run the tests" or "build the project",
say plainly that no such tooling exists yet rather than guessing at a
command.

## Working with `test.rtf`

`test.rtf` is RTF produced by macOS TextEdit. Two things matter:

- **Encoding.** The header declares `\ansicpg949` (Korean). Korean characters
  are stored as RTF escapes such as `\uc0\u50504` — not as raw UTF-8. When
  adding Korean text, either keep the same escape form or let a real RTF
  editor write the file; typing raw UTF-8 Korean bytes into the file will
  render incorrectly.
- **Line endings.** Each RTF paragraph ends with a trailing `\` before the
  newline. Preserve that when appending lines, and keep the closing `}` as
  the final character of the file.

Because RTF is markup, prefer targeted edits over rewriting the whole file,
and re-read the file after editing to confirm the structure is still intact.

## Conventions

**Branches.** `main` is the default branch. Work happens on feature branches
named `claude/<short-topic>-<suffix>` (e.g. `claude/claude-md-docs-en5618`).
Create the branch if it does not exist; never push directly to `main` without
explicit permission.

**Commits.** Messages so far use a short imperative or descriptive subject
line ("Update test.rtf with additional content"). Keep the subject under
~72 characters. Commits authored with Claude's help carry a trailing
`Co-Authored-By:` line; follow the attribution lines supplied by the current
session rather than copying the ones in older commits verbatim.

**Pushing.** Use `git push -u origin <branch-name>`. On network failure,
retry with exponential backoff (2s, 4s, 8s, 16s). Do not open a pull request
unless the user asks for one.

**Language.** The repository owner writes in both Korean and English. Match
the language the user writes in; file content may legitimately be either.

## Maintaining this file

This document describes a near-empty repository, so it will go stale the
moment real code lands. When the repository gains source files, update the
sections above to cover:

1. the actual directory layout and where entry points live,
2. the real install / build / test / lint commands,
3. any CI workflow under `.github/workflows/`,
4. code style and naming conventions the existing code establishes.

Delete the "What this repository is" framing once it no longer holds. Prefer
describing what you can verify by reading the tree over restating intent.
