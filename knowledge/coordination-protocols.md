# Coordination Protocols

Rules for plan presentation, progress reporting, result synthesis, and user communication.

---

## Delegation Plan Presentation

Before executing any agents, present the plan to the user:

### Plan Format

```
## Delegation Plan

**Goal**: [one-line summary of what the user wants]

**Agents**: [count] agents, [sequential/parallel/mixed] execution

| Step | Agent | Input | Output | Mode |
|------|-------|-------|--------|------|
| 1 | [name] | [what it receives] | [what it produces] | Sequential |
| 2a | [name] | [input] | [output] | Parallel |
| 2b | [name] | [input] | [output] | Parallel |
| 3 | [name] | [outputs from 2a+2b] | [output] | Sequential (gate) |

**Conditional gates**: [list any pass/fail checkpoints]
**Estimated agents**: [count] | **Execution mode**: [cost class]
```

### Plan Rules

- Present before executing unless spawned by another agent
- Name every agent, its input source, and expected output
- Identify parallel groups explicitly
- Mark conditional gates with pass/fail criteria
- State cost class: Light (1-2 agents), Standard (3-4), Heavy (5+)

---

## Progress Reporting

### Per-Agent Completion

Report immediately when each agent finishes:

```
✓ [agent-name] — [one-line summary of output]
  Artifacts: [list of produced files/documents]
  Duration: [time taken]
```

### Blocker Reporting

```
⚠ [agent-name] — blocked
  Reason: [what's preventing progress]
  Impact: [what downstream tasks are affected]
  Action: [what will be attempted next]
```

### Gate Results

```
Gate: [gate name]
Result: PASS / FAIL
Details: [one-line explanation]
Next: [what happens as a result]
```

---

## Result Synthesis

### Final Summary Format

```
## Execution Summary

**Goal**: [original goal]
**Status**: Complete / Partial / Failed

### Agent Results

| Agent | Status | Key Output |
|-------|--------|------------|
| [name] | Done | [one-line summary] |
| [name] | Done | [one-line summary] |
| [name] | Failed | [one-line error] |

### Deliverables

- [artifact name] — [file path or inline reference]
- [artifact name] — [file path or inline reference]

### Key Decisions

- [decision]: [rationale]

### Open Items

- [ ] [item needing user follow-up]
```

### Synthesis Rules

- One line per agent status — details in artifacts, not the summary
- Link to all produced artifacts
- Document key decisions and their rationale
- Flag open items that need human action
- Do not reproduce full agent outputs in the summary

---

## Communication Rules

| Rule | Description |
|------|-------------|
| Plan first | Always present delegation plan before executing |
| Progress as it happens | Report each agent completion, do not batch |
| Failures immediately | Do not wait until synthesis to report a failure |
| User language | Mirror the user's terminology, not agent internal names |
| No black box | User should always know what's running and why |
| Concise status | One line per agent, full details in linked artifacts |
| Adapt plans visibly | If the plan changes mid-execution, explain why |

---

## Agent Invocation Protocol

### Spawn Prompt Structure

```
You are the [agent-name] agent.

Task: [specific task description]

Context:
[relevant prior outputs, user requirements, constraints]

Scope:
- Include: [what to deliver]
- Exclude: [what NOT to do]

Expected output:
[format and content of the deliverable]
```

### Spawn Rules

- Include file paths where relevant
- Include full context from upstream agents (no lossy summarization)
- Specify acceptance criteria for the output
- For Haiku-tier agents: add explicit examples and detailed constraints
- Scope exclusions prevent agents from wandering into other agents' domains

---

## Anti-Patterns

| Pattern | Problem | Fix |
|---------|---------|-----|
| Serializing independent work | Wasted time | Identify and parallelize |
| Parallelizing dependent work | Race conditions, missing context | Enforce dependency order |
| Skipping gates | Quality/viability not validated | Gates are mandatory checkpoints |
| Summarizing context for downstream agents | Lost details | Pass full output |
| Silent failure handling | User unaware of issues | Report failures immediately |
| Wrapping single-agent task in team-lead | Unnecessary overhead | Route directly to the agent |
| Asking all agents for everything | Domain boundary violation | Match task to single agent |
