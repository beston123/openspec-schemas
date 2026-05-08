# OpenSpec Schemas

[English](README.md) | [简体中文](README_zh.md)

Reusable schema definitions for **OpenSpec** — a spec-driven development framework that turns feature ideas into structured, verifiable deliverables through phased workflows.

## What's Here

| Schema | Description |
|--------|-------------|
| **super-spec-driven** | Full lifecycle workflow: brainstorm → proposal → specs/design → plan → tasks → apply. Integrates with **Superpowers** skills for AI-assisted execution. |

More schemas coming soon.

## The super-spec-driven Workflow

```
brainstorm → proposal → specs / design → plan → tasks → apply → verify → archive
   (🤖)        (🤖)      (🤖)   (🤖)     (🤖)    (🤖)    (🤖)      (🤖)
```

| Phase | Artifact | What Happens |
|-------|----------|-------------|
| `brainstorm` | `brainstorm.md` | Collaborative design exploration using Superpowers brainstorming |
| `proposal` | `proposal.md` | Why this change is needed, what capabilities are affected |
| `specs` | `specs/**/*.md` | Testable requirements with WHEN/THEN scenarios |
| `design` | `design.md` | Technical decisions, architecture, risks |
| `plan` | `plan.md` | Micro-task breakdown (2–5 min steps, TDD style) |
| `tasks` | `tasks.md` | Checkbox checklist extracted from the plan |
| `apply` | — | Execute tasks via subagent-driven or inline execution |
| `verify` | — | Check completeness, correctness, and coherence |
| `archive` | — | Archive the completed change |

Each phase produces a concrete artifact that the next phase builds on — no loose threads.

### Quick Example

```
1. /opsx:new my-feature --schema super-spec-driven
2. /opsx:continue   → brainstorm (superpowers:brainstorming)
3. /opsx:continue   → proposal
4. /opsx:continue   → specs + design (produced in parallel)
5. /opsx:continue   → plan (superpowers:writing-plans)
6. /opsx:continue   → tasks
7. /opsx:apply      → implementation (subagent-driven or inline)
8. /opsx:verify     → completeness check
9. /opsx:archive    → archive the change
```

## Getting Started

### Prerequisites

- **OpenSpec** installed and configured
- **Superpowers** skills installed (for `super-spec-driven` schema)

### Install

Copy the schema folder into your project's OpenSpec directory:

```bash
git clone https://github.com/beston123/openspec-schemas.git
cp -r openspec-schemas/schemas your-project/openspec/
```

Your project will look like this:

```
your-project/
├── openspec/
│   ├── config.yaml        # Project config
│   ├── schemas/           # Custom schemas live here
│   │   └── super-spec-driven/
│   │       ├── schema.yaml
│   │       └── templates/
│   └── changes/           # Your changes
└── src/
```

#### Schema Resolution Order

When OpenSpec needs a schema, it checks in this order:

1. **CLI flag** — `--schema <name>`
2. **Change metadata** — `.openspec.yaml` in the change folder
3. **Project config** — `openspec/config.yaml`
4. **Default** — `spec-driven`

#### Configure As Default

Edit `openspec/config.yaml` to set the schema and per-artifact rules:

```yaml
schema: super-spec-driven

context: |
  Tech stack: TypeScript, React, Node.js
  We use conventional commits
  Domain: e-commerce platform

rules:
  proposal:
    - May include non-functional requirements (NFRs)
    - Include SLO targets (latency, concurrency, quality) when relevant
    - Include Capabilities section mapping to spec folder names
  specs:
    - Use Given/When/Then (Gherkin) format for all Scenarios
    - Every Requirement must include Priority (P0/P1/P2) and Rationale
    - Prefer existing specs over creating new ones.
  design:
    - Include designs for performance, availability, security, consistency, etc. (if applicable)
    - Include architecture diagrams (Mermaid or ASCII), sequence diagrams for complex flows
    - Avoid code implementation
```

## Contributing

Contributions are welcome! To add a new schema:

1. Create a folder under `schemas/<schema-name>/`
2. Add a `schema.yaml` defining the workflow phases
3. Add templates under `schemas/<schema-name>/templates/`
4. Submit a pull request

Please open an issue first to discuss significant changes.

## Acknowledgements

Inspired by [JiangWay/openspec-schemas](https://github.com/JiangWay/openspec-schemas).

## License

[MIT](LICENSE)
