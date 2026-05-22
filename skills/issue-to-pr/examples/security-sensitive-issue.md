# Example: Security-Sensitive Issue

## Input Issue

```text
Security: users may be able to download invoices from another organization by changing the invoice id in the URL.
Please verify and fix if confirmed.
```

## Skill Output

## Issue Summary

There is a possible authorization flaw in invoice downloads. A user may be able to access another organization's invoice by changing the invoice id in the URL. The expected behavior is that invoice downloads are restricted to users authorized for the invoice's organization.

## Task Type

Security / bug fix

## Requirements and Constraints

### Requirements
- Verify whether cross-organization invoice access is possible.
- Ensure invoice download authorization checks are enforced server-side.
- Add regression coverage for same-organization and cross-organization access.
- Avoid exposing sensitive invoice data in logs, tests, or PR text.

### Constraints
- The report is not yet confirmed.
- The affected endpoint, authorization model, and invoice storage layer are unknown.
- Security-sensitive details should be handled carefully.

### Non-goals
- Redesigning the full permission system unless the bug requires it.
- Changing invoice ids or URL structure as the only defense.
- Publishing exploit details beyond what reviewers need.

### Open Questions
- Which roles are allowed to download invoices?
- Are invoices scoped by organization, account, workspace, or tenant?
- Does the download path use signed URLs, direct file streaming, or a proxy endpoint?

## Likely Affected Areas

- Invoice download route or controller
- Authorization or policy layer
- Invoice lookup query
- Organization or tenant scoping logic
- Storage signed URL generation
- Invoice access tests
- Audit logging

## Implementation Plan

1. Inspect the invoice download flow and identify where authorization should be enforced.
2. Reproduce the reported behavior using two organizations and users with distinct access.
3. Verify whether invoice lookup is properly scoped to the requesting user's organization.
4. Fix the server-side authorization or tenant-scoping gap with the smallest safe change.
5. Add tests for allowed access, denied cross-organization access, missing invoices, and unauthorized users.
6. Review logging and error messages to avoid leaking invoice existence or sensitive data.
7. Verify the download flow still works for authorized users.

## Risk Checklist

- [ ] Authorization is enforced server-side, not only in UI routing.
- [ ] Cross-organization access is denied.
- [ ] Error responses do not leak sensitive invoice details.
- [ ] Existing authorized invoice downloads still work.
- [ ] Tests avoid real customer data and sensitive identifiers.

## Test Plan

### Automated Tests
- Add a test for an authorized user downloading an invoice in their organization.
- Add a test denying access to an invoice from another organization.
- Add a test for unauthenticated or unauthorized users.
- Add a test for missing or invalid invoice ids if relevant.

### Manual Verification
- Verify authorized invoice download works.
- Verify changing the invoice id does not expose another organization's invoice.
- Verify logs and responses do not expose sensitive invoice data.

### Regression Checks
- Confirm invoice list, invoice detail, and invoice download flows still agree on permissions.
- Confirm storage URL generation cannot bypass tenant checks.

## Pull Request Description

### Summary
Fixes a potential cross-organization authorization issue in invoice downloads.

### Changes
- Verified the invoice download authorization path.
- Enforced organization-scoped access before invoice download.
- Added regression coverage for allowed and denied invoice access.

### Testing
- Verified authorized invoice downloads still work.
- Verified cross-organization invoice access is denied.
- Ran invoice authorization tests.

### Risk
High. This touches authorization for billing documents, so reviewer focus should be on tenant scoping, error behavior, and regression coverage.

### Related Issue
Closes #

## Reviewer Checklist

- [ ] Authorization is checked before file access or signed URL creation.
- [ ] Invoice lookup is scoped to the requesting user's organization.
- [ ] Tests cover cross-organization denial.
- [ ] No sensitive data is exposed in logs, fixtures, or PR text.
