# Implementation Readiness Addendum

## Current Status

The documentation is complete from a journey, sequence, dependency, security, and error-handling perspective. It is ready for internal review and technical walkthrough.

It is not yet a final implementation baseline until environment-specific API details are confirmed from the live Backbase OpenAPI/API reference and Symitar connector design.

## Pending Before Final Sign-Off

1. Confirm exact API gateway routes for Arrangement Manager, Transaction Manager, Payment Order Service, Access Control, and IAM.
2. Confirm auth-prefix, realm, OAuth client IDs, redirect URIs, and logout/revoke behaviour.
3. Replace all illustrative request/response payloads with exact API reference schemas.
4. Confirm Symitar connector coverage for member, account, transaction, transfer, and ACH use cases.
5. Confirm transaction ingestion schedule and acceptable freshness window.
6. Confirm entitlement function names, privilege values, limits, and approval rules.
7. Confirm MFA/step-up authentication rules for high-risk transfers/payments.
8. Confirm notification channels and event triggers.

## Suggested Review Message

Hi Anirban,

The documentation is complete from a journey, sequence, dependency, security, and error-handling perspective. A few implementation-level items are still marked for confirmation, mainly the exact API gateway routes, environment-specific auth prefix/realm, final request/response payloads from the live OpenAPI specification, and Symitar connector mappings.

I have kept those items clearly marked as illustrative / pending confirmation so the team can review and replace them once the environment-specific API reference is available.
