---
name: task-decomposition
description: "Breaks down large tasks or projects into ordered, independently testable sub-tasks. Activated when planning features, designing architecture, or working on multi-step implementation."
---

# Task Decomposition Skill

When a task is classified as **Large** or **New Project**, decompose it into manageable sub-tasks before implementation.

## Decomposition Principles

1. **Each sub-task should be independently testable.** After completing a sub-task, you should be able to verify it works without completing subsequent sub-tasks.
2. **Order sub-tasks by dependency.** If sub-task B depends on sub-task A, A comes first.
3. **Keep sub-tasks small.** Each sub-task should touch ≤5 files and be completable in a single focused session. If a sub-task feels too large, split it further.
4. **Start with the data layer.** If the task involves data model changes, do those first — everything else depends on them.
5. **End with integration.** Wire things together and do cross-cutting concerns (error handling, logging, permissions) last.

## Recommended Ordering Pattern

For typical feature work:

1. Data model / schema changes (if any)
2. Core business logic (models, services, utilities)
3. API layer (routes, controllers, serializers)
4. UI components (if applicable)
5. Integration and wiring
6. Tests for new code paths
7. Documentation updates (if needed)

Skip any steps that don't apply. Do not force this order if the task naturally flows differently.

## Plan Format

Present the decomposed plan as:

```
### Execution Plan
1. [Sub-task title] — [1-sentence description of what changes and why]
2. [Sub-task title] — [1-sentence description]
...

**Dependencies**: [note any sub-tasks that must complete before others]
**Estimated total files**: [rough count]
**Risk areas**: [anything that might need extra attention or user input]
```

## Checkpoint Protocol

After completing each sub-task:
1. Briefly state what was done.
2. Confirm tests pass.
3. Update the task record (`docs/plans/YYYY-MM-DD-*.md`) with completed sub-task details in the "Changes Made" section.
4. Ask: "Proceeding to [next sub-task], or do you want to adjust the plan?"

If the plan changes during execution, update the "Execution Plan" section in the task record to reflect the revised plan. Note the reason for the change in the "Notes" section.

This gives the user a chance to realign requirements at every step, which is especially important for large tasks where requirements may evolve. The task record ensures that the final document accurately reflects what was actually done, not just what was originally planned.
