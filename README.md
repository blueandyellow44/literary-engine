# Literary Engine

A multi-agent pipeline for long-form fiction. Extraction, generation, and judging, with every interpretive claim required to cite the passage it came from.

This is a case study. The code is private, because the corpus it was built on is not mine to publish. What follows is the architecture and, more usefully, what measurement actually showed.

## The problem

Ask a model for a novel and you get competent prose that reads like a knock-off. Not wrong, not ungrammatical, just hollow. It has the surface of literature and none of the pressure. Prompt engineering does not fix this, because the failure is not in any single sentence. It is in the shape of the whole thing.

The engine was an attempt to find out which parts of that problem are actually tractable.

## The architecture

Roughly thirty composable skills and fifteen orchestrating agents, in four stages.

**Extraction.** Four per-work extractors run against one reference book and produce cited craft studies: arc and structure, character, author voice, dialogue craft. They share a single turn-seam offset so their findings join at the same moment in the text. A separate judge grades each study for evidence integrity, method adherence, internal consistency, and transfer. The extractor never grades itself.

**Aggregation.** Graded studies roll up into a register profile, a synthesized lane assembled across several authors rather than an imitation of one. The design refuses author signature tics on purpose, since copying a fingerprint only produces pastiche. What it wants is the transferable mechanism, how a sentence is built, how a reveal is withheld, how a belief breaks at the turn.

**Generation.** Scene briefs fill, prose drafts, chapters assemble, with a structural gate before drafting and a continuity judge after.

**Verification.** This is where the engine actually lives. A continuity judge owns canon, timeline, and the per-character knowledge boundary. A prose critic owns line craft and originality. A developmental diagnostician runs twelve passes over a complete draft looking for hollowness, missing interiority, absent stakes, motif that has decayed into tic. A revision architect turns a diagnosis into a dependency-ordered rewrite plan. None of them may rewrite. The critic judges, a separate editor revises, and the loop iterates.

## Two design decisions that carried the weight

**Separate the countable signal from the interpretive one.** Sentence length, dialogue ratio, and paragraph distribution are deterministic and get stored as distributions. The turn, the withholding, the subtext, the wound, all of that requires a model pass, and every such observation must cite its source passage by offset so it can be checked. Mixing the two was treated as the central mistake, because an uncited interpretive claim is indistinguishable from a hallucination.

**A maker never judges its own work.** Makers, judges, and harness auditors run in separate blind contexts, connected by sealed maps. This sounds like process overhead until the first time a drafting agent audits its own draft and passes it.

## What measurement showed

The validation harness pre-registers conditions, hypotheses, metrics, and pass bars before any material is generated, seals them as commits, scores blind with multiple independent judges, and computes the verdict against the sealed bars rather than narrating one. Stop conditions can hard-stop a program, and the record shows them being honored when they tripped.

The most useful artifact the project produced is not the pipeline. It is a permanent Negative Results Canon, a registry of things that were tried and did not work, which governs the rest of the documentation. Eight entries so far. Two of them killed load-bearing ideas the architecture was originally built around. One records a method incident where offsets were fabricated and stamped as verified. One is a verdict the project overstated and then corrected against itself.

Each entry names what it forbids anyone from claiming later, including me. That constraint is why this page carries no headline numbers. The results that exist are model-judging-model with a single human ratifying, on a single subject, with test material authored from inside the program. Those limits are recorded in the manual alongside the price of fixing each one. They are good enough to steer the build and not good enough to put in front of you as a claim, so they are not going in front of you as a claim.

The honest summary: generation governance did not survive contact with measurement. The post-draft resistance stack, the diagnose-and-revise machinery, is the part that held up.

## What I would tell someone building this

Build the judge before the writer. The interesting engineering in a creative pipeline is not the generation, which is mostly prompt and sampling. It is the apparatus that can tell you the output is bad in a way you can act on, and that will not flatter itself when it is wrong.

Write down what failed, with teeth. A negative result you can cite is worth more than a positive one you cannot reproduce, and a canon that forbids future overclaiming is the only thing I found that reliably stops a project from believing its own marketing.

## Related

- [Voice Gate](https://github.com/blueandyellow44/voice-gate), the diagnose-only voice instrument that came out of this work, and is public as code.

## License

MIT, for this document.
