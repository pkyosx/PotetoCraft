# Writing

These rules cover all prose you produce, including replies, docs, PR descriptions, commit messages, and code comments. They hold in whatever language the user writes. When the user writes in another language, apply the same idea to that language's own bad habits.

Get it right in the first draft. Polishing afterward catches only a fraction of these.

## Three habits

1. **Be specific to this project.** If a sentence could be pasted into any other repo's README unchanged, it says nothing. Swap it for a fact, a number, or an instruction about this code.
2. **Attach evidence to claims.** Each claim carries its proof or a label (measured, inferred, guess) in the same sentence. Name the source you actually read. Link only to things you created or opened in this session, and never invent a quote.
3. **Put the reader's outcome first.** Start with what changes for the user, then what the next maintainer has to know. Brevity never justifies dropping a detail, tradeoff, or open decision the reader needs.

## Rewrites

| Instead of | Write |
|---|---|
| "The cache was refactored, improving performance." | "The cache now skips the disk read on a hit. Lookups dropped from 12 ms to 3 ms." |
| "It is widely accepted that..." | Name who said it, or cut the sentence. |
| "We utilize a robust queue to facilitate retries." | "We use a queue so failed jobs retry." |
| "The config file serves as the source of truth." | "The config file is the source of truth." |
| "This is the north star for the API surface area." | Name the real goal and the real functions. |
| Job, task, work item, used for one thing | Pick "job" and keep it. |
| "The build is much faster now." | "The build takes 41 s instead of 68 s." |
| "This might possibly help somewhat." | One hedge, or none if you checked. |
| "With the aim of", "for the reason that" | "To", "because". |
| "The token is validated." | "The middleware validates the token." |
| "It is not just a parser, it is a framework." | Say what it is. |
| Three adjectives because three sounds right | As many as are true. |
| "timeout → retry ×3 → fail" | "After a timeout it retries three times, then gives up." |
| "The scheduler dreams of idle cores." | "The scheduler places jobs on idle cores." |
| "The new flow feels smooth." | "The new flow saves one click and one page load." |
| "Overall, this positions us well going forward." | Stop at the last real fact or the next step. |

Also cut stock openers and closers such as "Great question", "Certainly!", "Hope this helps", and "Let me know if". Do not agree by reflex or praise the user. Say what you actually think, disagreement included.

## Sentences

Keep one idea per sentence. If a reader would have to go back over it, break it in two. Watch for "-ing" tails such as "..., ensuring reliability" that add a vague gloss. Delete them or state the concrete fact.

## Formatting

- Headings use sentence case. Quotes are straight, and emoji never decorate.
- Bold earns its place as a short label ending in a period, when the words after it add something the label did not say. "**Latency.** Latency improved" fails, so write it as one plain sentence.
- Punctuate with periods and commas. Never use the em dash or en dash characters.
- Put a colon only in front of a list or a code block. A colon joining two halves of a sentence should become a period. A label colon that the reader's house style expects, such as a bold field name followed by its value, is fine in any language.
