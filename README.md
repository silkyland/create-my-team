# create-my-team

**Spawn a disposable team of subagents around any mission — research
first, plan gate, and an integration gate that checks every member's work
before it merges.**

`create-my-team` is an [agent skill](https://vercel.com/docs/agent-resources/skills)
for general-purpose multi-agent work: one agent doing a big task serially
is slow and single-minded, but an unmanaged swarm is worse. This skill
adds the management: capability probe, right-sized topology, standardized
mission briefs, and two gates that make a team of fallible members
produce reliable work.

## How it works

```
/create-my-team "Research and implement rate limiting across our API" max-agents: 6
```

1. **Frame the mission** — objective, deliverable, done-when, mission
   class (research / build / audit / migrate).
2. **Capability probe** — what subagent machinery does THIS session
   actually expose (Claude Code agents/workflows, Codex multi-agent tools,
   OpenCode subagents, headless CLI fallback)? Verified live, never
   assumed. **No spawning capability = honest degraded mode**: same
   briefs, phases, and gates, run sequentially — the discipline survives
   even when the concurrency doesn't.
3. **Team design** — the smallest topology that fits: **scout swarm**
   (parallel research), **pipeline** (staged handoffs), **panel + judge**
   (independent attempts, adjudicated), **manager–worker** (work-list
   fan-out). Every member gets a self-contained mission brief with scope,
   evidence rules, and an output contract — the contract is the merge
   plan. Recommending *no team* ("one careful agent is enough") is a
   valid outcome.
4. **Research phase — always first** — scouts return claims with
   citations; the lead spot-checks surprising ones before they enter the
   plan. A scout's confidence is not evidence.
5. **Plan gate** ⛔ — the synthesized plan (who builds what, rough cost)
   goes to the user before any executor spawns. Deep implementation
   missions can hand off to [deep-plan](https://github.com/silkyland/deep-plan)
   here.
6. **Execute + integrate** — writers get isolated worktrees; every member
   is timeboxed; every deliverable passes the **integration gate**:
   contract compliance, evidence spot-check (one fabricated citation =
   full re-verification), run-it-if-runnable, scope audit, sibling
   conflict check. One retry, then escalate — never silently absorbed.
7. **Report with attribution** — member / scope / delivered / gate result
   (PASS, FIX-AND-RETRY, REJECT, TIMEOUT). A hard mission where everything
   passed first try is a smell, not a flex.

## The skill family

| Skill | Moment |
|-------|--------|
| [know-my-repo](https://github.com/silkyland/know-my-repo) | Day one: onboard onto a repo with zero knowledge |
| [deep-plan](https://github.com/silkyland/deep-plan) | Plan the next feature/refactor — evidence-gated |
| [deep-plan-ingest](https://github.com/silkyland/deep-plan) | Distill an accepted plan into living knowledge files |
| [clean-slate](https://github.com/silkyland/clean-slate) | Reset rotten knowledge files — backup-gated |
| [transform-my-repo](https://github.com/silkyland/transform-my-repo) | Change the architecture: migration feasibility + strategy |
| [twin-my-site](https://github.com/silkyland/twin-my-site) | Extend the web product with a native mobile twin |
| [jury-my-repo](https://github.com/silkyland/jury-my-repo) | Multi-agent adversarial audit with a verified verdict |
| [love-me-love-my-docs](https://github.com/silkyland/love-me-love-my-docs) | A user manual that regenerates itself |
| [seed-ah](https://github.com/silkyland/seed-ah) | Fake-but-production-like demo data with a manifest |
| **create-my-team** | Spawn and manage a subagent team for any mission |

Shared law: **no claim without evidence** — here: a subagent's output is a
claim, and the integration gate is where claims become results.

## Install

```bash
npx skills add silkyland/create-my-team
```

Or copy this directory into your agent's skills folder
(e.g. `~/.claude/skills/create-my-team/`).

## Structure

```
create-my-team/
├── SKILL.md                              # 7-step workflow + the two gates
└── references/
    ├── team-topologies.md                # 4 topologies + selection and sizing rules
    ├── spawn-protocol.md                 # Capability probe, spawning rules, degraded mode
    ├── mission-brief-template.md         # The per-member contract
    └── integration-gate.md               # 5 checks, gate outcomes, attribution table
```

Follows the [Vercel skills](https://github.com/vercel-labs/skills) single-skill
layout and [Anthropic's skill authoring best practices](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices).

## License

MIT
