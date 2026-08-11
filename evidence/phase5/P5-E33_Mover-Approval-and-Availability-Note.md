# SC1008 Mover approval and availability note

## Change request

- Test ID: TC-006
- Employee ID: SC1008
- Worker: Isabella Green (TEST)
- Existing role: CareWorker
- Desired role: Nurse
- Existing facility: Sydney
- Desired facility: Sydney
- Status: Active
- Decision: APPROVED FOR LAB TEST

## Security reason

SC1008 is being moved from the CareWorker role to the Nurse role. The old CareWorker security-group membership and care-application role must be removed because access that is no longer justified must not remain after a role change.

## Action order

1. Resolve exactly one user using employeeId SC1008.
2. Verify the current CareWorker group and app role.
3. Remove the old CareWorker app role.
4. Remove the old SG-SC-CareWorkers group membership.
5. Update jobTitle and facility attributes.
6. Add SG-SC-Nurses.
7. Add the Nurse care-application role.
8. Revoke existing sign-in sessions.
9. Verify the old role is absent and the new role exists exactly once.
10. Test old-role denial and new-role access after a fresh sign-in.

## Availability trade-off

The workflow removes the old access before adding the new access. A short access gap can occur during processing. This temporary availability reduction is accepted in the lab because it prevents SC1008 from holding both CareWorker and Nurse access simultaneously.

## Safety conditions

- Do not match the user by display name.
- Do not create another identity.
- Do not remove unrelated assignments.
- Stop if zero or more than one employeeId match is found.
- Stop and record the result if any verification fails.
- Do not store passwords, tokens or MFA secrets.

## Approval

- Approved by: Sunhaven IAM Administrator (LAB)
- Environment: Sunhaven Care IAM Lab
- Approval date: 2026-08-11
