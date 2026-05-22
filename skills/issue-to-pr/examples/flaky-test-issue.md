# Example: Flaky Test Issue

## Input Issue

```text
Flaky test: checkout retry test sometimes fails in CI.
It passes locally, but fails on GitHub Actions about once every 10 runs.
The failure says the retry count was 1 instead of 2.
```

## Skill Output

## Issue Summary

The checkout retry test is intermittently failing in CI. The expected retry count is 2, but some CI runs observe 1. The issue appears timing-sensitive because it passes locally and only fails occasionally on GitHub Actions.

## Task Type

Test / bug fix

## Requirements and Constraints

### Requirements
- Reproduce or gather enough CI evidence to explain the flaky retry assertion.
- Determine whether the product code, test setup, mock timing, or CI environment is responsible.
- Stabilize the test without weakening meaningful coverage.

### Constraints
- The failure rate is intermittent.
- Local reproduction may not be reliable.
- The repository structure and test framework are not specified.

### Non-goals
- Deleting the retry coverage.
- Increasing timeouts without understanding the failure mode.
- Rewriting the checkout flow unless product behavior is proven incorrect.

### Open Questions
- Which test framework and mocking library are used?
- Does the failure happen only under parallel test execution?
- Are timers, promises, network mocks, or retry backoff involved?

## Likely Affected Areas

- Checkout retry tests
- Retry helper or checkout service
- Mocked network or payment layer
- CI test configuration
- Timer or async utility setup

## Implementation Plan

1. Inspect recent CI failures and collect the exact failing assertion and logs.
2. Review the checkout retry test for async races, fake timers, shared state, or incomplete mock cleanup.
3. Compare local and CI test settings, including parallelism, retries, and timer behavior.
4. Identify whether the retry logic is incorrect or the test observes state too early.
5. Apply the smallest fix: await the correct condition, isolate shared state, fix timer handling, or adjust the retry implementation if needed.
6. Add or update coverage so the retry count is asserted deterministically.
7. Run the affected test repeatedly and run the surrounding checkout tests.

## Risk Checklist

- [ ] The fix does not reduce meaningful retry coverage.
- [ ] The test no longer depends on real timing when fake timing is available.
- [ ] Shared mocks or global state are reset between tests.
- [ ] CI behavior is represented in the verification plan.

## Test Plan

### Automated Tests
- Run the affected checkout retry test repeatedly.
- Run the full checkout test file or package.
- Run tests with CI-like parallelism if supported.

### Manual Verification
- Review CI logs after the fix lands.
- Confirm failure messages remain useful if retry behavior regresses again.

### Regression Checks
- Confirm retry behavior still handles the intended transient failure.
- Confirm non-retry checkout failures still surface correctly.

## Pull Request Description

### Summary
Stabilizes the flaky checkout retry test by removing the race around retry count observation.

### Changes
- Inspected CI-only failure behavior for the checkout retry test.
- Updated the test or retry timing path to assert retry behavior deterministically.
- Preserved meaningful retry coverage.

### Testing
- Ran the affected retry test repeatedly.
- Ran the surrounding checkout tests.
- Verified behavior under CI-like settings where available.

### Risk
Low to medium. The main risk is weakening test coverage while removing flakiness, so reviewer attention should focus on whether the assertion still proves retry behavior.

### Related Issue
Closes #

## Reviewer Checklist

- [ ] The test is deterministic rather than simply less strict.
- [ ] Retry coverage still proves the intended behavior.
- [ ] Async timing, mocks, and cleanup are handled safely.
- [ ] CI verification is included.
