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

Use `-R` (`--repository`) to target the correct repo without changing directories:

### App repo
```
jj -R /home/wink/data/prgs/rust/hw-jjg-bot commit -m "title" -m "body"
```

### Bot session repo
```
jj -R /home/wink/data/prgs/rust/hw-jjg-bot/.claude commit -m "title" -m "body"
```

This avoids directory-change side effects and makes each command self-contained.

## jj Basics

- `jj -R <path> st` — show working copy status
- `jj -R <path> log` — show commit log
- `jj -R <path> commit -m "title" -m "body"` — finalize working copy into a commit
- `jj -R <path> describe -m "title" -m "body"` — set description without committing
- In jj, the working copy (@) is always a mutable commit being edited.
  `jj commit` finalizes it and creates a new empty working copy on top.
