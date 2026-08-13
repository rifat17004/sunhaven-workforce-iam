# Sunhaven Care Workforce IAM — Final Handover Checklist

## Document control

- Project owner: Rifat Islam Emon
- Environment: Student-controlled Microsoft Entra LAB
- Application: Sunhaven Care Portal - LAB
- Handover date: 2026-08-13
- Tested release-candidate commit: 67c35f84a93d38b8f5169643d859bb11437c9c58
- Final release tag: `sunhaven-final-v1.0.0` — to be created after this checklist is committed
- Required GitHub visibility: Private
- Production healthcare system: No
- Real resident or patient data: No

## Final checklist

| ID | Handover requirement | Status | Evidence and decision |
|---|---|---|---|
| H-01 | All source code is committed, while `.env` files and secrets are excluded. | PASS | P7-E127 confirms a clean release-candidate worktree, zero tracked real `.env` files and Git exclusion of `app/.env`. TC-013 security adjudication and active-history validation passed. Final handover records will be committed during release closeout. |
| H-02 | All test accounts and resident data are clearly fictional. | PASS | Test identities and residents use TEST labels. P7-E89 confirms five fictional residents, TEST-formatted identifiers and zero stored care notes containing resident information. |
| H-03 | Final tenant, application, role and group identifiers are documented privately. | PASS | P7-E129 records the protected identifier inventory, its SHA-256 hash, permission mode 600 and storage outside Git. The private inventory must not be uploaded to GitHub. |
| H-04 | RBAC matrix, Joiner-Mover-Leaver rules, access review and risk register are versioned. | PASS | The repository contains versioned role design and JML automation, Phase 6 access-review evidence, P7-E122 residual-risk register and P7-E125 future roadmap. |
| H-05 | All MVP tests pass on the identified release candidate. | PASS | P7-E02 records PASS for TC-001 through TC-014. The tested release-candidate commit is `67c35f84a93d38b8f5169643d859bb11437c9c58`. |
| H-06 | The live demonstration has been rehearsed and backup evidence is available. | PASS | Phase 7 rehearsal evidence P7-E100 through P7-E119 records Joiner creation, role access, resident access, clinical denial and Leaver enforcement. P7-E116 through P7-E118 preserve sanitized authorization screenshots. |
| H-07 | Premium or trial dependencies and expiry conditions are disclosed. | PASS | P7-E122 records licensing and governance limitations. P7-E124 and P7-E130 disclose that premium Entra governance may require an eligible licence and that the recorded tenant contained no account subscription SKUs. |
| H-08 | Client secrets will be rotated or revoked after assessment if the lab is no longer required. | CONTROLLED DEFERRED ACTION | Credential revocation is intentionally deferred so the application remains available for marking and demonstration. P7-E130 requires revocation or rotation immediately after assessment acceptance. |
| H-09 | Test users and cloud resources will be removed or disabled according to the cleanup plan. | CONTROLLED DEFERRED ACTION | Several tested leaver identities are already disabled and stripped of governed access. Remaining lab cleanup is deferred until assessment completion and is governed by P7-E130. |
| H-10 | The report identifies the solution as a student lab rather than a production healthcare system. | PASS | P7-E124 and P7-E130 explicitly describe the project as a fictional student-controlled laboratory with no production healthcare deployment or real resident data. |

## Security and privacy disposition

- Actual `.env` files committed to Git: No
- Client secrets recorded in committed evidence: No
- Passwords or access tokens recorded in committed evidence: No
- Active Git history containing the reviewed unredacted transcript value: No
- Raw audit and sign-in exports stored in Git: No
- Private identifier inventory stored in Git: No
- Real resident or patient information used: No
- GitHub repository must remain private: Yes

## Operational disposition

The lab remains active only because it may be required for final assessment, evidence inspection and live demonstration. Continued activity does not represent production authorization.

After assessment acceptance, the project owner must execute P7-E130 and validate:

1. Remaining test identities are disabled or deleted.
2. Sign-in sessions are revoked.
3. Governed security-group memberships are removed.
4. Sunhaven application assignments are removed.
5. Application client credentials are revoked or rotated.
6. Retired application and group resources are removed.
7. Local credentials and temporary files are securely deleted.
8. Required sanitized evidence remains available.

## Known limitations

- The demonstration workflow is not a production IAM service.
- Microsoft Entra premium governance features depend on eligible licensing.
- Local SQLite session blocking is a lab compensating control.
- Human approval and exact approval phrases remain required for write operations.
- The full technical rehearsal passed but exceeded the preferred live-demonstration duration.
- Public GitHub publication is not approved because the evidence contains tenant-specific laboratory identifiers and screenshots.

## Handover decision

Technical implementation, core testing, security review, audit correlation, access review, live-demo rehearsal, evaluation and roadmap activities are complete.

Post-assessment credential revocation and environment cleanup remain controlled deferred actions because performing them now could prevent assessment or demonstration.

Prepared by: Rifat Islam Emon  
Preparation date: 2026-08-13  
Assessor acceptance: Not yet recorded  
Handover status: READY FOR FINAL RELEASE TAGGING AND PRIVATE REPOSITORY HANDOVER

Result: PASS
