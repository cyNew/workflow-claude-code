---
description: "Finalize and ship changes: run tests, commit with a proper message, and optionally push. Use when changes are reviewed and ready to go."
argument-hint: "[optional: commit message override]"
---

# Ship

You are preparing changes for delivery. Follow this sequence strictly.

## Step 1: Pre-flight Checks

1. Run the full test suite. If any test fails, STOP and report the failure. Do not proceed.
2. Run the linter/formatter if configured (check package.json scripts, Makefile, or similar). Fix any issues.
3. Check `git status` to confirm what will be committed. Report the list of changed files.

## Step 2: Commit

1. If the user provided a commit message, use it.
2. Otherwise, generate a commit message following the project's convention. If no convention exists, use conventional commits:
   - `feat: <description>` for new features
   - `fix: <description>` for bug fixes
   - `refactor: <description>` for refactors
   - `docs: <description>` for documentation
   - `test: <description>` for test additions
   - `chore: <description>` for maintenance
3. If a task record exists in `docs/plans/` for this change, reference it in the commit body (e.g., `Task-Record: docs/plans/2026-02-14-fix-login-timeout.md`).
4. If the changes span multiple concerns, suggest splitting into multiple commits and ask the user.
5. Stage and commit the changes. **Include the task record file in the commit.**

## Step 3: Finalize Task Record

If a task record exists for this change:
1. Set `**Status**` to `done`.
2. Ensure "Changes Made" is complete with all modified files.
3. Add any final notes about decisions or trade-offs to the "Notes" section.

## Step 4: Confirm Next Action

Ask the user:
- "Changes committed. Want me to push to the current branch, create a new branch, or stop here?"

Do NOT push automatically. Always wait for confirmation.
