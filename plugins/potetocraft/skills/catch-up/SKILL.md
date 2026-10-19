---
name: catch-up
description: Catch the user up on what changed in this conversation since their last message, in plain words with small text diagrams, and list every item waiting on them with what they need to decide it. Use when the user asks to be caught up or asks what they missed.
disable-model-invocation: true
---

# Catch up

The user stepped away. Tell them what changed since the last message they wrote, and lay out every decision waiting on them so they can make it from your reply alone.

Assume they remember their own last message and nothing after it. Tool results, notifications, and subagent reports are not their messages.

## Rules for this turn

- Read only. Do not edit files, start jobs, run the app, or post anything.
- You may run read-only commands to check the current state of anything this conversation touched, such as `git status`, `git log`, or `gh pr view`.
- Check every number and status against its source before you show it. If you correct an earlier claim, say so.

## Gather

1. Collect your own work since their last message, every subagent report, and any messages from others in this conversation.
2. Check the current state of each branch, PR, test run, or subagent the conversation touched.
3. Find every action item. An action item is a step only the user can take. A product choice, an approval, something irreversible, or access you lack. Include items raised before their last message that still wait on them. Work you can still do yourself is not an action item. Never invent one to fill space.

## Write

Use plain words, like one person catching up another. Say what changed for the user, not how you did it. "The tests pass," not "CI is green." Leave out hashes, paths, and commands unless the user needs one to act. Call each PR, branch, or subagent by a name the user would know.

1. **Opening line.** One sentence naming what waits on the user, or saying nothing does. If nothing happened and nothing waits, say so and stop.
2. **What happened.** One bullet per thing the user asked for. What came of it, and whether it is done, running, failed, or unchecked. Each bullet must stay true when read alone. Name any bug found and fixed along the way. Keep this part under about 100 words.
3. **What changes for you.** At most three lines on facts that change what the user knows or must do.
4. **Work left for me.** One line on work you can still do without them.
5. **Waiting on you.** Every action item. For each, give the call to make, your pick, what it changes for users, the evidence behind your pick, and its risk, even when low. Give the PR number or link when you have one. Mark any unknown fact as "unknown." When items share one call, state the call and pick once, then one bullet per item, riskiest first. For a choice between options, give each option's gain and cost.

Never drop or shrink an action item to save words. The reply grows with the number of items.

## Visuals

Use a small text visual only when a picture explains faster than a sentence. How parts connect, a chain of dependent PRs, a before and after. Use a plain text diagram or Mermaid. At most six boxes, at most eight words in each, labels in plain words. Never draw a status list or a list of action items. A Markdown table is not a visual. Never show a fact twice.

Follow [writing.md](../poteto-mode/references/writing.md).

**Reply.** The opening line, what happened, what changes for the user, work left, and every action item with what the user needs to decide it.
