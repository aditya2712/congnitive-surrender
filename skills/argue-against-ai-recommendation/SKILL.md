---
name: argue-against-ai-recommendation
description: Use when a recommendation has just been made and the user is about to commit — architecture choices, library or framework selection, schema changes, or non-trivial refactors. Also when only one option has been presented, or the user says "sounds good" without naming a tradeoff. Not for stylistic preferences, isolated bug fixes, or sandbox experiments.
---

# Argue Against AI Recommendation

## Overview
A single confident recommendation invites cognitive surrender. Before the user commits, Claude produces the strongest opposing position so hidden tradeoffs surface while reversal is still cheap.

## When to Use
- After Claude or another model recommends an architecture, library, pattern, or schema.
- When the user says "sounds good, let's do it" without naming a tradeoff.
- Before any change with non-trivial reversal cost.

Fires between recommendation and commit. For pre-generation see `write-expectations-before-ai-output`; for pre-merge checks see `reconstruct-before-accepting`.

## The Practice
1. Restate the recommendation in one sentence, including its assumed context.
2. Produce the strongest opposing recommendation. Steel-man it — not a strawman.
3. Name the conditions under which the counter wins (scale, team size, latency budget, ops maturity, reversibility).
4. Identify which conditions actually hold for the user. Ask where they are uncertain.
5. Either re-affirm the original now that the counter has been engaged, or switch.

## Quick Reference
| Recommendation | Counter to steel-man |
| --- | --- |
| New service | Modular monolith |
| ORM | Raw SQL / query builder |
| Event-driven | Synchronous RPC |
| Rewrite | Strangler fig / leave it |

## Example
Claude: "I suggested Postgres LISTEN/NOTIFY for the job queue. Steel-man for the opposite: a dedicated queue (SQS, Redis) wins once you need retries with backoff, dead-letter inspection, or multiple consumer groups. You mentioned fan-out to multiple workers — that condition holds. Reconsider before I write the migration?"

## Common Mistakes
- Producing a weak counter so the original wins by default. If the counter is not defensible, search harder.
- Listing tradeoffs abstractly without mapping them to the user's context.
- Skipping because the recommendation "feels obvious." Obvious recommendations are the highest-risk surrenders.

## Red Flags
- "There is really only one way to do this." Almost never true; produce the counter.
- "The model already considered alternatives." It listed them; it did not steel-man them.
- "We're already mid-implementation." Reversal cost is rising — exactly when the counter is most valuable.
