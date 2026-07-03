# Error Handling Reference

## 1. Common API Error Handling

| Status/Scenario | Meaning | App Behaviour |
|---|---|---|
| 400 Bad Request | Invalid request payload | Show validation message; do not retry automatically |
| 401 Unauthorized | Token missing/expired/invalid | Attempt refresh if enabled; otherwise logout |
| 403 Forbidden | User not allowed | Show access denied; hide restricted feature |
| 404 Not Found | Resource unavailable | Show data not found/empty state |
| 408 Timeout | Network timeout | Show retry option |
| 409 Conflict | Duplicate/conflicting data | Show conflict message and guidance |
| 423 Locked | Account locked | Show locked account support message |
| 429 Too Many Requests | Rate limit | Ask user to wait/retry later |
| 500 Server Error | Backend failure | Show generic error and retry |
| 503 Unavailable | Service unavailable | Show maintenance/unavailable message |

## 2. Login-Specific Errors

| Scenario | Behaviour |
|---|---|
| Wrong username/password | Show invalid login details |
| Password expired | Redirect to password reset/change flow if available |
| Account locked | Show account locked message |
| MFA required | Navigate to MFA screen |
| IAM unavailable | Show service unavailable/retry |

## 3. Account/Transaction Errors

| Scenario | Behaviour |
|---|---|
| No account linked | Show empty state and contact/support guidance |
| Account access forbidden | Show access denied |
| Transaction list empty | Show no transactions message |
| Invalid account/arrangement ID | Navigate back and refresh account list |

## 4. Standard Error Object - Placeholder

```json
{
  "errorCode": "INVALID_CREDENTIALS",
  "message": "Invalid username or password",
  "traceId": "trace-123",
  "timestamp": "2026-07-03T10:00:00Z"
}
```

## 5. Implementation Notes

- Do not expose raw technical server messages to end users.
- Log `traceId` for debugging, not sensitive fields.
- Use consistent error mapping across app/web.
- For 401, avoid infinite refresh loops.
