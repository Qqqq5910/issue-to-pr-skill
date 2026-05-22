# Example: Performance Regression

## Input Issue

```text
Performance regression: opening the dashboard is much slower after the analytics widget launch.
It used to load in about 1 second and now takes 4-5 seconds on normal accounts.
Large enterprise accounts are worse.
```

## Skill Output

## Issue Summary

Dashboard load time regressed after the analytics widget launch. Normal accounts now take about 4-5 seconds to load instead of roughly 1 second, and large enterprise accounts appear more affected. The expected behavior is that the dashboard remains responsive while analytics data loads efficiently.

## Task Type

Performance

## Requirements and Constraints

### Requirements
- Confirm the regression and identify whether the analytics widget is the cause.
- Measure the dashboard load path before changing behavior.
- Reduce dashboard load time without removing required analytics functionality.
- Consider large-account data volume as a likely stress case.

### Constraints
- The baseline and current timings are approximate.
- The affected accounts, environment, and metrics source are not specified.
- The fix may involve frontend rendering, API calls, database queries, caching, or lazy loading.

### Non-goals
- Removing the analytics widget.
- Rebuilding the dashboard architecture without evidence.
- Optimizing unrelated dashboard sections.

### Open Questions
- Which metric matters most: first render, interactive time, API latency, or full widget completion?
- Does the slowdown happen on every dashboard visit or only cold loads?
- Are large enterprise accounts slow because of query volume, payload size, or rendering cost?

## Likely Affected Areas

- Dashboard page or route
- Analytics widget component
- Analytics API endpoint
- Dashboard data loading orchestration
- Database queries or aggregation jobs
- Caching and pagination behavior
- Performance monitoring or tracing setup

## Implementation Plan

1. Reproduce dashboard load behavior for normal and large accounts.
2. Add or inspect timing around page render, analytics API calls, payload size, and database query duration.
3. Compare dashboard loading with and without the analytics widget when possible.
4. Identify the narrowest bottleneck: blocking fetch, expensive query, oversized payload, synchronous render, or missing cache.
5. Apply a scoped fix such as lazy loading, request splitting, query optimization, caching, pagination, or memoized rendering.
6. Add performance-sensitive tests or instrumentation where practical.
7. Verify normal and large-account dashboard behavior and confirm existing analytics output remains correct.

## Risk Checklist

- [ ] Analytics data remains correct after optimization.
- [ ] Large accounts do not time out or load excessive payloads.
- [ ] The dashboard remains usable if analytics loading is delayed.
- [ ] Caching does not show stale or unauthorized data.
- [ ] The fix does not hide the regression by moving work to another blocking path.

## Test Plan

### Automated Tests
- Add or update tests for any changed data-loading or aggregation behavior.
- Add regression coverage for pagination, caching, or lazy-loading logic if changed.

### Manual Verification
- Compare dashboard load timing before and after the fix.
- Verify behavior for normal and large enterprise accounts.
- Confirm analytics widget data still appears correctly.

### Regression Checks
- Confirm unrelated dashboard widgets still load.
- Confirm error and loading states are visible and accessible.
- Confirm account permissions still apply to analytics data.

## Pull Request Description

### Summary
Improves dashboard load performance after the analytics widget regression while preserving analytics functionality.

### Changes
- Measured the dashboard load path and analytics widget contribution.
- Optimized the identified bottleneck in analytics loading or rendering.
- Preserved dashboard behavior for normal and large accounts.

### Testing
- Compared dashboard load timing before and after the change.
- Verified normal and large-account dashboard behavior.
- Ran affected dashboard and analytics tests.

### Risk
Medium. Performance changes can affect data correctness, caching behavior, and large-account edge cases.

### Related Issue
Closes #

## Reviewer Checklist

- [ ] The PR includes evidence of the bottleneck.
- [ ] The fix targets the measured regression rather than guessing.
- [ ] Analytics correctness and permissions are preserved.
- [ ] Large-account behavior was verified.
