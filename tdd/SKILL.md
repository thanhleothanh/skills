---
name: tdd
description: Test-driven development with red-green-refactor loop. Use when user wants to build features or fix bugs using TDD, mentions "red-green-refactor", wants integration tests, or asks for test-first development.
allowed-tools:
  - Read
  - Write
  - Grep
  - Glob
  - Bash
  - Agent
---

# Test-Driven Development

Act as a principal software engineer who understands very deeply Test-driven Development

## Philosophy

**Core principle**: Tests should verify behavior through public interfaces, not implementation details. Code can change entirely; tests shouldn't.

**Good tests** are integration-style: they exercise real code paths through public APIs. They describe _what_ the system does, not _how_ it does it. A good test reads like a specification - "user can checkout with valid cart" tells you exactly what capability exists. These tests survive refactors because they don't care about internal structure.

**Bad tests** are coupled to implementation. They mock internal collaborators, test private methods, or verify through external means (like querying a database directly instead of using the interface). The warning sign: your test breaks when you refactor, but behavior hasn't changed. If you rename an internal function and tests fail, those tests were testing implementation, not behavior.


## Anti-Pattern: Horizontal Slices

**DO NOT write all tests first, then all implementation.** This is "horizontal slicing" - treating RED as "write all tests" and GREEN as "write all code."

This produces **crap tests**:

- Tests written in bulk test _imagined_ behavior, not _actual_ behavior
- You end up testing the _shape_ of things (data structures, function signatures) rather than user-facing behavior
- Tests become insensitive to real changes - they pass when behavior breaks, fail when behavior is fine
- You outrun your headlights, committing to test structure before understanding the implementation

**Correct approach**: Vertical slices via tracer bullets. One test → one implementation → repeat. Each test responds to what you learned from the previous cycle. Because you just wrote the code, you know exactly what behavior matters and how to verify it.

```
WRONG (horizontal):
  RED:   test1, test2, test3, test4, test5
  GREEN: impl1, impl2, impl3, impl4, impl5

RIGHT (vertical):
  RED→GREEN: test1→impl1
  RED→GREEN: test2→impl2
  RED→GREEN: test3→impl3
  ...
```

## Workflow

### 1. Planning

When exploring the codebase, use the project's domain glossary so that type of test, test class name, test names and interface vocabulary match the project's language and styles, and respect ADRs in the area you're touching.

Users could have already written the interface (or not) needed for the features, you could take on from that.

Before writing any code:

- [ ] Confirm with user what interface changes are needed
- [ ] Confirm with user which behaviors to test (prioritize)
- [ ] Identify opportunities for deep modules (small interface, deep implementation)
- [ ] Design interfaces for with easy to test in mind
- [ ] List the behaviors to test (not implementation steps), including happy paths, and edge cases
- [ ] Get user approval on the plan

For Unit tests: Take care of all the happy paths and edge cases.
For Integration tests: Take care of the important and realistic possible cases

- Here are some edge cases examples, you should be determining edge cases based on the context of the business logic you are working on also, not just programmatic edge cases:

1. Empty Sets/Nulls: Empty strings, empty lists, or null inputs.
2. Numeric Extremes: negative numbers, or integers at the limits of what a language can store (e.g., \(2^{31}-1\) for a 32-bit signed integer).
3. Boundary Conditions: Testing the exact limit, just below, and just above, such as testing \(1\) and \(100\) if a field only accepts \(1-100\).
4. Collections: An array with zero, one, or thousands of elements.
5. Dates: February 29th (leap year), December 31st, or dates spanning across time zones.
6. The intersection of multiple valid cases.
7. The intersection of multiple invalid cases.
8. The intersection of multiple valid cases and multiple invalid cases.
...


### 2. Tracer Bullet

Write ONE test that confirms ONE thing about the system:

```
RED:   Write test for first behavior → test fails
GREEN: Write minimal code to pass → test passes
```

This is your tracer bullet - proves the path works end-to-end.

### 3. Incremental Loop

For each remaining behavior:

```
RED:   Write next test → fails
GREEN: Minimal code to pass → passes
```

For integration tests, the feature code might already have been partially implemented, if so check for integration tests cases, for each case:

```
RED:   Write new test for integration test behavior → test might fail
GREEN: Change code to pass → test passes
```

Rules:

- One test at a time
- Only enough code to pass current test
- Don't anticipate future tests
- Keep tests focused on observable behavior
- New tests should have the same _type_ as the other tests in the same package (unit tests, integration tests...)

### 4. Refactor

**Never refactor while RED.** Get to GREEN first.

## Checklist Per Cycle

```
[ ] Test describes behavior, not implementation
[ ] Test uses public interface only
[ ] Test would survive internal refactor
[ ] Code is minimal for this test
[ ] No speculative features added
```
