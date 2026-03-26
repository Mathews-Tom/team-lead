# team-lead

Multi-agent orchestration engine that decomposes complex requests into agent-sized tasks, delegates to specialized agents, manages execution order and dependencies, and synthesizes results into unified deliverables. The conductor that coordinates architecture, implementation, content, research, and release pipelines.

[![gitagent registry](https://img.shields.io/badge/gitagent-registry-blue)](https://registry.gitagent.sh)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## Run

```bash
npx @open-gitagent/gitagent run -r https://github.com/Mathews-Tom/team-lead
```

---

## What It Can Do

- **Task Decomposition** — breaks complex goals into agent-sized units with dependency graphs and parallel execution paths
- **Agent Delegation** — matches tasks to specialized agents with surgical accuracy based on domain capabilities
- **Workflow Patterns** — applies Build, Validate-then-Build, Research-and-Propose, Ship, and Content patterns
- **Conditional Gates** — enforces audit-before-ship, validate-before-build, and research-before-write checkpoints
- **Progress Tracking** — reports status as each agent completes, flags blockers, adapts plans when outputs change constraints
- **Result Synthesis** — collects multi-agent outputs into unified summaries with deliverable links and open items

---

## Structure

```
team-lead/
├── agent.yaml
├── SOUL.md
├── RULES.md
├── README.md
├── icon.png
├── banner.png
└── knowledge/
    ├── agent-capabilities-index.md
    ├── delegation-patterns.md
    └── coordination-protocols.md
```

---

## Built with

Built for the [gitagent](https://gitagent.sh) ecosystem.
