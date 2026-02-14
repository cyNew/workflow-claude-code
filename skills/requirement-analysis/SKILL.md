---
name: requirement-analysis
description: "Analyzes and clarifies development requirements by identifying ambiguities, missing details, and implicit assumptions. Activated when discussing new tasks, user stories, bug reports, or feature requests."
---

# Requirement Analysis Skill

When analyzing a requirement, systematically check for completeness before any implementation begins.

## Clarification Checklist

For every incoming requirement, verify the following. If items are missing or unclear, ask up to **3-4** focused questions in a single round to resolve them efficiently. Group related questions together and only ask about things that would actually change your implementation approach.

### Functional
- **What** exactly should happen? (expected behavior)
- **Who** triggers it? (user action, system event, API call, cron job)
- **Where** in the application does this occur? (which page, service, endpoint)
- **What are the edge cases?** (empty input, concurrent access, large payloads, permissions)

### Non-functional
- **Performance**: Are there latency or throughput requirements?
- **Security**: Does this involve user data, authentication, or authorization?
- **Compatibility**: Does this need to work with specific browsers, devices, or API versions?

### Scope boundaries
- **What is explicitly OUT of scope?** (avoid scope creep)
- **Are there related changes the user might expect but hasn't mentioned?**

## How to Apply

- Do NOT run through this entire checklist out loud. Use it as an internal guide.
- Only surface questions that are genuinely blocking — where the answer would change your implementation approach.
- If the requirement is clear and complete, confirm your understanding in one sentence and proceed.
- For vague requirements like "fix the login issue" or "improve performance", always ask at least one clarifying question before acting.
