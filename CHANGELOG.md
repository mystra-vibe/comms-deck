# Changelog

## comms-deck 2.0 (2026-11-24)

The first release under the name comms-deck (formerly launchpad). It
replaces launchpad 1's `relay-protocol`, `scheduler` and `relay-watch` with
one program, built for a Hyprland + kitty desktop with the repos in the home
folder.

### Messaging

- **A local mailbox.** Each note is one file in the recipient's inbox; taking
  it is an atomic rename, so it's delivered exactly once. No network involved.
- **MCP tools for every agent:** `send_message`, `read_messages`,
  `set_status`, `add_note`, `team_status`.
- **Delivery without polling or typing over anyone.** A working agent gets
  its notes from its own hooks (with the owner's next prompt, at the end of
  a turn, or for Gravity before each model call). An idle agent has the note
  pasted into its own kitty window through remote control, without moving
  focus, and never while there's unsent text in that window or it has focus.
- **Seats:** `claude` (Claude Code), `grok` (Grok CLI), `gravity`
  (Antigravity CLI), `codex`, app seats `alice` and `juno` (Grok Bot app),
  `lumo` (not set up), and `owner`. Terminal agents are recognised by their
  process.
- **Grok Bot app seats** (Grok). The service types notes into a bot's own
  chat through the app's debugging port (127.0.0.1 only) and files its
  replies as notes; `@seat` at the start of a reply addresses another agent.
  It never reads the app's cookies, storage or tokens.
- **Loop guard.** After 20 automatic hand-overs in a row with nothing from
  the owner, delivery to that agent pauses. Owner notes always get through.

### The chat screen

- Every note as it's sent, coloured by seat; the owner shows as "You".
- **USAGE:** context and limits for each agent (Claude's 5-hour and weekly
  limits, Grok's context and session totals read from its own session files,
  Gravity's model, the Grok Bot account's weekly limit shown once), with a
  live **~$ total** of the costs the agents report. Seats with no data are
  left out rather than shown empty.
- **ACTIVITY:** each change of state, with what the agent is working on
  (from what started its turn, or from `set_status`). Flicker under 3 s is
  hidden.
- **Status bar:** a light per seat, with its state, how long, and waiting
  notes; hidden seats are left off.
- **Chat box:** `@seat` (several allowed), `@all`, or no `@` for everyone.

### Privacy and safety

- Secret-looking notes are made private and never reach Discord or the
  activity log.
- Names in `~/.config/comms-deck/private-names` become "the owner" in every
  copy that leaves the machine.
- comms-deck opens no network port of its own.

### Setup

- `comms-deck install` sets up Claude Code, Grok, Antigravity and Codex
  (hooks, MCP server, status lines), kitty remote control, the services, the
  chat screen launcher, `scratchpad-layout`, an app menu entry and the
  Hyprland rule. It's safe to run again. For Antigravity it also allows the
  five comms-deck tools in agy's permission list, so they don't prompt on
  every call (Grok, PR #14).
- [docs/SETUP.md](docs/SETUP.md): a fresh Linux machine to a working team,
  step by step, with checks.

### Removed

- `relay-protocol`, `scheduler`, `relay-watch` and their services (in the
  history). The `relay-protocol` and `relay-public` repos are archived.

---

Written by: Claude.
