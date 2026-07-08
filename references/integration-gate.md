# Integration Gate

Where member output becomes mission result — or gets sent back. Every
deliverable passes ALL checks before merging; the gate is what makes a
team of fallible members produce reliable work.

## The checks, in order

1. **Contract compliance** — does the deliverable match its brief's
   output contract (format, sections, location, scope)? Off-contract work
   is returned with the specific gap named, even when the content looks
   good — un-mergeable good work is still un-mergeable. For briefs that
   carry Mission Questions, compliance includes **question coverage**:
   walk the numbers — every assigned question answered with evidence or
   tagged UNVERIFIED. A silently skipped question is a named gap,
   FIX-AND-RETRY.
2. **Evidence spot-check** — sample the citations: open 2–3 of the
   `file:line` references and confirm they say what the member claims;
   fetch one docs claim. One fabricated citation = full re-verification
   of that member's entire deliverable (fabrication is never isolated).
3. **Run it if it's runnable** — patches compile/lint/test; scripts
   execute; commands in docs actually work. "Looks right" is not a gate
   result.
4. **Scope audit (writers)** — diff the member's worktree: only IN-scope
   paths changed. Out-of-scope edits are reverted (and noted), even
   helpful ones — an untracked "improvement" is how missions grow
   surprises. A **ONE-WAY action** in a member's trail (a push, a
   deletion outside the worktree, an external side effect) skips the
   normal outcomes and escalates straight to the user — it can't be
   reverted at the gate, only reported.
5. **Sibling conflict check** — against already-merged deliverables:
   contradicting claims (two scouts asserting opposite facts → resolve
   with code, like jury-my-repo: no majority vote, code decides),
   overlapping edits, duplicated work. Resolve BEFORE merge; conflicts
   merged now are bugs found later.

## Gate outcomes

| Outcome | Action |
|---------|--------|
| **PASS** | merge; record in the attribution table |
| **FIX-AND-RETRY** | return once with the named gap(s); one retry per member — a second failure escalates |
| **REJECT** | scope reassigned (new member or the lead) or reported to the user as an honest hole |
| **TIMEOUT** | logged; scope reassigned or reported — never absorbed silently |

## Lead's own work

The lead's contributions (synthesis, any degraded-mode phase work) pass
the same gate, checked in the same order — self-merge without
self-review is how leads ship their own hallucinations while policing
everyone else's.

## The attribution table (final report)

| Member | Scope | Delivered | Gate result | Notes |
|--------|-------|-----------|-------------|-------|
| scout-vendor | framework ground truth | 14 cited facts | PASS | 2 spot-checks clean |
| builder-api | /api/v1 endpoints | patch, 6 files | FIX-AND-RETRY → PASS | missing test on first pass |
| scout-history | git trajectory | report | TIMEOUT | scope covered by lead |

Honest gate results are the point: a mission report where everything
passed first try on a hard task is a smell, not a flex.
