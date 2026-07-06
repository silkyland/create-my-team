---
name: create-my-team
description: >-
  General-purpose multi-agent teamwork: for any sizable task, probes what
  subagent-spawning capability the current platform actually exposes
  (Claude Code agents/workflows, Codex multi-agent tools, OpenCode
  subagents — or none, with an honest sequential fallback), designs a team
  topology sized to the task (scout swarm, pipeline, panel-and-judge,
  manager-worker), sends every member a standardized mission brief,
  researches BEFORE executing, presents the synthesized plan at a user
  gate, then spawns the execution team and cross-checks every deliverable
  at an integration gate before merging. Use when the user wants to spawn
  agents or subagents, parallelize research or work across a team, says
  "use a team/multi-agent" for a task, or mentions create-my-team or
  /create-my-team.
license: MIT
argument-hint: "[mission] [max-agents] [research-only: yes/no]"
---

# Create My Team

One agent doing a big task serially is slow and single-minded. This skill
assembles a disposable team of subagents around any mission — scouts to
research, specialists to build, reviewers to check — with the two
guardrails that make teams trustworthy: **research before execution** and
**every deliverable verified before merge**. Members are testimony;
integration is where truth gets checked.

## The Prime Directive (family rule)

> **A subagent's output is a claim, not a result.** Every deliverable
> returned by a team member is verified at the integration gate (evidence
> citations spot-checked, contract compliance, does-it-actually-run)
> before it merges into the mission result. And the team itself follows
> the law: no member designs or builds before the research phase ends.

## Progress checklist

Copy this into your response and check items off:

```
Team Progress:
- [ ] Step 1: Frame the mission — objective, deliverable, done-when, constraints
- [ ] Step 2: Capability probe — what spawning tools ACTUALLY exist here
- [ ] Step 3: Team design — topology, size, one mission brief per member
- [ ] Step 4: Research phase — scouts out, evidence in, synthesis written
- [ ] Step 5: Plan gate ⛔ — user approved the plan before execution spawns
- [ ] Step 6: Execute — workers run, integration gate checks every deliverable
- [ ] Step 7: Report — results with per-member attribution, honest failures
```

## Step 1 — Frame the mission

Objective in 2–5 lines, the concrete deliverable, definition of done,
constraints (deadline pressure, budget/token sensitivity, files that must
not change), and the mission class — research / build / audit / migrate /
mixed — which drives the topology choice in Step 3.

## Step 2 — Capability probe

**Never assume the platform.** This skill runs on Claude Code, Codex,
OpenCode, and others; each exposes different (or no) spawning machinery.
Probe per [references/spawn-protocol.md](references/spawn-protocol.md):

- Inventory the ACTUAL tools available in this session (agent/task
  spawning, parallel workflows, background execution) — from the live tool
  list, not from memory of what the platform "usually" has.
- Record: mechanism, parallelism limit, result-return path, timeout
  behavior, isolation options.
- **No spawning capability = degraded mode**, declared honestly: the same
  phases run sequentially by you, with the same briefs, gates, and
  attribution ("scout-1 (self)"). The structure survives; the parallelism
  doesn't. Never fake a team.

## Step 3 — Team design

Pick the smallest topology that fits — catalog and selection rules in
[references/team-topologies.md](references/team-topologies.md):

| Topology | Use when |
|----------|----------|
| **Scout swarm** | unknowns dominate — parallel research, distinct non-overlapping scopes |
| **Pipeline** | staged work where each stage feeds the next (research → design → build → verify) |
| **Panel + judge** | quality via independent attempts or reviews, then adjudication |
| **Manager–worker** | a work-list of similar independent items (N files to migrate, N modules to document) |

Size to the task, not to the ceiling — every member costs tokens; a
3-agent team that finishes beats a 10-agent team that thrashes. Write one
**mission brief** per member from
[references/mission-brief-template.md](references/mission-brief-template.md):
scoped objective, inputs, output contract, evidence rules, what NOT to do.
Briefs are what make results mergeable — a member without a contract
returns prose you can't integrate.

## Step 4 — Research phase (always first)

Whatever the mission class, scouts go out before anything is built:
codebase reality, vendor/docs ground truth, prior art, constraints. Each
scout returns claims with citations per its brief. You (the lead)
synthesize — and spot-check surprising claims yourself before they enter
the plan; a scout's confidence is not evidence.

For missions that are pure research, Steps 4→7 complete the job (skip 5–6).

## Step 5 — Plan gate ⛔

Present the synthesized plan to the user BEFORE spawning executors: what
will be built/changed, by which team members, in what order, what it will
roughly cost (members × scope), and what stays untouched. One question,
recommended answer attached. **No execution spawns before the gate
clears.** For deep implementation missions, offer running **deep-plan**
here instead — this skill orchestrates; deep-plan specifies.

## Step 6 — Execute and integrate

- Spawn workers per the topology; parallel where scopes are independent,
  sequential where they feed each other.
- **Isolation for writers:** members that modify files get separate
  worktrees/scopes so they can't trample each other; read-only members
  don't need it.
- Timebox every member; a hung member is killed, logged, and its scope
  reassigned or reported — never silently absorbed.
- **Integration gate** per deliverable, protocol in
  [references/integration-gate.md](references/integration-gate.md):
  contract compliance, evidence spot-check, run-it-if-runnable, conflict
  check against sibling deliverables. Rejected work goes back with the
  gap named (one retry), then escalates to you or the user.

## Step 7 — Report

- The mission deliverable, assembled from gate-passed work only.
- **Attribution table:** member, scope, delivered, gate result
  (passed / fixed-after-retry / rejected / timeout) — the honest record of
  who did what.
- Failures and rejections stated plainly, with what was done about them.
- Cost summary: members spawned, wall time, anything the user should know
  before asking for a bigger team next time.
