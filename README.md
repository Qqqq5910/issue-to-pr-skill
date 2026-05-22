# Issue to PR Skill

A lightweight agent skill that turns messy GitHub issues into clear implementation plans, test plans, and pull request descriptions for AI coding agents.

## Why this exists

AI coding agents are good at editing code, but they often struggle when the issue is vague, the repository is unfamiliar, or the expected PR standard is not explicit.

This skill gives agents a repeatable planning workflow before implementation begins.

## What it does

- Summarizes the issue
- Identifies likely affected areas
- Creates an implementation plan
- Generates a risk checklist
- Generates a test checklist
- Writes a clean PR description
- Adds a reviewer checklist

## Best for

- Open-source maintainers
- Indie hackers
- AI coding agent users
- Claude Code, Cursor, Codex, and similar workflows
- Contributors working on unfamiliar repositories

## Quick example

Input issue:

```text
Bug: Login button does not work on mobile Safari.
When tapped, nothing happens. It works on desktop Chrome.
```

Skill output:

```markdown
## Issue Summary

The login button does not respond to taps on mobile Safari, while the same flow works on desktop Chrome.

## Task Type

Bug fix

## Likely Affected Areas

- Login form component
- Button component
- Form submit handler
- Mobile or touch event handling
- CSS overlays, z-index, or pointer-events rules

## Implementation Plan

1. Reproduce the issue on mobile Safari or a WebKit-based environment.
2. Inspect the login button component, form submit handler, disabled state, and loading state.
3. Check whether CSS overlays, z-index, or pointer-events prevent taps.
4. Apply the smallest safe fix.
5. Add regression coverage for the login action.
6. Verify desktop behavior remains unchanged.

## Risk Checklist

- [ ] Desktop login behavior remains unchanged.
- [ ] Loading and disabled states still prevent duplicate submissions.
- [ ] The fix does not bypass form validation.
- [ ] The fix does not introduce accessibility regressions.

## Test Plan

### Automated Tests
- Add or update a test confirming that the login action is triggered when the button is activated.

### Manual Verification
- Verify login button works on mobile Safari.
- Verify login button still works on desktop Chrome.

## Pull Request Description

### Summary
Fixes the login button interaction issue on mobile Safari.

### Changes
- Adjusted login button interaction handling to support mobile Safari taps.
- Preserved existing desktop login behavior.
- Added regression coverage for the login button action.

### Testing
- Verified login on mobile Safari.
- Verified existing desktop Chrome login behavior.
- Ran the existing authentication tests.
```

## Structure

```text
skills/issue-to-pr/SKILL.md
skills/issue-to-pr/templates/
skills/issue-to-pr/examples/
```

## How to use

Copy the `skills/issue-to-pr` folder into your agent skills directory, then ask your agent to use the `issue-to-pr` skill on a GitHub issue, bug report, feature request, or refactor task.

Example prompt:

```text
Use the issue-to-pr skill on this issue:

Bug: Login button does not work on mobile Safari.
When tapped, nothing happens. It works on desktop Chrome.
```

## Templates included

- PR description template
- Test plan template
- Reviewer checklist template

## Examples included

- Bug issue
- Feature request
- Refactor task

## License

MIT License.
