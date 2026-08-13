# Sunhaven Workforce IAM live-demo rehearsal runbook

## Demonstration metadata

- Scenario: Joiner, authentication, authorization, leaver and audit
- Rehearsal employee ID: SC1013
- Rehearsal identity: Rehearsal Worker 01 (TEST)
- Initial role: CareWorker
- Facility: Sydney
- Tested release tag: sunhaven-mvp-v1.0.0
- Target duration: 10 minutes
- Data classification: Synthetic student-lab data only

## Safety rules

1. Never display or record a password, client secret, access token, QR code, recovery code or Authenticator approval number.
2. Keep the real `.env` file closed.
3. Use an Incognito window for the worker identity.
4. Keep the administrator account in the normal browser window.
5. Use only SC1013 during this rehearsal.
6. Confirm the tenant ID before every write operation.
7. Stop if the dry-run result is not the expected action.
8. Do not improvise a directory change during the demonstration.
9. If an Entra log is delayed, show the saved workflow event instead.
10. The final SC1013 state must be disabled with no governed access and an active local application block.

## Timed demonstration sequence

### 0:00–0:45 — Problem and architecture

Say:

> Sunhaven is a fictional care organisation. This student lab demonstrates identity lifecycle management for fictional workers. Approved workforce CSV data drives Microsoft Entra identities, security-group access and application roles. Microsoft Entra handles authentication and MFA, while the Flask application performs server-side role authorization. No real resident or healthcare data is used.

Show:

- The architecture diagram.
- The terminal located in the project repository.
- The frozen release tag.

### 0:45–2:15 — Joiner dry-run and apply

Say:

> I will first validate the approved workforce record and perform a read-only dry-run. The expected result is CREATE and zero write operations. I will then apply that exact approved plan.

Show:

- Input validation result: PASS.
- Dry-run result: CREATE.
- Tenant ID.
- Write operations executed by the dry-run: 0.
- Applied Joiner result: CREATED.
- PasswordRecorded: false.

Do not show:

- Temporary password.
- Clipboard contents.
- Password-change screen containing entered values.

### 2:15–3:30 — Identity and least-privilege assignments

Say:

> The Joiner created exactly one enabled identity. The user received the CareWorker security group and CareWorker application role, with no administrator role.

Show:

- Rehearsal Worker 01 (TEST) in Entra.
- Account enabled.
- Employee ID SC1013.
- SG-SC-CareWorkers membership.
- CareWorker enterprise-application role.
- No Entra administrative role.

### 3:30–5:15 — Worker sign-in, MFA, Allow and Deny

Say:

> Authentication and authorization are separate controls. Entra authenticates the user and requires MFA. The application then enforces the role on every protected request.

In the Incognito window:

1. Sign in as the SC1013 worker.
2. Complete the required password change privately.
3. Complete MFA privately.
4. Open `/whoami` and show the CareWorker claim.
5. Open `/residents` and show allowed fictional TEST residents.
6. Open `/clinical` and show HTTP 403.

Say:

> The same authenticated identity receives an allowed result for assigned residents and a denied result for the clinical route because CareWorker is not an approved clinical role.

### 5:15–6:45 — Leaver workflow

Say:

> The approved workforce record now changes to Leaving. The dry-run must propose DISABLE. The applied workflow follows a disable-first sequence.

Show the Leaver plan:

- Employee ID: SC1013.
- Action: DISABLE.
- Write operations executed by dry-run: 0.

Apply the workflow and show:

1. Account disabled.
2. Entra sessions revoked.
3. Governed groups removed.
4. Care-application assignments removed.
5. Local application block activated.
6. Final state verified.

### 6:45–8:00 — Immediate and future denial

Say:

> Directory disablement protects future authentication, while the local Object-ID block closes the existing Flask-session gap.

Demonstrate:

1. Refresh the already-open protected worker route.
2. Show the application Access Denied response.
3. Start a new Incognito sign-in attempt.
4. Show that the disabled account cannot authenticate.

Do not reveal the worker password during the new sign-in test.

### 8:00–9:15 — Audit and access-review evidence

Say:

> The lifecycle operation is traceable across the local application audit, the sanitized workflow event and Microsoft Entra logs.

Show:

- Sanitized Leaver workflow event.
- Local block status.
- Entra audit or sign-in failure.
- Phase 6 access-review Deny decision and remediation.
- UTC correlation evidence.

If a portal event is delayed, show the saved sanitized event and explain that portal ingestion may be delayed.

### 9:15–10:00 — Limitations and conclusion

Say:

> This is a student lab using fictional data, localhost hosting and a client secret. Security Defaults provides the available tenant baseline; advanced Conditional Access and native governance features depend on licensing. Entra disablement and session revocation may not instantly terminate an application-managed session, so the local Object-ID block provides prompt application denial. A production implementation would use managed hosting, certificate or managed-identity credentials, stronger monitoring, managed devices and formally governed approvals.

Finish with:

> The demonstration traces one fictional worker from approved Joiner data, through MFA and least-privilege access, to prompt Leaver removal and correlated audit evidence.

## Success criteria

- Demonstration duration is no more than 10 minutes.
- At least two minutes of contingency remains within the allocated assessment time.
- Joiner dry-run returns CREATE.
- Joiner apply returns CREATED.
- Worker receives CareWorker claim.
- `/residents` returns allowed access.
- `/clinical` returns HTTP 403.
- Leaver dry-run returns DISABLE.
- Leaver apply completes all containment actions.
- Existing application session is denied.
- New Entra authentication is blocked.
- Audit and access-review evidence is shown.
- No password, secret, token, QR code or recovery information is recorded.

## Backup evidence

If a live portal result is delayed, use:

- Phase 7 Joiner result and transcript.
- Worker-state export.
- CareWorker claim screenshot.
- Allow and Deny screenshots.
- Leaver workflow result and event.
- Local block status.
- Post-Leaver state export.
- Entra disabled-account sign-in failure.
- Phase 6 access-review remediation evidence.
- Phase 6 UTC event-correlation timeline.

## Rehearsal result

- Rehearsal start UTC:
- Rehearsal finish UTC:
- Total duration:
- Timing result:
- Technical result:
- Sensitive information exposed:
- Problems observed:
- Corrective action required:
- Final result:
