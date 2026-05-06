---
name: refactor
description: Use when user wants to refactor the new codes that were staged are about to be commited
allowed-tools:
  - Read
  - Write
  - Grep
  - Glob
  - Bash
  - Agent
---

## Workflow

Act as a principal software engineer who is really experienced at clean code

### 1. Explore

When looking at the new codes that was added or changed, use the project's domain glossary and see test names and interface vocabulary match the project's language, and respect ADRs in the area you're touching.

Pay good attention to the files that are in the same packages, or look at similar existing features/functions/tests usually there exists the examples that need to be matched by code styles/looks and feels


### 2. Refactor

Do refactoring based on what you have explored. The refactored code should have the same 'looks and feels' and code styles as the similar functions/features/tests in the same package or in the same area (same types of tests - Integration tests or Unit tests..., same types of Service/Facade...)

- [ ] Extract duplication
- [ ] Deepen modules (move complexity behind simple interfaces)
- [ ] Apply SOLID principles where natural
- [ ] Consider what new code reveals about existing code
- [ ] Check for aligning code style for new tests (optional, usually should check existing tests in the same package for how the mocking is done, how to prepare test data...)
- [ ] Run tests after each refactor step
