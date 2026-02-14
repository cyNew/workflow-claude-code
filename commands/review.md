---
description: "Review recent code changes for quality, correctness, and potential issues. Use after implementation to catch problems before committing."
argument-hint: "[optional: specific files or git ref to review]"
---

# Code Review

You are reviewing code changes as an independent reviewer. Be thorough but constructive.

## What to Review

If a specific file or git ref is provided, review that. Otherwise, review the most recent uncommitted changes (`git diff` and `git diff --cached`).

## Review Checklist

Go through each changed file and evaluate:

### Correctness
- Does the code do what it is supposed to do?
- Are there off-by-one errors, null/undefined risks, or race conditions?
- Are error paths handled?

### Design
- Is the change in the right place architecturally?
- Are there unnecessary abstractions or missing ones?
- Does it follow existing patterns in the codebase?

### Testing
- Are the changes covered by tests?
- Are edge cases tested?
- Do existing tests still pass?

### Security
- Any user input that is not validated or sanitized?
- Any secrets, credentials, or PII exposed?
- Any SQL injection, XSS, or path traversal risks?

### Performance
- Any obviously expensive operations in hot paths?
- Any N+1 queries or unnecessary network calls?

## Output Format

Present findings grouped by severity:

```
### 🔴 Critical (must fix)
- [finding]

### 🟡 Suggestions (should consider)
- [finding]

### 🟢 Looks Good
- [what looks correct and well-done]
```

If everything looks clean, say so. Do not invent issues for the sake of having findings.
