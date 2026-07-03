# Token & Session Management Reference

## 1. Token Lifecycle

```text
User Login
  -> IAM validates credentials
    -> Access token issued
      -> App uses token in Authorization header
        -> Token expires
          -> Refresh token flow if supported
            -> New access token
          -> Otherwise redirect to login
```

## 2. Storage Recommendations

| Platform | Recommended Storage |
|---|---|
| Android | Keystore / Encrypted Shared Preferences |
| iOS | Keychain |
| Web | Secure HTTP-only cookies where possible; avoid unsafe local storage for sensitive tokens |

## 3. Rules

- Never store password.
- Never print tokens in logs.
- Clear token on logout.
- Clear token on unrecoverable 401.
- Refresh token only once per expiry event to avoid duplicate calls.
- Do not call protected APIs without a valid token.

## 4. API Header

```http
Authorization: Bearer <access_token>
```

## 5. Refresh Flow - If Supported

**Method:** `POST`  
**Endpoint:** `To be confirmed from IAM API reference`

```json
{
  "grant_type": "refresh_token",
  "refresh_token": "<refresh_token>",
  "client_id": "mobile-app-client"
}
```

## 6. Session Expiry UI

| Situation | UI Action |
|---|---|
| Access token expired, refresh success | Continue silently |
| Access token expired, refresh failed | Show session expired and redirect to login |
| Refresh token expired | Redirect to login |
| Logout clicked | Clear session and redirect immediately |


## 6. Mobile Implementation Notes

| # | Note | Implementation Guidance |
|---|---|---|
| 1 | Use PKCE authorization code flow for mobile apps. | Do not use password grant for native/mobile clients unless explicitly approved by architecture/security. |
| 2 | Do not store credentials in plain text. | Store only tokens/session metadata using platform-secure storage. |
| 3 | Android token storage | Use EncryptedSharedPreferences or Keystore-backed secure storage. |
| 4 | iOS token storage | Use Keychain with an appropriate accessibility setting. |
| 5 | Token refresh | Refresh before expiry where possible; on 401, attempt refresh once before forcing logout. |
| 6 | Redirect URI / deep link | Confirm final redirect scheme for each platform, for example client-specific `app://callback`. |
| 7 | Certificate pinning | Enable only after final production certificates/domains are confirmed; maintain rotation strategy. |
| 8 | Logout | Clear local token/session data after server-side revoke/logout completes or when refresh fails. |
| 9 | Session context | If multiple service agreements are available, mobile must handle context selection before protected journeys. |
| 10 | Infinite-loop prevention | Avoid repeated refresh attempts when IAM returns invalid_grant or refresh token expiry. |

