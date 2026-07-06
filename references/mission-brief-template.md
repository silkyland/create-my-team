# Mission Brief Template

Every team member gets one of these — complete, self-contained, no
references to a conversation the member can't see. The brief is the
contract; the integration gate enforces it.

## Template

```markdown
# Mission Brief: <member-id> — <one-line role>

## Objective
<2–4 lines: exactly what this member must produce. One objective per
member — a brief with "and also" in it is two briefs.>

## Context you need
<The minimum: project root, relevant paths, the mission's one-paragraph
summary, decisions already made that bind this member. Complete enough to
act alone; short enough to leave room for the actual work.>

## Scope
- IN: <paths/topics this member owns>
- OUT: <adjacent things it must NOT touch — the sibling members' scopes,
  files that must not change, decisions above its pay grade>

## Evidence rules
- Every claim about the codebase: `file:line`.
- Every claim about a framework/library/API: vendor path or docs URL +
  version, checked now — training-data memory is not a source.
- Unverifiable statements: tag UNVERIFIED with what would verify them.
- If you find something that contradicts this brief, REPORT it — do not
  silently work around it.

## Output contract
<Exact deliverable shape — this is what the integration gate checks:>
- Format: <markdown report / patch / file list / structured findings>
- Required sections: <...>
- Write to: <.team/<member-id>/report.md or return as final message>
- Length budget: <keep members from writing novels>

## Boundaries
- Read-only / may modify only <paths> (in your own worktree).
- Do not install packages / call external services / spend beyond scope
  without flagging it back first.
- Timebox: <N> minutes of focused work — if you can't finish, return
  partial results with an honest DONE/NOT-DONE list rather than nothing.
```

## Writing rules for the lead

- **Scopes across briefs must tile, not overlap** — read all briefs
  together before spawning; every mission-critical area appears in
  exactly one IN list.
- Put decisions IN the brief, not questions — members that come back
  asking what you already knew wasted their run.
- The output contract is the merge plan: if you can't say how you'll
  combine two members' outputs, their contracts aren't specific enough
  yet.
- Reused briefs drift: re-derive from the template per mission; copy-paste
  briefs carry stale scopes from the last mission.
