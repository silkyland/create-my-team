# Spawn Protocol

How to discover, use, and survive the platform's actual multi-agent
machinery. Platform-generic by design — this skill runs under Claude
Code, Codex, OpenCode, and whatever ships next month.

## Capability probe (always first)

Check the LIVE session, not memory:

1. **Inventory spawning tools** actually present in your tool list —
   names vary: agent/task launchers, workflow orchestrators, background
   task runners, dedicated multi-agent APIs. If the platform documents a
   tool's parallelism/limits in its schema or description, record that as
   the ground truth.
2. **Known shapes (verify, don't assume):**
   - *Claude Code:* an Agent/Task tool for subagents (parallel when
     launched in one batch); a Workflow tool on some setups for scripted
     fan-out; background Bash for processes.
   - *Codex CLI:* multi-agent tool families (spawn/wait/send-input/close)
     on recent versions.
   - *OpenCode / others:* subagent or task tools where configured.
3. **Record before designing:** mechanism, max concurrent members,
   how results return (final message? file? stream?), timeout behavior,
   isolation options (worktree? sandbox?), and whether members can be
   messaged mid-run.
4. **CLI fallback:** with no in-platform spawning but other agent CLIs
   installed (claude/codex/opencode… in headless mode), background shell
   invocations can stand in as team members — costs the user's other
   subscriptions: consent first (see jury-my-repo for the pattern).

## Degraded mode (no spawning at all)

Honesty over theater:

- Declare it: "no subagent capability in this session — running the team
  plan sequentially myself."
- Keep the STRUCTURE: same briefs (worked one at a time), same phase
  order, same integration gate applied to your own phase outputs, same
  attribution table (`scout-1 (self)`).
- The value of the skill is the discipline, not the concurrency; a
  sequential team still beats an unstructured ramble.

## Spawning rules

- **One brief per member** (mission-brief-template.md), passed complete —
  members don't see the conversation; a brief that references "as
  discussed above" hands the member nothing.
- **Batch independent members in one launch** where the platform allows —
  that's what makes them actually parallel.
- **Timebox every member.** Default 10–15 min equivalent; on timeout:
  kill, log, reassign or report. Never wait indefinitely, never silently
  drop the scope.
- **Isolation for writers:** members that modify files get separate git
  worktrees (or the platform's isolation option). Read-only members run
  bare. Two writers in one directory is a merge conflict you scheduled.
- **ONE-WAY actions stay with the lead:** members never push, delete
  outside their worktree, call external services with side effects, or
  publish — their briefs say so (Boundaries section). Everything a member
  does must be revertible at the integration gate; anything that isn't
  is executed by the lead, post-gate, user-confirmed.
- **Results are artifacts:** prefer members returning to files
  (`.team/<member>/report.md`) or structured final messages per their
  contract — parseable, diffable, attributable.
- **Mid-run interaction** (platforms that support send-input): use it to
  redirect a member that's drifting, not to micromanage; if a member needs
  three corrections, its brief was wrong — fix the brief, respawn.

## Cost discipline

Members multiply token spend. Before spawning: members × expected scope ≈
cost note in the plan gate. During: prefer completing a smaller team over
expanding mid-mission; expansion is a user decision, not a reflex.
