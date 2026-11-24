# Who wrote what

Several AI agents (Grok, Codex and Claude) build this repo together for
the repo's owner. This file records who wrote each part, so credit stays with the
right agent as the code changes hands.

**Joint work** means the agents built it together, and nobody recorded at
the time who wrote which lines. Those files are credited to all three
agents, and no agent claims them alone.

## The programs

| File | Written by | Notes |
| --- | --- | --- |
| [`comms-deck`](comms-deck), [`systemd/comms-deck.service`](systemd/comms-deck.service) | Claude (2026-11-24) | comms-deck. Replaces `relay-protocol` (joint: Grok, Codex, Claude), `scheduler` and `relay-watch` (Claude), which are in the git history. Keeps their message file format, the public/private split and the secret patterns. |
| `comms-deck`: Grok Bot app adapter (SECTION 7b), hook idle rules, promptId handling, the kitty draft check, the app-seat failure reason, Gravity's prompt line, model and tool permissions | Grok (2026-11-24) | PRs #11, #12, #13 and #14, reviewed by Claude. Grok also reviewed the usage reader and the activity descriptions. |
| `comms-deck`: chat screen, usage panel and ~$ total, activity log and set_status, app seats, the Gravity seat, name redaction, Grok usage reader, installer | Claude (2026-11-24) | |
| [`desktop/comms-deck-chat`](desktop/comms-deck-chat), [`desktop/scratchpad-layout`](desktop/scratchpad-layout) | Claude (2026-11-24) | |
| [`agent-chat/agent-chat`](agent-chat/agent-chat) | **Joint: Grok, Codex, Claude** | Built together before 2026-11-20. Claude added the comments on 2026-11-20, with no code changes. |
| [`agent-chat/install.sh`](agent-chat/install.sh), [`agent-chat/test.sh`](agent-chat/test.sh) | **Joint: Grok, Codex, Claude** | Claude added the header comments on 2026-11-21. |
| [`push-courier`](push-courier), [`systemd/push-courier.service`](systemd/push-courier.service) | Claude (2026-11-21) | Reviewed by Grok (2026-11-22); its findings were fixed before it landed here. On 2026-11-24 Claude moved it onto comms-deck's mailbox and paths. |

## The docs

| File | Written by |
| --- | --- |
| [`README.md`](README.md) | Joint: Grok, Codex, Claude (Claude wrote the current text) |
| [`agent-chat/README.md`](agent-chat/README.md), [`agent-chat/AGENTS.md`](agent-chat/AGENTS.md) | Joint: Grok, Codex, Claude |
| [`docs/BRANCHING.md`](docs/BRANCHING.md) | Claude (2026-11-20), from the owner's plan for test → main → live |
| `CREDITS.md` (this file) | Claude (2026-11-21) |
| The puzzle footer in `README.md`, [`puzzle/check.py`](puzzle/check.py) | Claude (2026-11-21), from the owner's idea |
| [`COMMS-DECK.md`](COMMS-DECK.md) | Claude (2026-11-22; rewritten 2026-11-24), from the joint work above |
| [`docs/SETUP.md`](docs/SETUP.md) | Claude (2026-11-24); reviewed and tested by Gravity |
| [`CHANGELOG.md`](CHANGELOG.md) | Claude (2026-11-24) |
| [`PRIMER.md`](PRIMER.md) | Claude (2026-11-22), from the team's record and the joint work of Grok, Codex and Claude |
| [`docs/REDUNDANCY.md`](docs/REDUNDANCY.md) | Grok (2026-11-24) |

## Work in progress

Open work, and who it belongs to, is listed in
[COMMS-DECK.md](COMMS-DECK.md#5-where-things-stand-as-of-2026-11-24). When a piece
lands here, add its row to the tables above.

## About the commit history

This repo starts from a single fresh commit that gathers the work done in
earlier, now private, repos. The credits above carry that work's
authorship forward. From here on, each commit names its agents in
`Co-Authored-By:` lines.

## Keeping this up to date

When you add or substantially change a file:

1. Put a `Written by:` line at the top of the file (in its "read this first"
   comment) or at the bottom of a doc.
2. When you build on someone else's file, **keep their credit** and add
   yours with what you changed and the date, as `relay-protocol` does.
3. Update the table here.
4. Add one `Co-Authored-By:` line per agent to the commit.
5. Agents who only reviewed go under `Reviewed by:`.

---

Written by: Claude
