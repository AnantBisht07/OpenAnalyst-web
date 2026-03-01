# Desktop OAuth Integration Guide

Essential reference for VSCode Extension / OpenAnalyst desktop app integration.

---

## 1. Authentication URLs

| Environment | Sign-In URL |
|-------------|-------------|
| **Production** | `https://web.openanalyst.com/auth/sign-in?source=desktop` |
| Development | `http://localhost:3000/auth/sign-in?source=desktop` |

**Important:** The `?source=desktop` query parameter is **required**.

---

## 2. Custom Protocol Handler

Register handler for `openanalyst://` protocol.

| Event | URL Format |
|-------|------------|
| **Success** | `openanalyst://auth-callback?token=<CALLBACK_JWT>` |
| Error | `openanalyst://auth-error?error=<MSG>&code=<CODE>` |
| Logout | `openanalyst://logout-complete` |

---

## 3. Callback JWT Payload

The `token` parameter in the success callback is a JWT. **Decode it** to get:

```json
{
  "success": true,
  "isNewUser": false,
  "data": {
    "accessToken": "eyJhbGci...",
    "refreshToken": "eyJhbGci...",
    "expiresIn": 2592000,
    "user": {
      "_id": "694a54143443da94dad024eb",
      "email": "user@example.com",
      "fullName": "John Doe",
      "slug": "user-2"
    },
    "organizations": [
      {
        "_id": "694a54143443da94dad024ea",
        "name": "Organization",
        "slug": "org-2",
        "role": "admin",
        "accountType": "individual"
      }
    ],
    "currentOrgId": "694a54143443da94dad024ea"
  },
  "iat": 1766772506,
  "exp": 1766772806,
  "iss": "pipeshub-desktop-callback"
}
```

### Key Fields

| Field | Description |
|-------|-------------|
| `data.accessToken` | Use this for API calls (30-day expiry) |
| `data.refreshToken` | Use to refresh access token (90-day expiry) |
| `data.expiresIn` | Access token expiry in seconds (2592000 = 30 days) |
| `data.user` | User info: `_id`, `email`, `fullName`, `slug` |
| `data.organizations` | Array of orgs with `_id`, `name`, `slug`, `role`, `accountType` |
| `data.currentOrgId` | Currently selected organization ID |
| `isNewUser` | `true` if first login |

**Note:** Callback JWT expires in 5 minutes - process immediately.

---

## 4. API Base URLs

| Environment | Base URL |
|-------------|----------|
| **Production** | `https://web.openanalyst.com/api/v1/` |
| Development | `http://localhost:3000/api/v1/` |

### Authentication Header

```
Authorization: Bearer <ACCESS_TOKEN>
```

---

## 5. OpenAnalyst API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/openanalyst/health` | Health check |
| GET | `/openanalyst/user/profile` | Current user profile |
| GET | `/openanalyst/providers` | List AI providers |
| GET | `/openanalyst/providers/:id` | Get provider |
| GET | `/openanalyst/providers/:id/api-key` | Get decrypted API key |
| POST | `/openanalyst/providers` | Create provider |
| PUT | `/openanalyst/providers/:id` | Update provider |
| POST | `/openanalyst/providers/:id/test` | Test provider |
| DELETE | `/openanalyst/providers/:id` | Delete provider |
| GET | `/openanalyst/settings` | Get settings |
| PUT | `/openanalyst/settings` | Update settings |
| POST | `/openanalyst/settings/reset` | Reset to defaults |

---

## 6. Token Refresh

**Endpoint:** `POST /api/v1/userAccount/refresh-token`

**Header:**
```
Authorization: Bearer <REFRESH_TOKEN>
```

---

## 7. Logout

**Endpoint:** `POST /api/v1/userAccount/logout`

**Header:**
```
Authorization: Bearer <ACCESS_TOKEN>
```

---

## 8. Token Expiry

| Token | Expiry |
|-------|--------|
| Callback JWT | 5 minutes |
| Access Token | 30 days |
| Refresh Token | 90 days |

---

## 9. TypeScript Types

```typescript
interface CallbackPayload {
  success: boolean;
  isNewUser: boolean;
  data: {
    accessToken: string;
    refreshToken: string;
    expiresIn: number;
    user: {
      _id: string;
      email: string;
      fullName: string;
      slug: string;
    };
    organizations: Array<{
      _id: string;
      name: string;
      slug: string;
      role: 'admin' | 'member';
      accountType: 'individual' | 'business';
    }>;
    currentOrgId: string;
  };
  iat: number;
  exp: number;
  iss: string;
}
```

---

## 10. Code Example

```typescript
import { jwtDecode } from 'jwt-decode';

function handleAuthCallback(callbackUrl: string) {
  // 1. Extract token from URL
  const url = new URL(callbackUrl);
  const encodedToken = url.searchParams.get('token');

  // 2. URL-decode the token
  const callbackJwt = decodeURIComponent(encodedToken);

  // 3. Decode JWT to get payload
  const payload = jwtDecode<CallbackPayload>(callbackJwt);

  // 4. Extract what you need
  const { accessToken, refreshToken, user, organizations, currentOrgId } = payload.data;

  // 5. Store tokens securely and use for API calls
  return { accessToken, refreshToken, user, organizations, currentOrgId };
}
```

---

## 11. Error Codes

| Code | Description |
|------|-------------|
| `INVALID_CREDENTIALS` | Wrong email/password |
| `USER_NOT_FOUND` | User doesn't exist |
| `ACCOUNT_LOCKED` | Account locked |
| `SESSION_EXPIRED` | Session expired |

---

## Quick Checklist

- [ ] Open `https://web.openanalyst.com/auth/sign-in?source=desktop` in browser
- [ ] Register `openanalyst://` protocol handler
- [ ] Handle `openanalyst://auth-callback?token=<JWT>` callback
- [ ] URL-decode then JWT-decode the token parameter
- [ ] Extract `data.accessToken` and `data.refreshToken` from payload
- [ ] Store tokens securely
- [ ] Use `Authorization: Bearer <accessToken>` for API calls
