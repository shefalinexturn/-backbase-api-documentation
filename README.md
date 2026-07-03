# Backbase Journeys, API Sequences, and Dependencies

**Consolidated Reference — Credit Union Digital Banking Integration**

**Scope:** Backbase IAM Authentication, Secure Login, session/token handling, user context, member onboarding, account dashboard, transaction history, internal transfers, ACH/payment initiation, Backbase Stream onboarding, Symitar mapping, and logout journey documentation.

**Purpose:** This documentation converts the guide-style document into developer-friendly Markdown/HTML reference material. It explains journey-wise flow, API sequence, API dependencies, input/output references, error handling, and implementation notes.

> **Status Note:** This is complete as a journey, sequence, dependency, security, and error-handling reference for internal review and walkthrough. It should not be treated as the final implementation baseline until all environment-specific endpoints, payload schemas, auth-prefix/realm values, and Symitar connector mappings are confirmed from the live Backbase OpenAPI/API reference for the target environment. Items marked as illustrative or confirmation required must be validated before development sign-off.

> **Source Note:** The structure and patterns are based on Backbase module/API reference material, public Backbase sample repositories, and project-level analysis. Verified patterns and illustrative items are intentionally separated so the team can replace placeholders with exact target-environment values.


## Table of Contents

1. Overview and Document Status
2. Document Set
3. Assumptions
4. Journey Documentation Format
5. IAM Authentication and Secure Login
6. User Context and Session
7. Member Onboarding / Party / Account
8. Account Summary / Account Dashboard
9. Transaction History
10. Logout and Session Termination
11. API Catalogue and Dependency Mapping
12. Symitar Mapping Summary
13. Error Handling Reference
14. Token and Session Management
15. Mobile Implementation Notes
16. Open Items for Confirmation

## Assumptions

| # | Assumption | Impact |
|---|---|---|
| 1 | Backbase IAM / Keycloak is the identity provider for secured journeys. | All protected DBS calls require a valid access token. |
| 2 | Symitar remains the system of record for member, account, balance, transaction, and payment execution data. | Backbase stores/serves digital banking views, while core data accuracy depends on Symitar integration. |
| 3 | Backbase Stream is used to ingest Symitar data into DBS services. | Account and transaction visibility depends on Stream ingestion and cursor freshness. |
| 4 | Access Control is used for server-side entitlement enforcement. | UI-level hiding is not sufficient; APIs must enforce permissions. |
| 5 | Payment Order Service handles payment initiation lifecycle, while Symitar executes the actual core transaction. | A payment accepted by Backbase does not always mean the core transaction is posted. |
| 6 | Exact endpoint paths may vary by API gateway, realm, deployment, and environment configuration. | Final implementation must validate all URLs from the live OpenAPI/API reference. |

## Document Set

| File | Purpose |
|---|---|
| `index.html` | Browser-friendly complete documentation |
| `journeys/01-iam-authentication-secure-login.md` | Login and authentication journey |
| `journeys/02-user-context-session.md` | User profile/session context after login |
| `journeys/03-member-onboarding-party-account.md` | Member signup / Party / Account creation journey |
| `journeys/04-account-summary.md` | Account listing / account summary journey |
| `journeys/05-transaction-history.md` | Transaction list / transaction detail journey |
| `journeys/06-logout-session-termination.md` | Logout and session termination journey |
| `reference/api-catalog.md` | API catalogue and dependencies |
| `reference/error-handling.md` | Error cases and UI behaviour |
| `reference/token-session-management.md` | Token, refresh, secure storage notes |
| `reference/open-items.md` | Items requiring confirmation from API reference/team |
| `reference/implementation-readiness-addendum.md` | Final readiness notes and pending sign-off items |

## How to Use

1. Open `index.html` in a browser for a single-page reference.
2. Use Markdown files in GitHub, Confluence, or project documentation.
3. Replace placeholder endpoints with exact Backbase API reference values.
4. Validate request/response payloads with the shared Backbase API HTML.
5. Keep each journey updated as implementation progresses.

## Standard Journey Documentation Format

Each journey contains:

- Business purpose
- Actors and systems involved
- Preconditions
- Step-by-step sequence
- API dependency table
- Request/response reference
- Error scenarios
- Implementation notes
- Open confirmation items

