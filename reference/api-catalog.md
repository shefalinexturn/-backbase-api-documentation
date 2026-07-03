# API Catalogue & Dependency Mapping

## 1. Catalogue Summary

| # | API/Service | Purpose | Method | Endpoint | Depends On | Provides |
|---|---|---|---|---|---|---|
| 1 | IAM Login/Auth API | Authenticate user | POST | To be confirmed | Username/password/client config | Access token, refresh token |
| 2 | User Profile/Context API | Get logged-in user context | GET | To be confirmed | Access token | User ID, party/customer ID |
| 3 | Entitlements API | Get permissions/features | GET | To be confirmed | Access token, user ID | Roles/permissions |
| 4 | Party Reference Data API | Load onboarding dropdown/reference data | GET | To be confirmed | Environment/token as applicable | Reference data |
| 5 | Party Lifecycle API | Create/update party/customer | POST/PUT | To be confirmed | Valid onboarding data | Party ID/customer ID |
| 6 | Current Account/Arrangement API | Create/link account | POST/GET | To be confirmed | Party/customer ID | Account/arrangement ID |
| 7 | Account List API | Fetch user accounts | GET | To be confirmed | Access token, optional customer ID | Account list |
| 8 | Transaction List API | Fetch account transactions | GET | To be confirmed | Access token + account/arrangement ID | Transactions |
| 9 | Transaction Detail API | Fetch transaction detail | GET | To be confirmed | Transaction ID | Transaction details |
| 10 | Logout/Revoke API | End session | POST | To be confirmed | Access/refresh token | Session terminated |

## 2. End-to-End Dependency Chain

```text
Login API
  -> access_token / refresh_token
      -> User Profile API
          -> userId / partyId / customerId
              -> Entitlements API
              -> Account List API
                  -> accountId / arrangementId
                      -> Transaction List API
                          -> transactionId
                              -> Transaction Detail API
```

## 3. Onboarding Dependency Chain

```text
Party Reference Data API
  -> reference values for form validation
      -> Party Lifecycle API
          -> partyId / customerId / membershipId
              -> Current Account / Arrangement API
                  -> accountId / arrangementId
                      -> IAM user linking / entitlement assignment
```

## 4. Common Headers

```http
Accept: application/json
Content-Type: application/json
Authorization: Bearer <access_token>
```

## 5. Common Response Data That Must Be Preserved

| Field | Why Important |
|---|---|
| `access_token` | Required for secured API calls |
| `refresh_token` | Required for refresh/revoke if enabled |
| `expires_in` | Used for expiry handling |
| `userId` | User-specific operations/audit |
| `partyId/customerId` | Customer/party mapping |
| `accountId/arrangementId` | Account and transaction journeys |
| `transactionId` | Transaction details/dispute/future journeys |

## 6. Confirmation Checklist Against API Reference HTML

- [ ] Confirm exact endpoint paths.
- [ ] Confirm HTTP methods.
- [ ] Confirm authentication scheme.
- [ ] Confirm required headers.
- [ ] Confirm request body schema.
- [ ] Confirm response body schema.
- [ ] Confirm error response format.
- [ ] Confirm pagination model.
- [ ] Confirm token refresh mechanism.
- [ ] Confirm service/domain names.


## 7. Symitar Mapping Summary

| Backbase Object / Concept | Symitar Source / Concept | Purpose | Notes / Dependency |
|---|---|---|---|
| Legal Entity | Member record | Represents the credit union member/customer in Backbase. | Must be created before service agreement, users, arrangements, and entitlements. |
| User | Online banking user / member identity | Represents the login identity mapped to the member. | Linked with IAM and service agreement context. |
| Service Agreement | Member access scope / digital banking relationship | Defines what the user can access and transact on. | Required for entitlement checks and context selection. |
| Arrangement | Share / Loan / Certificate account | Represents account product summary and balances in Backbase. | Used by dashboard, transaction history, and payment journeys. |
| Arrangement `externalId` | Symitar Share ID / Loan ID / Certificate ID | Links Backbase account representation to the core ledger account. | Must be preserved for core calls and reconciliation. |
| Transaction | Share/loan transaction history | Shows posted/pending account activity. | Freshness depends on transaction sync/cursor job. |
| Payment Order | Transfer / ACH / payment instruction | Initiates funds movement request from digital channel. | Symitar remains final execution/system of record. |
| Entitlement / Function Group | Digital banking role/permission | Controls account access, transfer/payment creation, approvals, and limits. | Must be enforced server-side through Access Control. |
| Limit | Payment/transfer limit | Controls transactional/daily thresholds and approval flow. | Required for high-value transfers and ACH/payment approval rules. |
| Notification | Alert/event from digital banking or payment lifecycle | Sends confirmation or status update to user. | Trigger depends on payment/account event completion. |

## 8. Endpoint Confirmation Required

The following endpoint shapes are useful for design discussion but must be validated from the target environment's OpenAPI/API reference before implementation:

| Area | Illustrative Endpoint Shape | Confirmation Needed |
|---|---|---|
| Arrangement Manager | `GET /api/arrangement-manager/client-api/v2/arrangements` | Confirm gateway route, version, query parameters, and response schema. |
| Transaction Manager | `GET /api/transaction-manager/client-api/v2/transactions` | Confirm exact endpoint, pagination, filters, account identifier name, and service-agreement/user headers. |
| Payment Order Service | `POST /api/payment-order-service/client-api/v2/payment-orders` | Confirm payment type values, body schema, lifecycle states, and approval handling. |
| IAM / Keycloak | `/{auth-prefix}/realms/{realm}/protocol/openid-connect/*` | Confirm auth prefix, realm, client IDs, redirect URI, refresh/revoke/logout behaviour. |
| Access Control | Permissions / entitlement endpoint | Confirm function names, privileges, service agreement requirements, and limit configuration. |

