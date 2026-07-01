---
name: testing
description: Validate code changes through appropriate testing, prevent regressions, and ensure changes are safe before completion.
---

# Testing

Testing verifies that changes behave as intended and do not introduce regressions.

Testing should provide confidence, not simply increase coverage.

## Core Principles

- Follow existing project testing conventions.
- Test observable behavior rather than implementation details.
- Prefer simple, deterministic tests.
- Keep tests readable and maintainable.
- Add the minimum number of tests needed to establish confidence.
- Coverage is a signal, not a goal.

## Understand the Change

Before writing or running tests, identify:

- What changed?
- What behavior is expected?
- What could accidentally break?
- Which existing tests already provide coverage?

Choose tests based on risk instead of running the full suite by default.

## Testing Strategy

Prefer the following order of confidence:

1. Existing tests already verify the change.
2. Add focused unit tests.
3. Add integration tests if component interactions changed.
4. Use end-to-end tests only for critical user workflows.
5. Use manual verification only when automation is impractical.

Do not introduce expensive or slow tests when simpler tests provide equivalent confidence.

## Test Pyramid

Prefer:

- many unit tests
- fewer integration tests
- very few end-to-end tests

Always choose the lowest practical level that provides sufficient confidence.

## Test Scope

### Unit Tests

Use unit tests to verify:

- business logic
- algorithms
- validation
- edge cases
- error handling

Unit tests should be fast and isolated from external dependencies.

### Integration Tests

Use integration tests when changes affect interactions between components, including:

- APIs
- databases
- message queues
- caches
- file systems
- external services

Verify both outputs and observable side effects.

### End-to-End Tests

Reserve end-to-end tests for critical user workflows.

Do not rely on E2E tests to validate internal logic.

## Feature Development

For new functionality, verify:

- expected behavior
- invalid input
- boundary conditions
- error handling
- state changes
- returned values
- observable side effects

## Bug Fixes

Whenever practical, every bug fix should include a regression test.

A good regression test:

- reproduces the original issue
- fails before the fix
- passes after the fix
- prevents future regressions

## Refactoring

When refactoring:

- preserve existing behavior
- ensure existing tests continue to pass
- update tests only if external behavior intentionally changes

Avoid rewriting tests solely due to implementation changes.

## Test Design

Good tests are:

- independent
- deterministic
- focused
- readable
- maintainable

Prefer reuse of:

- existing fixtures
- existing helpers
- existing assertion styles
- existing test structure

Avoid:

- testing private implementation details
- unnecessary mocking
- duplicated assertions
- fragile timing assumptions
- random or flaky behavior
- introducing new testing frameworks without strong justification

## When Tests Are Not Necessary

Additional tests may not be needed when:

- only comments are changed
- formatting changes only
- documentation changes only
- configuration changes with no behavioral impact
- existing tests already fully cover the change

Do not create redundant tests that do not increase confidence.

## Mocking

- Mock only external dependencies
- Do not mock the code being tested
- Prefer real implementations when practical
- Use mocking only to isolate external systems or reduce flakiness

## Snapshot Testing

- Use snapshot tests sparingly
- Prefer explicit assertions for important behavior
- Review snapshot updates carefully instead of accepting blindly

## AI Guidance

Before creating new tests:

- Inspect existing test files first
- Match project naming conventions
- Match assertion style
- Reuse existing fixtures
- Extend existing test files instead of creating new ones unnecessarily

Never claim tests passed unless they were actually executed.

If tests cannot be executed:

- clearly state what was not verified
- distinguish assumptions from validated behavior
- describe remaining risks

Avoid creating duplicate or redundant test files (e.g. multiple versions of the same test suite).

## Failed Tests

If tests fail:

- determine whether failure is related to the change
- do not ignore failures
- do not blindly update snapshots
- investigate root cause before proceeding
- explicitly resolve or document unresolved failures

## Edge Cases

Consider testing where relevant:

- empty input
- null values
- invalid values
- boundary values
- duplicate input
- large input
- concurrency issues
- timeout behavior
- permission failures
- resource exhaustion

Only include cases relevant to the change.

## Performance and Reliability

When applicable, verify:

- no obvious performance regressions
- no unnecessary memory growth
- proper resource cleanup
- retry behavior
- timeout handling

## Before Completion

Before considering work complete:

- identify impacted tests
- run the minimal relevant test suite
- verify new tests pass
- verify affected existing tests pass
- investigate unexpected failures
- ensure regression coverage exists where needed
- confirm no obvious behavioral regressions remain

If testing is incomplete:

- explain what was not verified
- explain why
- describe remaining risks clearly

## Completion Checklist

Before finishing, confirm:

- implementation behaves as intended
- important execution paths are covered
- relevant edge cases are considered
- regressions are unlikely
- test suite remains clean
- confidence matches the risk level of the change
