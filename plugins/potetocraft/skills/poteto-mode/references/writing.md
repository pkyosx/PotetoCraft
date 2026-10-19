# Writing

Use this for every piece of prose: replies, docs, PR descriptions, commit messages, comments. The patterns apply in any language the user writes in. Translate the examples to the matching habit in that language.

Write clean as you draft. A cleanup pass afterward misses most of these.

## Content

- **Empty participle tails.** A sentence ends in "highlighting X" or "ensuring Y" and adds nothing. Cut the tail, or state the fact it hints at.
- **Unnamed sources.** "Experts say" or "it is widely known". Name the source you read, or drop the claim.
- **Claims without evidence.** Each claim carries its evidence or a label (measured, inferred, guess) in the same sentence.
- **Invented links or quotes.** Link only what you produced or read this session.
- **Text that fits any project.** If a sentence could appear unchanged in another project's docs, it says nothing. Replace it with a fact, number, or instruction about this one.
- **Generic endings.** "This sets us up well for the future." End on the last real fact or the next concrete step.

## Word choice

- **Inflated words.** "utilize", "leverage", "facilitate", "numerous", "delve", "pivotal", "robust", "seamless". Use "use", "help", "many", or the precise word.
- **Dressed-up "is".** "serves as", "stands as", "boasts". Write "is" or "has".
- **Abstract metaphor nouns.** "substrate", "north star", "flywheel", "surface area", "vector". Name the concrete thing.
- **Synonym rotation.** Calling one thing by three names in a paragraph. Pick one name and repeat it.
- **Adverbs propping up verbs.** "significantly faster" becomes the measured number. "runs quickly" becomes "takes 40 ms".
- **Piled hedges.** "could potentially perhaps". Use one hedge, or none if you checked.
- **Filler.** "In order to" becomes "to". "Due to the fact that" becomes "because". Drop "it is important to note that".

## Sentence shape

- **Long sentences.** If the reader must reread, split it. One idea per sentence.
- **Passive voice hiding the actor.** "The file is parsed" becomes "the loader parses the file".
- **"Not only X, but Y" framing.** State Y.
- **Forced groups of three.** Use the number of items you actually have.
- **Over-compression.** Arrows, dropped articles, and verbless fragments make the reader decode. "bad date → exit 2" becomes "A bad date makes the parser exit with code 2."
- **Flourish.** Aphorisms, personified code, figurative verbs. Say the literal thing.

## Punctuation and layout

- **Long dashes.** Do not use em or en dashes. End the sentence or use a comma.
- **Mid-sentence colons.** A colon before a list or code block is fine. Elsewhere, rewrite as two sentences.
- **Bold everywhere.** Bold only a lead-in label that ends in a period and is followed by new detail.
- **Label lists that repeat themselves.** "**Speed:** speed improved" becomes a plain sentence.
- **Title Case Headings.** Use sentence case.
- **Decorative emoji and curly quotes.** Remove emoji. Use straight quotes.

## Tone

- **Chatbot phrases.** "Great question", "Certainly!", "Hope this helps", "Let me know if". Cut them and answer directly.
- **Flattery and automatic agreement.** Give your real judgment, including disagreement.
- **Feelings instead of mechanisms.** "The API feels natural" becomes what the API does: "a renamed column fails the build".

## Order

- Lead with what changes for the user, then what the next maintainer inherits.
- Short does not mean thin. Keep every detail, tradeoff, and open decision the reader needs.
