# CLAUDE.md - Bot Instructions for hw-jjg-bot

## Project Structure

This project uses **two separate jj-git repos**:

1. **App repo** (`/` — project root): Contains the application source code.
2. **Bot session repo** (`/.claude/`): Contains Claude Code session data.

Both repos are managed with `jj` (Jujutsu), which coexists with git.

## Repo Paths

- App repo: `/home/wink/data/prgs/rust/hw-jjg-bot`
- Bot session repo: `/home/wink/data/prgs/rust/hw-jjg-bot/.claude`
  (symlink to `~/.claude/projects/-home-wink-data-prgs-rust-hw-jjg-bot`)

## Committing

Use `-R` (`--repository`) at the end to target the correct repo without
changing directories. Putting `-R` last keeps the verb/action visible at
the start of the command.

### App repo
```
jj commit -m "title" -m "body" -R /home/wink/data/prgs/rust/hw-jjg-bot
```

### Bot session repo
```
jj commit -m "title" -m "body" -R /home/wink/data/prgs/rust/hw-jjg-bot/.claude
```

This avoids directory-change side effects and makes each command self-contained.

## jj Basics

- `jj st -R <path>` — show working copy status
- `jj log -R <path>` — show commit log
- `jj commit -m "title" -m "body" -R <path>` — finalize working copy into a commit
- `jj describe -m "title" -m "body" -R <path>` — set description without committing
- In jj, the working copy (@) is always a mutable commit being edited.
  `jj commit` finalizes it and creates a new empty working copy on top.
