# workflow

A Claude Code plugin that provides a unified, structured development workflow — from receiving a requirement to shipping code.

## Overview

Instead of separate commands for small fixes, large features, and new projects, this plugin provides a single `/task` entry point that **automatically assesses impact and routes to the appropriate pipeline**.


## Installation

### From marketplace (GitHub)

```bash
# Add marketplace
/plugin marketplace add cyNew/workflow-claude-code

# Install the plugin
/plugin install workflow@workflow-claude-code
```

### Local development / direct testing

```bash
# Install after adding marketplace
/plugin marketplace add ./path/to/workflow-claude-code
/plugin install workflow@workflow-claude-code

# or start with
claude --plugin-dir ./plugins/workflow
```

## Components

### Commands

| Command | Description |
|---------|-------------|
| `/task <description>` | **Main entry point.** Analyzes requirement → assesses impact → determines size → executes the appropriate pipeline. |
| `/implement <description>` | Focused implementation step: locate → code → test → self-review. Use when scope is already clear. |
| `/review [files or ref]` | Independent code review of recent changes. Checks correctness, design, security, and performance. |
| `/ship [commit message]` | Pre-flight checks → commit → confirm push. Ensures tests and linting pass before committing. |

### Skills (auto-activated)

| Skill | Triggers on |
|-------|-------------|
| `impact-assessment` | Discussing requirements, planning changes, evaluating complexity |
| `requirement-analysis` | New tasks, user stories, bug reports, feature requests |
| `task-decomposition` | Planning features, designing architecture, multi-step work |

### Agents

| Agent | Model | Purpose |
|-------|-------|---------|
| `scout` | Sonnet | Research and reconnaissance — scans codebase, searches the web, fetches docs, uses MCP tools |
| `coder` | Sonnet | Implementation — executes focused coding tasks, runs tests, returns structured change summary |
| `code-reviewer` | Sonnet | Independent code review from a separate context |

### MCP Integration (optional)

Copy `.mcp.json.example` to `.mcp.json` and customize. The `scout` agent can leverage MCP tools like Context7 for version-specific library documentation. Without MCP, `scout` falls back to web search and WebFetch.

### Hooks

| Event | Matcher | Action |
|-------|---------|--------|
| PreToolUse | `git commit` | Runs test suite before allowing commit |
| PreToolUse | `git push --force`, `git reset --hard`, `git clean -fd` | Blocks destructive git operations |
| PostToolUse | `Edit\|Write\|MultiEdit` | Auto-formats changed files (Prettier for JS/TS, Black/Ruff for Python) |

## Workflow Overview

The plugin components work together in a pipeline:

### Full workflow via `/task` (recommended entry point)

```
User: /task <requirement>
  │
  ├─ Phase 1: Understand requirement    ← skill: requirement-analysis
  │
  ├─ Phase 1.5: Quick Triage
  │   ├─ Trivial → implement directly → verify → done (no task record)
  │   └─ Not trivial → continue ↓
  │
  ├─ Phase 2: Impact Assessment         ← skill: impact-assessment, agent: scout
  │
  ├─ Phase 2.5: Create task record      → docs/plans/YYYY-MM-DD-slug.md
  │
  └─ Phase 3: Route by Size
      ├─ Small  → agent: coder → verify → update record → report
      ├─ Large  → skill: task-decomposition → agent: coder (×N) → integration review
      └─ New    → architecture → milestones → agent: coder (×N) → integration review
```

### Standalone commands

| Command | Use when | Components used |
|---------|----------|-----------------|
| `/task` | New task, unknown scope | scout + coder + skills |
| `/implement` | Know exactly what to change | coder only |
| `/review` | Changes done, want a second look | code-reviewer |
| `/ship` | Ready to commit and push | tests + git |

### Task Records

For non-trivial tasks, `/task` creates a markdown file in `docs/plans/` that preserves:
- Original requirement (verbatim)
- Impact assessment results
- Execution plan (updated if plan changes mid-flight)
- All files changed with rationale
- Decisions, trade-offs, and notes

This gives your team a paper trail from requirement to commit. When reviewing changes later, the task record links the "what was changed" back to the "why it was changed".

## Customization

- **Sizing thresholds**: Edit `skills/impact-assessment/SKILL.md` to adjust what counts as small vs. large for your team.
- **Review standards**: Edit `agents/code-reviewer.md` to add project-specific review criteria.
- **Pre-commit hooks**: Edit `hooks/hooks.json` to customize which checks run before commits.
- **Formatting**: The PostToolUse hook auto-detects Prettier and Black/Ruff. Add your own formatters as needed.

## License

MIT
