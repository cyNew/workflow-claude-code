---
description: "Execute a focused implementation step. Use when you already know exactly what to change and just need to implement, test, and review."
argument-hint: "<what to implement>"
---

# Implement

You are executing a single, well-defined change by delegating to the `coder` agent.

## Step 1: Prepare Context

Gather the information the coder needs:
- Search the codebase for the relevant files and conventions (or delegate to the `scout` agent if the project is unfamiliar).
- Identify: the test command, code style, and any constraints.

## Step 2: Delegate

Send the task to the `coder` agent with:
- A clear description of what to change
- The project context (language, framework, test command, code conventions)
- Any constraints (files not to touch, patterns to follow)

## Step 3: Review Result

When the coder returns:
- If **success**: review the summary, confirm the changes look correct.
- If **partial** or **blocked**: address the issue — provide missing info, clarify scope, or re-delegate.

## Step 4: Report

Present the coder's implementation summary to the user. List all modified files and what was done.
