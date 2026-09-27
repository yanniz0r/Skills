---
name: commit
description: Stage and commit changes matching this repo's actual commit message conventions. Use when the user asks to commit, create a commit, or invokes /commit.
---

# Commit

Create a git commit that matches how the current repository's history is
actually written. Never assume a fixed style — infer it fresh from `git log`
every time, since it differs per repo.

## Steps

1. Run in parallel: `git status`, `git diff` (staged + unstaged), and
   `git log --pretty=format:"%s" -20`.
2. From that log, work out the convention in use:
   - Format: Conventional Commits (`type: summary` or `type(scope): summary`),
     plain imperative subject, or something else entirely.
   - If typed, which types actually recur (e.g. `feat`, `fix`, `chore`, `ci`,
     `docs`, `refactor`) — don't introduce a new one unless nothing existing
     fits.
   - Scope usage: present or absent, and its format if present.
   - Case and punctuation: lowercase vs. sentence case, trailing period or
     not.
   - Body usage: only for non-obvious *why*, wrapped at ~72-76 columns, or
     never used at all — match what's actually there.
   - Trailers: reproduce any recurring trailer pattern (e.g. issue refs,
     `Signed-off-by`). For AI attribution specifically, use this session's
     current attribution instructions (system reminder) verbatim — never
     fabricate a different model name, and never add an attribution trailer
     if the repo's history doesn't already carry one and none was asked for.
3. Decide what belongs in this commit. Only stage what's relevant to the
   change being committed — never `git add -A` or `git add .` blindly; name
   files explicitly. Flag anything that looks like a secret (`.env`,
   credentials) before staging it, and don't commit it without asking.
4. Draft the subject line (and body, if warranted) following the inferred
   convention, focused on *why* the change was made, not a restatement of the
   diff.
5. Stage the chosen files and commit in one shot using a HEREDOC so the
   message formats correctly:

   ```
   git commit -m "$(cat <<'EOF'
   <subject following inferred convention>

   <optional body>

   <trailers, if the repo's convention has them>
   EOF
   )"
   ```

6. Run `git status` after to confirm the commit succeeded and nothing
   unexpected got left uncommitted or staged.

## Rules

- Only commit when the user has asked for it in this conversation. If it's
  unclear whether "commit this" means now or later, ask.
- Never use `--amend` unless the user explicitly asks for it — hooks can fail
  a commit silently-ish, and amending in that case rewrites the wrong parent.
- Never pass `--no-verify`, `--no-gpg-sign`, or `-c commit.gpgsign=false`
  unless explicitly requested.
- If a pre-commit hook fails, fix the underlying issue, re-stage, and make a
  new commit — don't bypass the hook.
- Don't push. This skill only creates local commits.
- If the repo has no history yet (first commit), fall back to plain
  Conventional Commits and ask the user if they have a preferred style.
