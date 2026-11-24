# Load Balancer: Routes Reviews Too

**Author:** Lumo (lumo seat) · **Date:** 24 Nov 2026 · **Status:** draft for review
**Complements:** the owner's announced load balancer — task routing by availability.
Canonical draft lives in the lumo chat; this is the working copy for the deck.

## Problem

This morning's bottleneck was not writing code. Features landed fast all day (quantum-kittens #35, the availability ordering, the six-word lines, alice's boot-loop fix #37). What stalled was **review throughput**: everything queued behind a two-person reviewer pool (claude and grok), while gravity, codex and lumo sat outside it. Grok was flagged "urgent, please review #37" while the machine's other seats idled. A task nobody verifies is not done, so routing reviews is not a nice-to-have — it is the load balancer's core job.

## Requirements

1. **Reviews are tasks.** The router treats "review PR N" as a routable task, weighted by urgency (age × merge-blocking flag), not by arrival order.

2. **Reviewer pool by capability, not availability alone.** Eligible reviewers are seats that can actually open a diff: claude, grok, gravity (via her own tools), lumo (web + local file access). Codex is paused; alice and juno stay out — they are chat seats, not reviewers. Availability orders *within* the pool; it does not define the pool.

3. **Spent and stuck seats are skipped.** A seat that is `idle until` (grey) or `stuck` is never handed a review. If the whole pool is unavailable, the review escalates to the owner rather than waiting silently.

4. **One reviewer per change, assigned atomically.** The router claims a review by writing an assignment file before announcing it, so two idle agents never both start (the duplicate-work rule, enforced by machine instead of etiquette).

5. **The reviewer writes their own `Reviewed by:` line.** This is deck law already; the router must never stamp approval on a reviewer's behalf, and must never auto-approve after a timeout. Silence is not sign-off.

6. **Routing is visible.** Every assignment appears on the chat screen like a note does: who has it, since when, and what unblocks it. Invisible routing is indistinguishable from dropped work.

7. **Nothing merges by machine.** The owner merges. The load balancer proposes, files, and reminds — it does not push to main, ever.

## Non-goals

- Waking a spent agent early.
- Routing `@deck` desktop actions (that mechanism stays as built).
- Replacing `team_status` etiquette notes — those stay for humans; the router is for claims and hand-offs.

## Suggested shape

A small scheduler sitting beside the deck, not inside it: it watches the PR queue (via the existing GitHub access `push-courier` already has), maintains `reviews/<pr>.json` assignments under the deck's data dir, and announces each assignment as a normal note. Name is free; Chronophage already covers scheduled waking, so this only needs to cover claiming and escalation.

## Acceptance check

The morning's failure replays as: #37 lands in the queue at "urgent", the router offers it to the highest-ranked available reviewer, marks it claimed so nobody duplicates it, and — if that reviewer is spent — offers it to the next seat in the pool within a minute instead of waiting for a human to redistribute it.
