# Team Topologies

Four shapes cover almost every mission. Pick the smallest that fits;
combine only when the mission genuinely has two phases with different
shapes (e.g. scout swarm feeding a pipeline).

## 1. Scout swarm (parallel research)

```
lead ──┬── scout A: codebase structure
       ├── scout B: vendor/docs ground truth
       ├── scout C: prior art / history
       └── scout D: constraints (CI, deploy, security)
            ↓ all return claims+citations
          lead synthesizes, spot-checks, writes the evidence base
```

- **Use when:** unknowns dominate; the mission starts with "find out".
- **Scopes must be distinct and non-overlapping** — overlap wastes tokens
  and produces contradictory duplicates the lead must reconcile.
- Scouts are read-only. Sizing: 3–5; beyond that, synthesis costs more
  than the scouting saved.

## 2. Pipeline (staged handoffs)

```
scout(s) → planner → builder(s) → verifier → lead merges
```

- **Use when:** stages feed each other; later work depends on earlier
  decisions.
- Each stage's output contract IS the next stage's input contract — define
  both in the briefs, or the handoff turns to prose.
- A stage that misses its contract blocks the line: fix at that stage,
  never patch downstream.
- For build pipelines, push a **walking skeleton** through all stages
  first — the thinnest slice that traverses the whole line, merged and
  run before the stages fill out. It proves every handoff contract at
  slice-one cost.

## 3. Panel + judge (independent attempts, adjudicated)

```
lead ──┬── attempt A (angle: minimal change)
       ├── attempt B (angle: framework-blessed way)
       └── attempt C (angle: performance-first)
            ↓
          judge scores against stated criteria → lead takes winner,
          grafts the best ideas from runners-up
```

- **Use when:** the solution space is wide and taste matters (design,
  naming, architecture, tricky algorithms) — or for review panels where
  each member gets a different lens (correctness / security / performance).
- Angles must be genuinely different, assigned in the briefs — three
  members with the same prompt converge and the panel buys nothing.
- The judge gets criteria, not vibes: state the scoring dimensions in its
  brief.

## 4. Manager–worker (work-list fan-out)

```
lead builds the work-list (evidence first!) ──┬── worker: item 1..k
                                              ├── worker: item k+1..2k
                                              └── worker: ...
            ↓ each returns per the same contract
          integration gate per batch → lead merges
```

- **Use when:** N similar, independent items — files to migrate, modules
  to document, endpoints to test.
- The work-list comes from a census (scout it first if unknown) — a
  guessed work-list means missed items reported as "done".
- **First batch is a skeleton batch of one item** — one worker, one item,
  through the integration gate and merged before the rest fan out. A
  wrong contract found after one item costs one item; found after N
  parallel batches it costs them all.
- Writers get isolation (worktree/scope split). Batch size: enough that a
  worker's overhead amortizes; small enough that a bad worker loses one
  batch, not the mission.

## Selection rules

1. Mission class research → swarm. Staged build → pipeline. Wide solution
   space or review → panel. Repetitive list → manager-worker.
2. **Default sizes:** swarm 3–5, pipeline 3–4 stages, panel 3 + 1 judge,
   workers ⌈N/batch⌉ capped by the platform's parallelism limit.
3. If the honest answer is "one careful agent is enough" — say so and
   skip the team. An unneeded team is pure overhead; recommending none is
   a valid outcome of this skill (family tradition).
