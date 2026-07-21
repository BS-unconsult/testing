---
name: resume-session
description: >
  Checkpoints and resumes discussion state across ephemeral Claude Code cloud
  sessions via files committed to this repo. Trigger in resume mode on:
  "/resume-session", "resume", "where were we", "pick up where we left off",
  "continue from last session", "catch me up". Trigger in checkpoint mode on:
  "checkpoint", "save this session", "checkpoint this session", "wrapping up",
  "save our progress for next time". Do NOT use for handovers the user will
  copy-paste manually — that is session-handover; do NOT use for migrating to
  an entirely new project — that is project-handover.
---

## Why this exists

Every cloud session runs in a fresh container. Previous sessions' chat
transcripts are not on disk in a new container — there is nothing to resume
from unless it was written down somewhere durable. The only durable storage
available across sessions is this git repo. That means session state has to
be checkpointed into the repo before a session ends, or it is simply gone,
and the next session has to know to look for it there.

## Checkpoint mode (user is wrapping up / says "checkpoint")

When the user is wrapping up, or says anything like "checkpoint", "save this
session", "checkpoint this session", "wrapping up", or "save our progress for
next time":

1. Distill the current session into exactly these five sections, under 500
   words total, written as state, not narrative:
   - **Where we left off**
   - **Decisions made**
   - **What was tried**
   - **Open questions**
   - **Start here**

   Distill primarily from the in-context conversation. If earlier context has
   been summarized away and detail is missing, supplement by reading the
   current session's own transcript at
   `/root/.claude/projects/-home-user/<current-session-id>.jsonl` (the newest
   `.jsonl` file in that directory).

2. Prepend a header above the five sections:
   - A title line: `# Session checkpoint — YYYY-MM-DD — <short topic>`
   - A line naming the dated archive filename this checkpoint is also saved
     as
   - A line naming the repo(s) and branch(es) touched this session

3. Write the full result to BOTH:
   - `.claude/handovers/YYYY-MM-DD-<short-topic-slug>.md` — a dated archive
     file, never overwritten
   - `.claude/handovers/latest.md` — always overwritten with the newest
     checkpoint

4. Commit with message `checkpoint: <topic> (YYYY-MM-DD)` and push with
   `git push -u origin <current-branch>`. If the push fails due to a network
   error, retry up to 4 times with exponential backoff (2s, 4s, 8s, 16s).

5. Confirm to the user in one line that the checkpoint is saved, and that
   next session they can say "/resume-session" or "where were we" to pick
   back up.

## Resume mode (user starts a session with "/resume-session" / "where were we")

When a session starts with "/resume-session", "resume", "where were we",
"pick up where we left off", "continue from last session", or "catch me up":

1. Run `git fetch origin` in `/home/user/testing`. The newest checkpoint may
   live on a `claude/*` branch rather than the default branch, since
   checkpoints are committed to whatever branch the prior session was
   working on. Check the currently checked-out branch's
   `.claude/handovers/latest.md` first. If that doesn't look current, run
   `git log --all --oneline -- .claude/handovers/` to find which ref holds
   the newest checkpoint commit, and read it directly with
   `git show <ref>:.claude/handovers/latest.md`.

2. If a checkpoint is found: brief the user with a compressed "Here's where
   we left off" summary covering the five sections, ending with the
   "Start here" action. Then stop and let the user redirect — do not ask
   clarifying questions first.

3. Fallback if NO checkpoint exists anywhere: reconstruct context from git
   evidence in BOTH `/home/user/testing` and `/home/user/unconsult-tools`:
   - `git log --all --since='30 days ago' --pretty=format:'%h %ad %an %s' --date=short`
   - recent `claude/*` branches in each repo
   - the diff of the most recent Claude-authored commits

   State clearly to the user that this summary is reconstructed from commits
   only, so any discussion-only context — decisions talked through but never
   turned into a commit — is missing and will need to be re-established.

4. Never delete old dated handover files. They are the permanent archive.
