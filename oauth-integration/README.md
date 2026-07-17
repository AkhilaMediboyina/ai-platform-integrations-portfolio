# OAuth 2.0 Integration Service

## Purpose

This project demonstrates a reusable OAuth 2.0 connection service for third-party API integrations.

## Authentication Flow

1. The user selects **Connect Account**.
2. The backend generates a secure OAuth `state` value.
3. The user is redirected to the provider's login page.
4. The user grants permission.
5. The provider redirects to the callback URL with an authorization code.
6. The backend validates the `state` value.
7. The authorization code is exchanged for an access token and refresh token.
8. Tokens are encrypted before storage.
9. The connection is marked as active.

## Token Lifecycle

Before every API request, the system checks whether the access token is close to expiring.

If it is near expiration:

1. A single worker acquires a database lock.
2. The refresh token is used to obtain a new access token.
3. The new token and expiration time are stored securely.
4. The lock is released.
5. The original API request continues.

## Error Handling

- Retry temporary failures using exponential backoff.
- Handle network timeouts.
- Detect revoked refresh tokens.
- Mark revoked accounts as **REAUTH_REQUIRED**.
- Prevent multiple workers from refreshing the same token simultaneously.

## Security

- Encrypt tokens at rest.
- Never log access tokens.
- Validate the OAuth `state` parameter.
- Request only the minimum required scopes.
- Audit all token refresh operations.
