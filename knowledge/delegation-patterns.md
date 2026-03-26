# Delegation Patterns

Standard workflow patterns, parallelization rules, and task decomposition strategies.

---

## Standard Workflow Patterns

### Build Pattern (New Project)

```
project-architect → project-planner → full-stack-builder → codebase-auditor → release-captain
```

**Use when**: Building a new project from scratch. Each step feeds the next.

**Parallelizable**: None — strictly sequential dependency chain.

### Validate-then-Build Pattern (Idea to Product)

```
idea-scout → [GO?] → project-architect → project-planner → full-stack-builder → release-captain
```

**Use when**: Starting from an unvalidated idea. Gate at idea-scout prevents wasted build effort.

**Gate**: If idea-scout returns NO-GO, halt and report findings. Do not proceed to architecture.

### Research-and-Propose Pattern (Consulting)

```
research-analyst  ─┐
project-architect ─┤→ proposal-writer
project-planner   ─┘
```

**Use when**: Client-facing engagement needs research, architecture, and timeline fed into a proposal.

**Parallelizable**: research-analyst, project-architect, and project-planner run simultaneously. proposal-writer waits for all three.

### Ship Pattern (Code Ready)

```
codebase-auditor → [PASS?] → release-captain
```

**Use when**: Code is written and needs quality validation before release.

**Gate**: If codebase-auditor returns FAIL, halt and report issues. Do not ship.

### Content Pattern (Publishing)

```
research-analyst → content-strategist → media-producer
```

**Use when**: Publishing content that needs research, writing, and visual assets.

**Parallelizable**: media-producer can run in parallel with content-strategist if visual requirements are known upfront.

---

## Decomposition Rules

### Task Sizing

| Criterion | Guideline |
|-----------|-----------|
| Single agent | Each task maps to exactly one agent's domain |
| Clear boundary | Input and output are well-defined |
| Independently testable | Output can be verified without other tasks |
| Time-bounded | Completes in a single agent invocation |

### Dependency Analysis

1. List all tasks
2. For each task, identify: what it needs as input, what it produces as output
3. Draw edges: if Task B needs Task A's output, A → B
4. Identify parallel groups: tasks with no shared dependencies run simultaneously
5. Identify gates: tasks whose output determines whether subsequent tasks run

### Parallelization Rules

| Rule | Description |
|------|-------------|
| Independence | Two tasks run in parallel only if neither needs the other's output |
| Resource safety | No two parallel tasks modify the same files or resources |
| Gate respect | Conditional gates are never parallelized with their dependent tasks |
| Fan-out limit | Maximum 3-4 agents in parallel to maintain coherent progress tracking |

---

## Context Passing

### Full Context Rule

Downstream agents receive the complete output of upstream agents. Never summarize away details that the downstream agent may need.

### Context Structure

```
Task: [specific description]
Context from [upstream agent]:
[full output or artifact reference]
Constraints: [scope, timeline, quality requirements]
Expected output: [what this agent should produce]
```

### What to Include

| Include | Exclude |
|---------|---------|
| Architecture decisions and rationale | Team-lead's internal planning notes |
| Data, numbers, specific findings | Status updates about other agents |
| Scope constraints and boundaries | Implementation details from unrelated agents |
| User's original request (verbatim) | Reformulated versions of the request |

---

## Failure Recovery

| Scenario | Action |
|----------|--------|
| Agent returns error | Retry once with adjusted parameters |
| Agent returns low-quality output | Provide more specific instructions, retry once |
| Retry fails | Escalate to user with error description and what was attempted |
| Gate fails (audit/validation) | Report issues, do not proceed past gate |
| Agent unavailable | Execute that agent's workflow inline if possible |
| Mid-workflow plan change | Pause, re-plan remaining steps, inform user |

### Escalation Format

```
[Agent Name] failed after retry.
Task: [what was attempted]
Error: [what went wrong]
Impact: [what downstream tasks are blocked]
Options: [suggested alternatives for the user]
```
