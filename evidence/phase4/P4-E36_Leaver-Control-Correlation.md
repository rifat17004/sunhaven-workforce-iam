# Step 4.5C - Leaver control correlation

## Test identity

A fictional TEST CareWorker identity was used. No real resident,
employee or clinical information was processed.

## Test sequence

1. The CareWorker was enabled in Microsoft Entra ID.
2. The CareWorker established an authenticated Flask application session.
3. The CareWorker's Entra Object ID was added to the application's
   blocked_users table.
4. The existing browser session was denied on its next protected request.
5. The Entra account was disabled.
6. Microsoft Entra sign-in sessions were revoked.
7. A new Incognito sign-in was attempted.
8. Microsoft Entra rejected the new authentication.

## Control correlation

| Test condition | Control responsible | Result | Evidence |
|---|---|---|---|
| Existing authenticated Flask session | Application blocked_users check | HTTP 403 | P4-E31 |
| New authentication attempt | Entra accountEnabled false | Sign-in denied | P4-E35 |
| Existing Entra refresh sessions | Entra session revocation | Refresh sessions invalidated | P4-E34 |
| Application denial audit | app_audit_events | DENY: local application block | P4-E32 |

## Security explanation

The local application block provides prompt denial for an already-open
Flask session. Disabling the Microsoft Entra account prevents new
authentication. Revoking Entra sessions invalidates refresh sessions
and requires reauthentication.

No single control covers the complete session lifecycle. The
application block complements Entra disablement and session revocation;
it does not replace them.
