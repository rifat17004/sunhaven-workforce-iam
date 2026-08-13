# Sunhaven Workforce IAM — Lessons Learned

## Purpose

This document evaluates lessons learned from designing, implementing and testing the fictional Sunhaven workforce IAM lab. Conclusions are based on recorded project evidence rather than assumptions.

## 1. Security lessons

### Defence in depth is necessary for leaver control

Disabling the Entra account and revoking sessions are essential, but token invalidation may not become observable immediately in every application. The local application block provided an additional server-side control that denied the existing SC1013 request immediately after the Leaver workflow.

Evidence:

- Leaver workflow execution: 7.57 seconds
- Workflow start to observed application denial: 16.76 seconds
- Denial reason: `DENY: local application block`

### Authorization must be enforced by the application

Entra app-role claims identify the worker’s authorized role, but the Flask application must still validate that role for every protected route. Testing confirmed that a CareWorker could access assigned fictional residents but could not access the clinical route.

### Fail-closed safeguards prevent operator mistakes

During rehearsal, an incorrect approval phrase was rejected before any directory write occurred. Exact approval text, explicit tenant validation, dry-run planning, immutable Object IDs and post-operation readback reduced the risk of modifying the wrong identity or tenant.

### Secrets and health information require separate controls

The project prevented secrets from being committed and used only fictional TEST residents. However, a production service would still require managed credential storage, encryption, privacy assessment, retention controls and centralized monitoring.

## 2. Usability lessons

### Initial authentication creates necessary friction

The first sign-in required a password change and MFA registration. This increased onboarding effort, but it reduced the risks associated with temporary credentials and account takeover.

The measured interval from identity creation to first successful application access was 339.77 seconds, approximately 5 minutes 40 seconds.

### Role-specific interfaces reduce unnecessary exposure

Workers saw only the routes permitted by their application role. Clear HTTP 403 pages helped distinguish an authorization denial from an application failure.

### Shared-device use requires additional design

Short sessions and local blocking reduce risk, but they do not fully control unattended browsers on shared care workstations. Production deployment should add managed shared-device settings, automatic data clearing and documented sign-out procedures.

## 3. Automation lessons

### Dry-run planning should precede every lifecycle change

The Joiner and Leaver workflows produced read-only plans before applying changes. This allowed the operator to inspect the proposed identity, group, role and action before authorizing writes.

### Idempotency makes reruns safer

Repeated Joiner, Mover and Leaver operations returned `NO CHANGE` when the intended state already existed. This reduced the risk of duplicate identities, duplicate assignments and unnecessary writes.

### Readback verification is as important as execution

A successful API response does not by itself prove the intended final state. The automation therefore read back account status, group membership, application roles, session actions and local block state.

### Manual CSV input remains a risk

Validation caught invalid roles and duplicate employee IDs, but manually preparing CSV files can still introduce errors or delays. A production design should obtain approved workforce changes directly from an authoritative HR system.

## 4. Monitoring and evidence lessons

### UTC timestamps make event correlation possible

Using UTC across lifecycle output, Entra logs and application audit events allowed Joiner, access, Mover and Leaver events to be placed on one consistent timeline.

### Portal logs may not appear immediately

Microsoft Entra audit and sign-in records can be delayed. Sanitized exports, raw-file hashes and backup screenshots prevented the demonstration from depending on immediate portal availability.

### Evidence must be sanitized before Git storage

Raw exports may contain IP addresses, device information, session identifiers and other sensitive metadata. The project retained raw evidence privately and committed only sanitized reports and hashes.

## 5. Demonstration lessons

The technical rehearsal passed, but its duration was 1,137 seconds, or 18 minutes 57 seconds. This exceeded the 10-minute demonstration allocation.

The live presentation should therefore:

1. Use an eight-minute primary path with two minutes spare.
2. Pre-position all required browser tabs and terminals.
3. Use prepared commands with verified approval phrases.
4. Explain the architecture in no more than 30 seconds.
5. Show only one allowed action and one denied action.
6. Use backup screenshots when portal logs are delayed.
7. Avoid repeating detailed test evidence already established in Step 7.1.

## 6. Overall conclusion

The lab demonstrated secure Joiner, Mover, Leaver, role-based authorization, MFA, session control, audit correlation and access-review remediation using fictional data.

The core technical controls worked as intended. The most important remaining improvements are production-grade hosting, centralized audit retention, managed credential storage, licensed governance capabilities, shared-device protections and a shorter demonstration workflow.

Result: PASS
