# Example: Vague Maintainer Request

## Input Issue

```text
The settings page is confusing and users keep making mistakes.
Can we clean this up?
```

## Skill Output

## Issue Summary

The settings page is causing user confusion and mistakes, but the issue does not yet identify which settings, user roles, mistakes, or workflows are affected. The expected outcome is likely a clearer settings experience, but the scope needs to be constrained before implementation.

## Task Type

Feature / UX improvement

## Requirements and Constraints

### Requirements
- Clarify which settings page workflows are confusing.
- Identify the user mistakes the change should prevent.
- Define a small, reviewable improvement rather than a broad redesign.
- Preserve existing settings behavior unless a specific change is approved.

### Constraints
- The issue is vague and does not include screenshots, analytics, support tickets, or examples.
- The repository structure and UI framework are unknown.
- UX changes may affect documentation, tests, and user expectations.

### Non-goals
- Redesigning the entire settings area without more evidence.
- Renaming or moving settings that users rely on without migration or communication.
- Changing backend settings semantics.

### Open Questions
- Which users are making mistakes?
- Which settings or actions are involved?
- What is the most common mistake?
- Are there screenshots, recordings, support tickets, or analytics events?
- Is the preferred fix copy, grouping, validation, confirmation, or layout?

## Likely Affected Areas

- Settings page or route
- Settings form components
- Validation and confirmation flows
- Help text or empty states
- User documentation
- UI tests or accessibility tests

## Implementation Plan

1. Gather concrete examples of the confusing workflow from the maintainer, support tickets, analytics, or product notes.
2. Inspect the settings page structure, form behavior, validation, and existing tests.
3. Pick the smallest high-confidence improvement, such as clearer labels, grouping, validation copy, or confirmation around risky actions.
4. Keep behavior changes explicit and avoid changing unrelated settings.
5. Add or update tests for any changed form behavior.
6. Verify accessibility, keyboard navigation, and responsive layout if UI changes are made.
7. Update documentation or release notes if user-facing settings behavior changes.

## Risk Checklist

- [ ] The PR addresses a specific confusion point rather than a broad redesign.
- [ ] Existing settings behavior is preserved unless intentionally changed.
- [ ] Copy changes do not introduce ambiguity.
- [ ] Risky settings still have appropriate validation or confirmation.
- [ ] Accessibility and responsive layout are not regressed.

## Test Plan

### Automated Tests
- Update UI or form tests for changed labels, grouping, or validation behavior.
- Add regression coverage for any risky setting workflow that changed.

### Manual Verification
- Walk through the affected settings workflow as the target user.
- Verify changed copy, layout, and validation in desktop and mobile widths.
- Confirm unrelated settings are unchanged.

### Regression Checks
- Confirm saved settings persist correctly.
- Confirm validation and error states still work.
- Confirm keyboard and screen-reader flows remain usable.

## Pull Request Description

### Summary
Improves the settings page by clarifying the specific workflow that was causing user mistakes.

### Changes
- Identified the settings workflow responsible for confusion.
- Applied a scoped UI or copy improvement.
- Preserved existing settings behavior outside the targeted change.

### Testing
- Verified the affected settings workflow manually.
- Ran or updated relevant settings UI tests.
- Checked responsive and accessibility-sensitive behavior.

### Risk
Medium. Settings changes can confuse existing users if labels, grouping, or behavior shift unexpectedly.

### Related Issue
Closes #

## Reviewer Checklist

- [ ] The PR scope is tied to a concrete confusion point.
- [ ] Unrelated settings behavior is unchanged.
- [ ] Tests or manual checks cover the affected workflow.
- [ ] Accessibility and responsive layout were considered.
