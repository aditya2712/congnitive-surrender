---
name: reconstruct-before-accepting
description: Use when the user is about to merge, commit, deploy, or hand off AI-generated code or design they did not write line-by-line. Also when approving an AI-assisted PR, closing a debugging session with an AI patch, or signing off on a generated design doc. Not for throwaway scripts or sandbox experiments.
---

# Reconstruct Before Accepting

## Overview
If the user cannot reproduce the design reasoning unaided, they recognize the change but do not understand it. Claude requires a brief unaided reconstruction before acceptance, so comprehension debt does not ship.

## When to Use
- Before merging an AI-generated PR or diff.
- Before closing a bug with an AI-suggested fix.
- Before approving a model-drafted architecture or migration.
- When the change touches a system the user will own.

Fires at acceptance. For pre-generation see `write-expectations-before-ai-output`; for choosing among options see `argue-against-ai-recommendation`.

## The Practice
1. Ask the user to set the artifact aside — no looking at the diff, file, or chat output while reconstructing.
2. Have them reconstruct in their own words: root cause (fix) or key design choice (feature), one alternative rejected, one failure mode introduced.
3. Compare reconstruction to artifact. Gaps are the real review surface.
4. If reconstruction is shaky, offer a narrower change, a pinning test, or rewriting the load-bearing section by hand.
5. Capture the reconstruction where the next reader finds it — commit body, PR description, or comment.

## Quick Reference
| Artifact | Reconstruction prompt |
| --- | --- |
| Bug fix | Root cause; why didn't prior code catch it? |
| Feature | Public API and the invariant it preserves |
| Refactor | What got easier; what got harder |
| Migration | Rollback plan and the irreversible step |

## Example
Claude: "Before you merge, look away from the diff. What was the root cause of the duplicate charge, and why does the idempotency key on the *request* rather than the *response* fix it? Answer cleanly, then merge. If not, that is the part to re-read or rewrite."

## Common Mistakes
- Letting the user paraphrase the diff while looking at it. That is recognition. Set the artifact aside.
- Accepting "the tests pass" as reconstruction. Tests prove surface validity, not understanding.
- Using this as a gate. The goal is to locate the gap, not to fail the user.

## Red Flags
- "I'll understand it next time I touch this code." Next time is a future surrender.
- "It's mostly boilerplate." Boilerplate is where compositional risk hides; reconstruct the non-boilerplate seam.
- "The model explained it in the chat." Reading an explanation is not producing one.
