# Example: Feature Request

## Input Issue

```text
Feature: Add a dark mode toggle to the settings page.
Users should be able to switch between light mode, dark mode, and system default.
```

## Skill Output

## Issue Summary

Users need a theme preference control in the settings page with three options: light mode, dark mode, and system default. The selected preference should affect the application theme consistently.

## Task Type

Feature

## Requirements and Constraints

### Requirements
- Add a settings control for light, dark, and system default.
- Persist the selected preference.
- Apply the theme consistently across the app.
- Respect system preference when system default is selected.

### Constraints
- Existing theme implementation is unknown.
- Persistence mechanism should match existing app patterns.

### Non-goals
- Full redesign of the settings page.
- Creating new theme tokens unless current tokens are insufficient.

### Open Questions
- Does the app already have theme tokens or a theme provider?
- Should the preference sync across devices or stay local?

## Likely Affected Areas

- Settings page UI
- Theme provider or global layout
- User preferences storage
- CSS variables or design tokens
- Tests for settings and theme behavior

## Implementation Plan

1. Inspect the existing theme and settings architecture.
2. Identify where user preferences are stored.
3. Add a theme preference field with light, dark, and system options.
4. Update the theme application logic to resolve the active theme.
5. Add tests for preference selection and theme resolution.
6. Verify behavior across reloads and system preference changes.

## Risk Checklist

- [ ] Existing theme styles are not broken.
- [ ] Preference persistence follows project conventions.
- [ ] System default updates correctly when OS preference changes.
- [ ] The control is accessible by keyboard and screen readers.

## Test Plan

### Automated Tests
- Test that each theme option can be selected.
- Test that the selected preference is persisted.
- Test that system default resolves to the current system preference.

### Manual Verification
- Select light mode and reload.
- Select dark mode and reload.
- Select system default and change OS theme.
- Verify settings page and core app screens.

### Regression Checks
- Existing settings controls still work.
- No layout regressions in light or dark mode.

## Pull Request Description

### Summary
Adds a theme preference control to the settings page.

### Changes
- Added light, dark, and system default theme options.
- Persisted the selected theme preference.
- Updated theme resolution logic.
- Added tests for theme preference behavior.

### Testing
- Verified all three theme options manually.
- Verified persistence after reload.
- Ran settings and theme-related tests.

### Risk
Medium. Theme logic can affect broad UI surfaces, so visual regression review is recommended.

### Related Issue
Closes #

## Reviewer Checklist

- [ ] Theme preference behavior matches the issue.
- [ ] Settings UI is accessible.
- [ ] Theme persistence follows existing conventions.
- [ ] No obvious visual regressions in light or dark mode.
