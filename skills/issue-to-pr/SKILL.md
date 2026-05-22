---
name: issue-to-pr
description: Convert GitHub issues, bug reports, feature requests, refactor tasks, documentation requests, performance concerns, security concerns, and maintenance tasks into structured implementation plans, test plans, PR descriptions, and reviewer checklists before code changes begin.
---

# Issue to PR Skill

Use this skill when a user provides a GitHub issue, bug report, feature request, refactor task, documentation request, performance concern, security concern, or maintenance task and wants to turn it into a clear implementation workflow.

The goal is not to rush into code changes. The goal is to make the work understandable, bounded, reviewable, and testable before implementation begins.

## Core principles

1. Clarify the issue before proposing changes.
2. Prefer the smallest safe change that solves the issue.
3. Separate facts from assumptions.
4. Identify likely affected files or modules without pretending certainty.
5. Make risks, non-goals, and testing explicit.
6. Produce output that can be copied into a GitHub PR.
7. Avoid over-engineering unless the issue clearly requires architectural work.

## Do and don't

Do:

- Separate facts, assumptions, and open questions.
- Inspect the repository before naming exact files when codebase access is available.
- Keep the plan scoped to the smallest safe change that solves the issue.
- Include test gaps and manual checks when automation is not practical.
- Make security, compatibility, accessibility, and regression risks explicit when relevant.

Don't:

- Jump directly into implementation.
- Invent exact files, commands, failures, test results, or maintainer intent.
- Promise that tests pass unless they were actually run.
- Expand the issue into an unrelated refactor or redesign.
- Hide uncertainty; mark it as an assumption or question.

## Workflow

### 1. Restate the issue

Rewrite the issue in clear, concise language. Include what is happening, what should happen instead, who or what is affected, known environment details, and missing information that could affect implementation. Do not invent facts. Mark uncertain points as assumptions.

### 2. Classify the task type

Choose one primary type: bug fix, feature, refactor, documentation, test, performance, security, or chore. Add secondary types only when useful.

### 3. Extract requirements and constraints

Split the issue into functional requirements, non-functional requirements, constraints, non-goals, and open questions. Keep this short when the issue is small.

### 4. Identify likely affected areas

List likely files, folders, modules, components, tests, configuration, or documentation areas. Use cautious language such as likely, should inspect, possible, or depending on repository structure. Do not claim a file must be changed unless it is clearly known.

### 5. Produce an implementation plan

Create an ordered plan with concrete steps: reproduce the issue, inspect existing behavior, locate the responsible module, make the smallest safe change, update tests, verify regression risk, and update documentation when user-facing behavior changes.

### 6. Add a risk checklist

Include risks such as breaking backward compatibility, changing public API behavior, affecting unrelated platforms, weakening validation or security, adding flaky tests, creating accessibility regressions, or hiding the issue instead of fixing the root cause.

### 7. Add a test plan

Include unit tests, integration tests, manual verification, regression checks, edge cases, and platform/browser/device checks when relevant. If a test cannot be automated, say so and provide a manual check.

### 8. Generate a PR description

Write a PR description with Summary, Changes, Testing, Risk, and Related Issue. Keep it clean and ready to paste into GitHub.

### 9. Generate a reviewer checklist

Create a short checklist for reviewers focused on correctness, scope control, regression risk, and test coverage.

## Bundled resources

- Use `OUTPUT_FORMAT.md` when the user needs a stricter copyable output shape.
- Use `templates/pr-description.md` when the user specifically asks for PR text.
- Use `templates/test-plan.md` when the main deliverable is testing guidance.
- Use `templates/review-checklist.md` when the user asks for reviewer guidance.
- Use `examples/` to mirror tone and structure for common issue types.

## Default output format

```markdown
## Issue Summary

...

## Task Type

...

## Requirements and Constraints

### Requirements
- ...

### Constraints
- ...

### Non-goals
- ...

### Open Questions
- ...

## Likely Affected Areas

- ...

## Implementation Plan

1. ...
2. ...
3. ...

## Risk Checklist

- [ ] ...
- [ ] ...

## Test Plan

### Automated Tests
- ...

### Manual Verification
- ...

### Regression Checks
- ...

## Pull Request Description

### Summary
...

### Changes
- ...

### Testing
- ...

### Risk
- ...

### Related Issue
Closes #...

## Reviewer Checklist

- [ ] ...
- [ ] ...
```

## Style rules

- Be specific, not verbose.
- Prefer concrete steps over generic advice.
- Do not pretend to know repository internals that were not provided.
- Keep implementation plans scoped to the issue.
- Call out missing context only when it materially affects the work.
- Use Markdown that works well in GitHub issues and PRs.
- Make the final PR description easy to copy.

## Handling vague issues

When the issue is vague, still produce a useful first-pass plan. Add assumptions or open questions instead of blocking progress.

## Handling codebase access

If the repository is available, inspect the relevant files before naming exact affected files. If the repository is not available, describe likely areas at a conceptual level and avoid false certainty.

## When not to use this skill

Do not use this skill as a full implementation agent, automatic PR opener, or replacement for repository investigation. If the user asks to implement the issue immediately, use this skill first only when planning, risk framing, or PR drafting is materially useful.
