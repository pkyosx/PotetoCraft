---
name: correct
description: Find the mistakes agents keep repeating in this repo and change the repo so the next agent cannot make them, preferring architecture, then types, then a check, then a test, with docs last. Use when the user asks to stop a repeated agent mistake or to make a correction stick.
disable-model-invocation: true
---

# Correct

The user keeps correcting agents in this repo for the same mistakes. Change the repo so the next agent cannot repeat them.

Assume every contributor is an agent that sees only the files it opened, copies the nearest example, and takes the shortest path that compiles. A good fix makes the change that looks right from one file correct for the whole repo. See [encode-lessons-in-structure](../poteto-mode/references/principles/encode-lessons-in-structure.md).

Leave every edit in the working tree for the user to review. Prepare a proposed commit split and report it. The user decides when and how to commit.

## 1. Find the mistake classes

Read, with read-only commands:

- Recent history, `git log --oneline -100`, and the diffs of fixes.
- Reverts, `git log --grep=revert -i`.
- Review comments on recent PRs, `gh pr view <n> --json comments,reviews`, if `gh` is available.
- Agent instruction files in the project, such as `AGENTS.md` or `CLAUDE.md`.
- Comments that explain a workaround or say "do not."
- The corrections the user gave in this conversation.

Group the mistakes into classes. A class counts once it has two real occurrences. Write down each occurrence with its evidence, such as a commit, a PR comment, or a line.

## 2. Pick the highest level that works

For each class, try these in order. Stop at the first one that makes the mistake fail.

1. **Architecture.** Make the mistake impossible. Give each piece of state one owner. Give each task one supported way. Hide internals so a wrong import fails. Replace hand-synced lists with one source. Remove old paths and dead code that an agent would copy.
2. **Types.** Make the bad state impossible to write.
3. **A lint or check.** When bad code still compiles, add a check whose error message names the file, type, or function to use instead. Use only tools the project already has. If the pattern is already common, fail only when a change adds more.
4. **A test.** Assert the behavior that broke. Fix or remove tests that pass when the behavior breaks, or fail when only internals change.
5. **Docs or agent rules.** Last, and only for judgment calls. Nothing fails when an agent skips a doc.

For each class, note why each higher level did not work.

## 3. Fix and prove

Fix the most frequent classes first. Keep each class's change separate so it can be reviewed on its own.

Prove each new check or test fails on a real past mistake. Recover the bad version with `git show <sha>:<path>` into the scratch directory, or rebuild the smallest copy of it there, and run the check against it. Paste the command and the failing output. Then run the check on the current tree and show it passes. Use a command that also runs in the project's CI.

An allowed exception goes on the offending line with a reason. Ask the user to approve each one.

## 4. Keep the rule table

Keep a table in the project's agent instruction file that pairs each rule with what enforces it.

| Rule | Enforced by |
|---|---|
| One sentence on what not to do | The check, type, test, or "doc only" |

When the user corrects you, fix the mistake and add the rule. If the rule was already there and nothing enforced it, that is a repeat. Fix it at the highest level that works in the same change. Remove a rule once its mistake can no longer happen.

## 5. Report and wait

Write the report per [writing.md](../poteto-mode/references/writing.md), then wait for the user.

**Reply.** Each class with its evidence (two or more occurrences), the level picked and why higher levels did not work, the proof that each new check fails on a real past mistake, the files changed, and a proposed split into separate commits with a draft message for each. Nothing has been committed. Wait for the user to say what to do next.
