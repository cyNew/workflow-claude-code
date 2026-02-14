---
name: impact-assessment
description: "Assesses the scope and impact of a proposed code change by scanning the codebase for affected files, modules, APIs, and dependencies. Automatically activated when discussing requirements, planning changes, or evaluating task complexity."
---

# Impact Assessment Skill

When evaluating the impact of a proposed change, follow this systematic approach.

## Discovery Process

1. **Identify keywords**: Extract key entities from the requirement — function names, class names, API endpoints, table names, module names, config keys.
2. **Search broadly**: Use Grep and Glob with each keyword to find all references across the codebase. Do not limit searches to obvious directories.
3. **Trace dependencies**: For each affected file, check its imports and exports. Identify upstream callers and downstream dependencies.
4. **Check data layer**: Look for database migrations, schema files, ORM models, or SQL queries related to the change.
5. **Check API surface**: Look for route definitions, API handlers, OpenAPI specs, or client SDK code that may be affected.
6. **Check configuration**: Look for environment variables, config files, feature flags, or deployment manifests that may need updates.

## Sizing Criteria

Apply these rules to determine task size:

| Criteria             | Trivial | Small | Large    |
|----------------------|---------|-------|----------|
| Files changed        | ≤2      | ≤5    | >5       |
| Modules touched      | 1       | 1     | >1       |
| DB schema changes    | No      | No    | Yes      |
| API contract changes | No      | No    | Yes      |
| New dependencies     | No      | No    | Yes      |
| Breaking changes     | None    | None  | Possible |
| Scope obvious?       | Yes     | —     | —        |

If ALL Trivial criteria are met and the scope is immediately obvious from the requirement, classify as **Trivial**. Trivial tasks skip impact assessment and task records entirely.

If ANY "Large" criterion is met, the task is **Large**.

If there is no existing codebase (greenfield), classify as **New Project**.

## Output

Always produce a structured impact summary. See the `/task` command for the exact format.

## When Uncertain

If the codebase is unfamiliar or the search results are ambiguous:
- State what you found and what you couldn't determine.
- Recommend the user verify specific areas manually.
- Default to the larger size classification — it is safer to overestimate than underestimate.
