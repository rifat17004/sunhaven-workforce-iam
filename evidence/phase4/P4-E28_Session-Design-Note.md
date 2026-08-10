# Sunhaven Care Portal — Local Session and Leaver Design

## Environment

This design applies only to the Sunhaven Care IAM student laboratory.
All identities and residents are fictional TEST records.

## Local session duration

The normal local application session duration is 15 minutes.

For an accelerated verification test, the same control may be started with a
one-minute duration. The documented production-style laboratory value remains
15 minutes.

## Application-side leaver block

The application maintains a blocked_users table keyed by the trusted Microsoft
Entra Object ID (`oid`) claim.

Every sensitive application request will check:

1. The user has an authenticated Entra identity.
2. The Object ID is not actively blocked.
3. The local application session has not expired.
4. The user possesses one of the permitted application roles.

A blocked user receives HTTP 403 on the next protected request, including when
the browser already has an authenticated application session.

## Protected administration mechanism

For this student laboratory, app-side blocking is performed through the local
manage_blocked_user.py administration tool.

The tool requires local operating-system access, a valid Entra Object ID and an
explicit confirmation. Phase 5 automation will call the same reusable blocking
function.

## Microsoft Entra controls

Application blocking does not replace directory deprovisioning.

The leaver process must also:

1. Disable the Microsoft Entra user account.
2. Revoke the user's Entra sessions.
3. Remove or reconcile application and group assignments.

The application block produces prompt local denial. Entra disablement and
session revocation prevent future authentication and token renewal.

## Audit strategy

The application records:

- Administrator or workflow identifier
- Action
- Target Object ID
- UTC time
- Result

Tokens, passwords and client secrets are not recorded.

Directory audit evidence and application audit evidence will be correlated by
the target Entra Object ID and time.
