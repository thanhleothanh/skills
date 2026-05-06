---
name: quick-task
description: Use when user wants to finish a small task when building a feature, the what-to-do should also be mentioned
allowed-tools:
  - Read
  - Write
  - Grep
  - Glob
  - Bash
  - Agent
---

## Workflow

Act as a principal software engineer

### 1. Planning

Look at the what-to-do and, look at also the context of the currently staged code, (user might already have added new codes, or changed existing codes halfway through the solutions) 

The user might also give hints of similar existing code or similar existing features that you need to look at that have the same type of business logic/code styles or ADRs that needs to be aligned

Plan what needs to be done based on what was explored

Before writing any code:

- [ ] Look at the code related to what the users tell you to do, and related to the hints
- [ ] Confirm with user what needed to be done next as small tasks
- [ ] Get user approval on the plan

### 2. Incremental Loop

For each remaining broken down small tasks: use `/tdd` and `/refactor` to finish the small tasks.