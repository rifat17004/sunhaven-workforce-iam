# Sunhaven Care Workforce IAM — Post-Assessment Cleanup Plan

## Document control

- Environment: Student-controlled Microsoft Entra LAB
- System: Sunhaven Care Portal - LAB
- Owner: Rifat Islam Emon
- Cleanup trigger: Completion and acceptance of the final assessment and live demonstration
- Current status: DEFERRED UNTIL ASSESSMENT COMPLETION
- Production healthcare system: No
- Real resident or patient data: No

## Purpose

This plan defines the controlled cleanup of the Sunhaven Care Workforce IAM laboratory after the assessment and demonstration are complete. Cleanup must not begin while the environment is still required for marking, evidence review, retesting or demonstration.

## Preconditions

Before cleanup:

1. Confirm the assessment and live demonstration are complete.
2. Confirm no further tenant access or retesting is required.
3. Confirm all required source code and sanitized evidence are committed.
4. Confirm the final Git release commit and tag are recorded.
5. Confirm the private identifier inventory and recovery material remain outside Git.
6. Confirm no password, client secret, access token or MFA registration secret exists in the repository.
7. Preserve only the minimum evidence required by the university retention requirements.

## Cleanup sequence

### 1. Disable remaining fictional test identities

Review all accounts created for the Sunhaven lab, including administrators, operators, auditors, workers and rehearsal identities.

Actions:

- Disable remaining enabled fictional test users.
- Revoke their active sign-in sessions.
- Confirm accountEnabled is False.
- Record the result without capturing passwords, tokens or private authentication data.

### 2. Remove governed access

For every fictional test identity:

- Remove membership from all SG-SC-* security groups.
- Remove all Sunhaven Care Portal application-role assignments.
- Confirm governed-group membership count is zero.
- Confirm care-application role-assignment count is zero.

### 3. Remove local application access

Actions:

- Retain active local blocks for leaver identities until the local lab is retired.
- Remove the local SQLite database only after required audit evidence has been preserved.
- Remove locally generated session files and development-only runtime data.
- Do not delete committed sanitized evidence.

### 4. Rotate or revoke application credentials

After the assessment:

- Revoke or delete the Sunhaven Care Portal client secret.
- Confirm the secret is no longer valid.
- Do not record the previous or replacement secret in Git, screenshots, reports or transcripts.
- If the application must be retained, create a new credential only when a new approved use begins.

### 5. Retire application and group resources

If the lab is no longer required:

- Remove the Sunhaven Care Portal enterprise-application assignments.
- Delete the application registration and service principal.
- Delete the SG-SC-* lab security groups after membership removal is verified.
- Delete or permanently disable remaining lab-only users.
- Preserve the tenant only if it is required for another approved student lab.

### 6. Remove local credentials and private temporary files

Actions:

- Delete the local `app/.env` file when the application is retired.
- Clear shell variables, clipboard contents and temporary directories used during testing.
- Review the private evidence directory and retain only approved records.
- Never upload the private identifier inventory, raw exports, recovery bundle or credential material to GitHub.

### 7. GitHub and repository handling

- Use a private GitHub repository for the project.
- Push only the sanitized active Git history.
- Do not upload `.env`, raw private exports, recovery bundles or private identifier inventories.
- Confirm repository secret scanning and history validation still pass after upload.
- Protect the final release tag from accidental modification.

## Premium and trial dependency disclosure

The student tenant did not contain account subscription SKUs during the recorded licensing check. Native Microsoft Entra access reviews and other premium governance functions may require Microsoft Entra ID Governance or another eligible premium licence.

The project therefore demonstrates access review through a documented, evidence-backed lab workflow rather than claiming a production licensed governance deployment.

Any premium or trial licence introduced later must have its product name, activation date and expiry date recorded before use.

## Evidence-retention rule

Retain:

- Sanitized source code
- Requirements and design documents
- Test crosswalk and PASS results
- Sanitized screenshots and audit reports
- Residual-risk register
- Lessons learned and roadmap
- Final handover checklist and release identifier

Keep outside Git:

- Raw audit and sign-in exports
- Private identifier inventory
- Recovery bundles
- Any file containing credentials, tokens, network identifiers or sensitive authentication information

## Completion criteria

Cleanup is complete only when:

- Remaining lab users are disabled or deleted.
- Sessions have been revoked.
- SG-SC-* memberships are removed.
- Sunhaven application assignments are removed.
- Client credentials are revoked or rotated.
- Retired application and group resources are deleted where appropriate.
- Local credentials and temporary files are removed.
- Sanitized evidence remains available.
- A final cleanup validation report records PASS.

## Current decision

Cleanup execution is intentionally deferred because the environment may still be required for assessment, evidence review and live demonstration.

No cleanup write operations were executed while creating this plan.

Result: PASS
