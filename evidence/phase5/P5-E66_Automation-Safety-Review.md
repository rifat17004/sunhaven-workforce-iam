# Sunhaven Workforce Automation Safety Review

Review date: 2026-08-12

## Scope

The review covers:

- Invoke-SunhavenJoiner.ps1
- Invoke-SunhavenMover.ps1
- Invoke-SunhavenLeaver.ps1
- Get-WorkforceDryRunPlan.ps1
- Test-WorkforceInput.ps1

## Safety-control results

| Control | Result | Evidence |
|---|---|---|
| Dry-run before Graph writes | PASS | Workflows require an explicit Apply switch and exact approval text. |
| Match by employeeId | PASS | Workflows require exactly one matching workforce row and exactly one matching Entra identity. |
| Fail closed on zero or multiple matches | PASS | Unexpected match counts stop execution before writes. |
| Check existing access before adding | PASS | Existing groups, application roles and identity state are inspected before changes. |
| Idempotent rerun | PASS | Joiner, Mover and Leaver reruns return NO CHANGE with zero writes. |
| Structured sanitized results | PASS | Workflow results are written without passwords, tokens or client secrets. |
| Non-zero failure exit | PASS | Required workflow failures return a non-zero process exit. |
| Read state after every write | PARTIAL | All workflows verify the final desired state, but not every individual write has immediate readback. |
| Retry only known transient failures | PARTIAL | Joiner assignment retry currently retries every caught assignment error. |
| Controlled failure test | NOT RUN | A simulated failure must demonstrate an ERROR result and non-zero exit without directory changes. |

## Required Step 5.5 work

1. Restrict Joiner retries to known transient Graph failures.
2. Add focused readback verification for important writes.
3. Run a controlled failure test.
4. Prove that the failure produces a sanitized error and non-zero exit.
5. Confirm no unintended Entra changes occurred.

## Security conclusion

The existing workflows already provide dry-run protection, exact identity resolution, approval gates, final-state verification and idempotent reruns. Step 5.5 will harden transient-error handling and demonstrate safe failure behaviour.

## Final verification status

| Safety control | Final status | Evidence |
|---|---|---|
| Dry-run before writes | COMPLETE | Joiner, Mover and Leaver dry-run evidence |
| Exact employeeId matching and fail-closed validation | COMPLETE | Phase 5 validation and planning evidence |
| Existing assignments inspected before changes | COMPLETE | Joiner, Mover and Leaver planning results |
| Retry only known transient failures | COMPLETE | P5-E67 |
| Structured ERROR result without secrets | COMPLETE | P5-E68, P5-E69 and P5-E70 |
| Nonzero exit code after controlled failure | COMPLETE | P5-E70 |
| Joiner write read-back controls | COMPLETE | P5-E71 |
| Mover write read-back controls | COMPLETE | P5-E72 |
| Leaver write read-back controls | COMPLETE | P5-E72 |
| Joiner rerun produces no duplicate access | COMPLETE | P5-E26 through P5-E28 |
| Mover rerun produces no duplicate access | COMPLETE | P5-E44 through P5-E46 |
| Leaver rerun performs zero additional writes | COMPLETE | P5-E63 through P5-E65 |

## Conclusion

The Joiner, Mover and Leaver automation now fails closed, supports
read-only planning, verifies important directory changes through
bounded read-back checks, records structured secret-free failures and
returns a nonzero exit code when an operation fails.

The controlled failure test used a simulated authorization error.
It made no Microsoft Graph connection and executed zero directory
write operations.

Step 5.5 result: PASS.
