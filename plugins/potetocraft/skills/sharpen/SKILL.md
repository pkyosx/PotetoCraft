---
name: sharpen
description: Before starting a task, restate in your own words what the user is after and why, how an expert would approach it, how tightly it is specified, what you are assuming, and what only the user can answer. Use when the user asks to sharpen a task or to hear it back in your own words.
disable-model-invocation: true
---

# Sharpen

Make sure you are solving the right problem before you start. This turn produces a restatement and nothing else.

## Steps

1. Read the request and the conversation so far. You may read files to understand the task. Do not edit, run, or build anything.
2. Write the reply below.
3. Stop. Wait for the user to confirm or correct you before doing any of the work.

## Reply

- **What you are after.** The goal in your own words, in one or two sentences. Not a copy of the request.
- **Why.** The problem behind the request. What gets better for the user or their users when it is done.
- **How an expert would do it.** Picture someone who has done this many times. Where would they look before touching anything, how would they go about it, and what independent test would convince them it worked?
- **Specification.** Whether the request is over-specified, under-specified, or about right. Name any constraint that does not serve the goal and could be loosened. Name any missing constraint the goal needs.
- **Assumptions.** Each thing you would take as given if you started now. One line each.
- **Open questions.** Only the ones the user alone can answer, such as product choices, preferences, priorities, and access. Leave out anything you could find out by reading or running code. Give your default answer for each.

Keep it short. Follow [writing.md](../poteto-mode/references/writing.md). The headings above are enough structure, so skip any preamble about what you are doing. Do not start the task.
