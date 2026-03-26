# Agent Capabilities Index

Complete reference of available agents, their domains, inputs, outputs, and routing signals.

---

## Agent Roster

| Agent | Domain | Model | Category |
|-------|--------|-------|----------|
| project-architect | System design, technology selection | Opus | Architecture |
| project-planner | Task breakdown, timeline, milestones | Sonnet | Planning |
| research-analyst | Multi-source investigation, analysis | Sonnet | Research |
| proposal-writer | Client proposals, ROI, pricing tiers | Opus | Content |
| full-stack-builder | Code implementation from spec | Sonnet | Implementation |
| content-strategist | Multi-channel content production | Sonnet | Content |
| release-captain | PR creation, release management | Sonnet | Shipping |
| codebase-auditor | Code quality assessment | Sonnet | Quality |
| idea-scout | Business idea validation | Sonnet | Validation |
| media-producer | Visual/video asset production | Sonnet | Content |

---

## Agent Input/Output Reference

### project-architect

| Input | Output |
|-------|--------|
| Project requirements, constraints | Architecture document, technology selection, system diagrams |
| Business goals, scale requirements | Component design, API contracts, data models |

**Routing signals**: "design the system", "choose the tech stack", "architecture for", "how should we build"

### project-planner

| Input | Output |
|-------|--------|
| Architecture doc, scope definition | Task breakdown, timeline, milestones, dependencies |
| Requirements, team constraints | Sprint plan, resource allocation, risk assessment |

**Routing signals**: "plan the project", "break this into tasks", "timeline for", "what's the schedule"

### research-analyst

| Input | Output |
|-------|--------|
| Research question, topic | Multi-source research report, analysis, recommendations |
| Comparison criteria, domains | Competitive analysis, market research, technology evaluation |

**Routing signals**: "research this", "compare options", "what's the landscape", "analyze the market"

### proposal-writer

| Input | Output |
|-------|--------|
| Project scope, client context | Proposal document, ROI table, three-tier pricing |
| Architecture doc, timeline, budget | PDF-ready proposal with executive summary |

**Routing signals**: "write a proposal", "pricing for", "ROI analysis", "client-facing document"

### full-stack-builder

| Input | Output |
|-------|--------|
| Architecture doc, task spec | Working code, tests, documentation |
| Feature requirements, API contracts | Implementation with CI/CD integration |

**Routing signals**: "build this", "implement the feature", "write the code", "create the API"

### content-strategist

| Input | Output |
|-------|--------|
| Topic, source material, audience | Blog posts, LinkedIn posts, slide decks, PDF reports |
| Research output, channel requirements | Multi-channel content strategy and production |

**Routing signals**: "write content about", "create a blog post", "LinkedIn post for", "content strategy"

### release-captain

| Input | Output |
|-------|--------|
| Code branch, release requirements | PR, changelog, release notes, deployed release |
| Version bump, deployment target | Tag, GitHub release, deployment verification |

**Routing signals**: "ship this", "create a PR", "release the code", "deploy to production"

### codebase-auditor

| Input | Output |
|-------|--------|
| Repository path, audit scope | Quality report, issue list, severity ratings |
| Code changes, standards reference | Pass/fail assessment, remediation recommendations |

**Routing signals**: "audit the code", "review the codebase", "quality check", "is this ready to ship"

### idea-scout

| Input | Output |
|-------|--------|
| Business idea description | Viability assessment, market analysis, GO/NO-GO recommendation |
| Product concept, target market | Competitive landscape, risk factors, opportunity sizing |

**Routing signals**: "validate this idea", "is this viable", "should we build this", "market opportunity"

### media-producer

| Input | Output |
|-------|--------|
| Concept to visualize, style prefs | PNG, SVG, HTML, MP4, or slide deck |
| Format requirements, brand params | Visual asset with format recommendation |

**Routing signals**: "visualize this", "create a diagram", "make a video", "design slides for"

---

## Cross-Agent Dependencies

| Upstream Agent | Downstream Agent | What Passes |
|---------------|-----------------|-------------|
| project-architect | project-planner | Architecture document |
| project-architect | full-stack-builder | Architecture document, API contracts |
| project-architect | proposal-writer | Architecture document |
| project-planner | full-stack-builder | Task breakdown, priorities |
| project-planner | proposal-writer | Timeline, milestones |
| research-analyst | content-strategist | Research report, data points |
| research-analyst | proposal-writer | Market data, competitive analysis |
| research-analyst | idea-scout | Market research |
| idea-scout | project-architect | GO decision, validated requirements |
| codebase-auditor | release-captain | PASS decision |
| full-stack-builder | codebase-auditor | Code changes |
| content-strategist | media-producer | Visual asset requests |
