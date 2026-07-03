# Open Items / Confirmation Required

This document lists the implementation-level items that must be confirmed against the live Backbase API reference/OpenAPI specification, target environment configuration, and Symitar integration design before final development sign-off.

| # | Item | Why Required | Owner/Source | Status |
|---|---|---|---|---|
| 1 | Exact IAM auth prefix and realm values | Required for login, token refresh, revoke, and logout | IAM / Environment config | Open |
| 2 | Final OAuth client IDs for Web, iOS, and Android | Required for PKCE/OIDC client setup | IAM / Security team | Open |
| 3 | Final redirect URI / deep-link scheme for each platform | Required for mobile and web callback handling | Mobile/Web + IAM team | Open |
| 4 | Exact token endpoint, refresh endpoint, revoke/logout behaviour | Required for session lifecycle and security | IAM guide / API reference | Open |
| 5 | MFA / OTP / step-up authentication requirement | Impacts login, high-risk payment, and transfer journeys | Security / Backbase team | Open |
| 6 | Exact user profile/context endpoint | Required to resolve user, service agreement, party/customer mapping | API reference/OpenAPI | Open |
| 7 | Source of partyId/customerId/memberId/UPID | Required for domain mapping and downstream API calls | Backbase/Symitar mapping | Open |
| 8 | Party Lifecycle API request/response payloads | Required for onboarding/member provisioning | API reference/OpenAPI | Open |
| 9 | Party Reference Data API list and enum values | Required for onboarding forms and validation | API reference/OpenAPI | Open |
| 10 | Current Account / Arrangement API exact endpoints | Required for account dashboard and account linking | API reference/OpenAPI | Open |
| 11 | Arrangement response schema and account identifier field names | Required by account dashboard, transaction, and payment journeys | API reference/OpenAPI | Open |
| 12 | Transaction API endpoint, pagination, filters, and sorting | Required for transaction screen implementation | API reference/OpenAPI | Open |
| 13 | Transaction sync schedule and acceptable freshness window | Required to explain online transaction visibility vs core posting | Stream/Symitar team | Open |
| 14 | Payment Order Service endpoint and payload schema | Required for internal transfer and ACH payment journeys | API reference/OpenAPI | Open |
| 15 | Payment lifecycle states and approval flow | Required for UI status, confirmation, retry, and notification handling | Payments/Access Control team | Open |
| 16 | Entitlement function names and privilege values | Required for server-side Access Control checks | Access Control config | Open |
| 17 | Daily and transactional limits by job role/member type | Required for transfer/payment validation and approval routing | Business + Access Control | Open |
| 18 | Symitar connector availability for member lookup | Required for onboarding and user/member mapping | Symitar integration team | Open |
| 19 | Symitar connector availability for share/loan/certificate account list | Required for account dashboard and arrangement ingestion | Symitar integration team | Open |
| 20 | Symitar connector availability for transaction history | Required for Stream transaction ingestion | Symitar integration team | Open |
| 21 | Symitar connector availability for internal transfer and ACH | Required for payment execution | Symitar integration team | Open |
| 22 | Notification channels after transfer/payment | Required for confirmation SMS/email/push/in-app notifications | Notification/business team | Open |
| 23 | Error response format across services | Required for common UI error handling | API reference/OpenAPI | Open |
| 24 | Production certificate/domain details for certificate pinning | Required for mobile security implementation | Infrastructure/security team | Open |

## Finalisation Rule

The document can be shared as a consolidated technical reference now. For implementation baseline/sign-off, close or explicitly defer the open items above and replace all illustrative endpoint paths and sample payloads with target-environment values.
