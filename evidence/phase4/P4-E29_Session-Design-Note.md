# Step 4.5B - Local session and leaver-block design

## Session duration

The Sunhaven Care Portal LAB uses a fixed local protected-session
duration of 15 minutes.

SESSION_REFRESH_EACH_REQUEST is disabled so normal page requests do
not extend the fixed local-session start time.

## Blocked-user control

The blocked_users table is keyed by the Microsoft Entra Object ID.

Before a protected route runs, the application checks:

1. The validated identity contains an Entra Object ID.
2. The Object ID is not actively blocked.
3. The local protected session has not exceeded 15 minutes.
4. The user's Entra application role permits the requested route.

## Denial behaviour

A blocked or expired user receives HTTP 403. The application records a
sanitized denial in app_audit_events and clears the local Flask session.

## Relationship with Entra ID

The local blocked-user control does not replace Entra account
disablement or Entra session revocation. The local check provides
prompt application denial for an already-open session. Entra
deprovisioning prevents future token acquisition and refresh.
