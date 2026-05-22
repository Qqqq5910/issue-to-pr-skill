# Example: Refactor Task

## Input Issue

```text
Refactor: Split the large UserService file into smaller modules.
The file is hard to maintain and mixes profile, billing, and notification logic.
Do not change behavior.
```

## Skill Output

## Issue Summary

The current `UserService` is too large and mixes profile, billing, and notification responsibilities. The requested change is a behavior-preserving refactor that splits the service into smaller modules.

## Task Type

Refactor

## Requirements and Constraints

### Requirements
- Split profile, billing, and notification logic into clearer modules.
- Preserve all existing behavior.
- Keep public interfaces stable unless the issue explicitly allows otherwise.
- Ensure existing tests continue to pass.

### Constraints
- This should be a refactor, not a behavior change.
- Broad refactors are risky, so the first PR should stay reviewable.

### Non-goals
- Changing business logic.
- Rewriting the service from scratch.
- Introducing a new framework or architecture pattern without need.

### Open Questions
- Which public methods are consumed outside the service?
- Are there existing tests covering the current behavior?

## Likely Affected Areas

- `UserService` or equivalent service module
- Profile-related service logic
- Billing-related service logic
- Notification-related service logic
- Service tests and mocks
- Dependency injection or module exports

## Implementation Plan

1. Inspect `UserService` public methods and external callers.
2. Identify clear responsibility groups: profile, billing, and notification.
3. Ensure current behavior is covered by tests before moving logic.
4. Extract one responsibility at a time into smaller modules.
5. Preserve the existing public API through a facade or compatibility exports.
6. Run the full relevant test suite after each extraction.
7. Update internal documentation or comments if module boundaries change.

## Risk Checklist

- [ ] Public API remains stable.
- [ ] Existing mocks and tests are updated without weakening coverage.
- [ ] No behavior changes are mixed into the refactor.
- [ ] Circular dependencies are not introduced.
- [ ] Error handling remains unchanged.

## Test Plan

### Automated Tests
- Run existing `UserService` tests.
- Add coverage for untested public methods before moving logic.
- Run integration tests covering profile, billing, and notifications.

### Manual Verification
- Verify key user profile flows.
- Verify billing-related user actions.
- Verify notification-related user actions.

### Regression Checks
- Compare behavior before and after refactor where possible.
- Confirm imports and dependency injection still resolve correctly.

## Pull Request Description

### Summary
Splits the large user service into smaller responsibility-focused modules without changing behavior.

### Changes
- Extracted profile-related logic.
- Extracted billing-related logic.
- Extracted notification-related logic.
- Preserved existing service API for callers.
- Updated tests and imports.

### Testing
- Ran existing user service tests.
- Ran integration tests for profile, billing, and notification flows.
- Verified no intended behavior changes.

### Risk
Medium to high. This is a broad refactor, so reviewers should focus on API stability, import changes, and test coverage.

### Related Issue
Closes #

## Reviewer Checklist

- [ ] The refactor is behavior-preserving.
- [ ] Public interfaces remain stable.
- [ ] Responsibility boundaries are clearer.
- [ ] Test coverage was not weakened.
- [ ] No unrelated cleanup or feature work was mixed in.
