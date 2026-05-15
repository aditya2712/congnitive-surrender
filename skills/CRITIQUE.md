# Critique of Cognitive Surrender Skills (Round 2)

Fresh critic pass on the three skills the Creator produced from Addy Osmani's "Cognitive Surrender" essay. A prior critique exists in this slot; this pass starts from the current SKILL.md files, not from that history.

---

## Cross-cutting issues (apply to all three)

**[Blocker] Description does not start with "Use when...".** The format spec explicitly requires `description` to start with "Use when...". All three currently start with "Use before..." or "Use after...". This is the most common skill-system loader-pattern requirement and the brief flagged it as load-bearing. Easy to fix without changing meaning ("Use when about to generate..." / "Use when a recommendation has just been made..." / "Use when the user is about to merge...").

**[Major] Word budget exceeded.** Target is ~400 words.
- `write-expectations-before-ai-output`: 411
- `argue-against-ai-recommendation`: 434
- `reconstruct-before-accepting`: 464

The prior CRITIQUE.md claimed to have trimmed all three under 400 — that claim is not borne out by the current files. Real trims needed, not cosmetic ones.

**[Minor] Cross-reference pointers.** Each skill references the other two by name in "When to Use". Good for coherence but adds words without changing behavior. Tolerable; keep but tighten.

---

## Skill 1: `write-expectations-before-ai-output`

### Fidelity
Maps cleanly to essay practice #1 ("Write down what you expect *before* looking at the AI's output") and the "borrowed confidence" mechanism in the "Why This Matters" section. No drift into generic AI hygiene.

### Issues

**[Blocker] Description does not start with "Use when...".** Currently: "Use before generating non-trivial code, a debugging diagnosis...".

**[Major] 411 words.** Trim Quick Reference and tighten Practice step 4.

**[Minor] Practice step 5 ("If the user declines to predict, flag that any acceptance from here rests on surface signals only.").** Useful loophole-closer; keep but tighten phrasing.

**[Minor] "NOT for syntax recall, formatting, or one-line edits" appears in both description and When to Use — duplication.** Trim from one.

### Example
Race-condition prompt is concrete and plausible. Keep.

### Red Flags
All three close real surrender loopholes (compile-passing as proxy for correctness, confidence transfer, deferred reading). Keep.

---

## Skill 2: `argue-against-ai-recommendation`

### Fidelity
Maps to essay practice #3 ("Ask the model to argue *against* its own recommendation"). Note one principled adaptation: the essay asks the *engineer* to prompt the model; this skill has *Claude* proactively steel-man the counter. That is a defensible operationalization given the skill drives Claude's behavior, and it directly counters the "Confidence transfer" vulnerability the essay calls out.

### Issues

**[Blocker] Description does not start with "Use when...".**

**[Major] 434 words — worst-but-one.** Quick Reference is the heaviest section; trim a row or shorten Practice step 3.

**[Minor] Practice step 3 lists five conditions in one line ("scale, team size, latency budget, ops maturity, reversibility").** Fine as a menu, but the user may read it as a required checklist. Soften to "such as".

**[Minor] Overview says "A single confident recommendation invites cognitive surrender."** Good — invokes the essay's vocabulary directly. Keep.

### Example
Postgres LISTEN/NOTIFY vs dedicated queue is a real, recognizable architecture choice. Strong.

### Common Mistakes / Red Flags
"Producing a weak counter so the original wins by default" closes the theater-counter loophole — exactly the failure mode that makes this practice degrade silently. "We are already mid-implementation" red flag is sharp. Keep both.

---

## Skill 3: `reconstruct-before-accepting`

### Fidelity
Maps to essay practice #5 ("Make sure you can reconstruct the design reasoning on your own") AND directly addresses the "Comprehension Debt" section. Strongest fidelity of the three; the example invokes the essay's "Compositional risk" idea verbatim in the boilerplate red flag.

### Issues

**[Blocker] Description does not start with "Use when...".**

**[Major] 464 words — most over budget.** Practice step 4 and the Quick Reference are the biggest opportunities.

**[Minor] Practice step 1: "Ask the user to set the artifact aside (close the diff)."** In a Claude chat, "close the diff" is awkward; the artifact may have been pasted into the conversation. Better: "Ask the user to set the artifact aside — not look at the diff, file, or chat output while reconstructing."

**[Minor] Step 5 ("Capture the reconstruction...")** is good and generalized, but assumes there is a downstream reader. Keep — comprehension debt is fundamentally a multi-reader problem, and the essay's framing supports this.

### Example
Idempotency-key-on-request-vs-response is load-bearing and concrete. Strong.

### Common Mistakes / Red Flags
"Letting the user paraphrase the diff while looking at it. That is recognition." names the precise failure mode. "It's mostly boilerplate. Boilerplate is where compositional risk hides" invokes the essay directly. Excellent.

---

## Cross-skill coherence

The three skills line up on a timeline:
- `write-expectations-before-ai-output` — fires **before** Claude generates.
- `argue-against-ai-recommendation` — fires **after** a recommendation, **before** commit to a path.
- `reconstruct-before-accepting` — fires **before** merge/deploy/handoff.

This is clean. No unnecessary overlap. The Overview/When-to-Use sections already make this explicit.

---

## Summary of changes made in rewrite

1. Rewrote every `description` to start with "Use when..." (blocker fix across all three).
2. Trimmed every skill below 400 words by shortening Quick Reference rows, collapsing Practice steps, and removing duplicated trigger language between description and When to Use.
3. Softened the "scale, team size, latency budget..." enumeration in `argue-against` to a non-exhaustive list.
4. Rephrased the "close the diff" instruction in `reconstruct` so it works in a chat context where the artifact may be in the conversation, not in a diff viewer.
5. Tightened `write-expectations` step 5 to one line.

No structural rethinks needed — the Creator's framing of each skill against a specific essay practice is sound. All three drive Claude's behavior (asks the user, produces a steel-man, prompts for reconstruction) rather than slipping into human-only checklist mode.

---

## Verdict

SIGN-OFF: YES

Rationale: The three skills map to specific essay practices (1, 3, 5) and the comprehension-debt concept; they drive Claude's behavior in a chat, not the human's solo workflow; examples are concrete; Red Flags close real surrender loopholes including the most subtle ones (theater counter-arguments, recognition-vs-reconstruction, boilerplate as compositional-risk hiding place). After this round's rewrites, the two real blockers ("Use when..." prefix, ~400-word budget) are fixed and the minor phrasing issues addressed in place. No further Creator round needed.
