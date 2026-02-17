# Agent Teams

Launch a team of AI agents to implement features with built-in code review gates.

## Prerequisites

> **Agent teams are experimental and disabled by default.** You need to enable them before using this plugin.

Add `CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS` to your `settings.json` or environment:

```json
// ~/.claude/settings.json
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
```

Or set the environment variable:

```bash
export CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1
```

Restart Claude Code after enabling.

## Installation

```bash
/plugin marketplace add izmailovilya/ilia-izmailov-plugins
/plugin install agent-teams@ilia-izmailov-plugins
```

## Usage

```
/team-feature <description or path/to/plan.md> [--coders=N]
/conventions [path/to/project]
```

**Examples:**
```
/team-feature "Add user settings page with profile editing"
/team-feature docs/plan.md --coders=2
/conventions
```

## How It Works

### /team-feature

A Team Lead agent orchestrates the full implementation pipeline:

```
Phase 1: Discovery & Planning
  Researchers explore your codebase in parallel
  Lead classifies complexity (SIMPLE / MEDIUM / COMPLEX)
  Tech Lead validates the plan
  Risk analysis catches problems BEFORE coding

Phase 2: Execution
  Coders implement tasks with gold standard examples
  3 specialized reviewers check every change:
    - Security Reviewer (injection, XSS, auth bypasses)
    - Logic Reviewer (race conditions, edge cases)
    - Quality Reviewer (DRY, naming, conventions)
  Tech Lead gives final architectural approval

Phase 3: Completion
  Integration verification (build + tests)
  .conventions/ updated with new patterns
  Summary report
```

### /conventions

Analyzes your codebase and creates/updates `.conventions/` directory with:
- `gold-standards/` — exemplary code snippets (20-30 lines each)
- `anti-patterns/` — what NOT to do
- `checks/` — naming rules, import patterns

These conventions are used by `/team-feature` to keep code consistent.

## Team Roles

| Role | Lifetime | Purpose |
|------|----------|---------|
| **Lead** | Whole session | Orchestrates everything |
| **Codebase Researcher** | One-shot | Explores project structure |
| **Reference Researcher** | One-shot | Finds canonical code examples |
| **Tech Lead** | Permanent | Validates plan, reviews architecture |
| **Coder** | Per task | Implements with gold standard patterns |
| **Security Reviewer** | Permanent | Injection, XSS, auth, secrets |
| **Logic Reviewer** | Permanent | Race conditions, edge cases, null handling |
| **Quality Reviewer** | Permanent | DRY, naming, conventions compliance |
| **Unified Reviewer** | Permanent | All-in-one for SIMPLE tasks |
| **Risk Tester** | One-shot | Verifies risks before implementation |

## Complexity Levels

| Level | Team Size | Review | Risk Analysis |
|-------|-----------|--------|---------------|
| SIMPLE | 3 agents | Unified reviewer | Skipped |
| MEDIUM | 4-6 agents | 3 specialized reviewers | Yes |
| COMPLEX | 5-8+ agents | 3 reviewers + deep analysis | Full |

## Structure

```
agent-teams/
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   ├── team-feature.md
│   └── conventions.md
├── agents/
│   ├── codebase-researcher.md
│   ├── reference-researcher.md
│   ├── tech-lead.md
│   ├── coder.md
│   ├── security-reviewer.md
│   ├── logic-reviewer.md
│   ├── quality-reviewer.md
│   ├── unified-reviewer.md
│   └── risk-tester.md
├── references/
│   ├── gold-standard-template.md
│   └── risk-testing-example.md
└── README.md
```

## License

MIT
