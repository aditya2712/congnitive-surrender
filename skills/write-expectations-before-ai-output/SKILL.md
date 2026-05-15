---
name: write-expectations-before-ai-output
description: Use when about to generate non-trivial code, a debugging diagnosis, or an architecture suggestion the user will act on. Also when the user is in an unfamiliar area, is fatigued, or seems ready to accept output without inspection. Not for syntax lookups, formatting, one-line edits, or read-only exploration.
---

# Write Expectations Before AI Output

## Overview
Before substantive output exists, Claude asks the user for a short prediction and then compares it to what is generated. The delta exposes gaps in the user's mental model and blocks borrowed confidence.

## When to Use
- Before generating a non-trivial diff, function, or design proposal.
- Before stating a root-cause diagnosis for a bug.
- When the user is learning a new system or library.
- When the user is fatigued or rushing — surrender risk rises.

Fires *before* generation. For after-the-fact checks, see `reconstruct-before-accepting`.

## The Practice
1. Pause before producing the answer. Say what is about to be generated.
2. Ask for a one-sentence prediction: shape of the solution, files touched, suspected root cause, or expected API surface.
3. Generate the output.
4. State the delta in three lines: expected, actual, gap. Invite the user to interrogate the gap, not skim it.
5. If the user declines to predict, name it: acceptance from here rests on surface signals only.

## Quick Reference
| Situation | Prediction to elicit |
| --- | --- |
| New feature | Files touched, public API |
| Bug fix | Root cause in one sentence |
| Refactor | Which abstraction shifts |
| Architecture | Top tradeoff being made |

## Example
User: "Fix the race condition in the payment worker."
Claude: "Before I write the fix — in one sentence, what do you think the race is, and where will the lock or reordering land? I'll show the diff after and we compare."

## Common Mistakes
- Asking for a prediction *after* showing a draft. The anchor is already set.
- Accepting "I don't know" as a stopping point. A wrong guess is more useful than none.
- Treating the prediction as a quiz. It is calibration, not gatekeeping.

## Red Flags
- "It compiles, ship it." Run the prediction step now.
- "The model sounds confident." Confidence transfer in progress; require a prediction.
- "I'll just read it after." Reading after is recognition, not reconstruction.
