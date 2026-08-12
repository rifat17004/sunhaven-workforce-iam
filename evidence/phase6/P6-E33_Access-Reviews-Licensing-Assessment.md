# Sunhaven Phase 6 Native Access Reviews Licensing Assessment

Evidence ID: P6-E33

## Assessment scope

This assessment determined whether the Sunhaven Care IAM Lab tenant could implement Microsoft Entra native Access Reviews as the optional enhanced-governance path described in Step 6.4 of the implementation handbook.

## Tenant

* Tenant name: Sunhaven Care IAM Lab
* Tenant ID: 72a753ee-6910-4a9b-a36e-e8790da83acb
* Tenant domain: rifat011002gmail.onmicrosoft.com
* Assessment date: 2026-08-13
* Environment: Fictional educational lab

## Licensing result

The Microsoft Entra admin center displayed “No account SKUs found” under Licenses > All products.

The tenant does not contain a Microsoft Entra ID Governance, Microsoft Entra Suite, or Microsoft Entra ID P2 product licence. Therefore, the tenant does not have the required entitlement for configuring a native Microsoft Entra Access Review of the Sunhaven application or governed groups.

## Implementation decision

Native Access Reviews were not configured.

No trial was activated, no licence was purchased and no directory changes were made during this assessment.

This result is recorded as an environmental licensing limitation, not an implementation failure.

## Existing compensating control

The project completed the manual access-review process in Step 6.3. That process included:

* Exporting the pre-review access inventory
* Recording explicit Approve and Deny decisions
* Identifying an unauthorized DefaultAccess assignment
* Producing a remediation dry run
* Applying the approved removal
* Exporting the post-review access inventory
* Confirming that all approved assignments remained
* Confirming that the denied assignment was removed
* Recording reviewer and operator separation

The final Step 6.3 validation result was PASS.

## Future licensed implementation

If Microsoft Entra ID Governance or Microsoft Entra Suite licensing becomes available, Sunhaven can replace or supplement the manual review with a scheduled native Access Review that:

* Assigns a named reviewer
* Records decisions and justifications
* Applies denied results
* Exports review history
* Regularly recertifies governed access

## Final outcome

* Native Access Reviews licence available: No
* Native review configured: No
* Trial or purchase initiated: No
* Directory write operations executed: 0
* Manual access-review control available: Yes
* Step 6.4 outcome: DOCUMENTED OPTIONAL ENHANCEMENT — NOT LICENSED
* Result: PASS

