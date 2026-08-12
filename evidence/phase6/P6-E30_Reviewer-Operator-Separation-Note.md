# Sunhaven Phase 6 Reviewer and IAM Operator Separation Note

## Environment

This is a fictional, single-person student lab. No production identities, residents or health information were used.

## Reviewer function

Rifat Islam Emon acted as the fictional project reviewer. The reviewer examined the read-only pre-review inventory before any remediation was performed.

Every access record received an explicit Approve or Deny decision. A blank decision was not treated as approval.

Review evidence:

- P6-E17_Pre-Review-Access-Inventory.csv
- P6-E18_Pre-Review-Inventory-Summary.txt
- P6-E19_Completed-Access-Review.csv
- P6-E20_Access-Review-Decision-Summary.txt

## IAM operator function

After the decisions were recorded, Rifat Islam Emon acted separately as the lab IAM operator.

The operator:

1. Ran a no-write remediation dry run.
2. Verified the exact tenant, application, identity and assignment.
3. Used the required approval phrase.
4. Removed only the denied DefaultAccess assignment.
5. Re-exported and validated the resulting access state.

Remediation and validation evidence:

- P6-E21_Remediation-Dry-Run-Plan.json
- P6-E22_Remediation-Dry-Run-Transcript.txt
- P6-E23_Access-Review-Remediation-Result.json
- P6-E24_Access-Review-Remediation-Transcript.txt
- P6-E25_Post-Review-Access-Inventory.csv
- P6-E26_Post-Review-Inventory-Summary.txt
- P6-E27_Post-Review-Validation.txt
- P6-E28_Post-Review-Approved-Assignments.png
- P6-E29_IAM-Administrator-App-Denied.png

## Separation limitation

Because this is an individual student lab, two separate people and two separate privileged operator accounts were not available. Functional separation was implemented through ordered evidence, an immutable pre-review inventory, explicit decisions, a no-write dry run, exact approval text and independent post-change validation.

In a production environment, the business reviewer and IAM operator should be different authorized people wherever possible.

## Result

The review contained three Approve decisions and one Deny decision. The denied assignment was removed, the three approved assignments remained unchanged, and post-review validation returned PASS.
