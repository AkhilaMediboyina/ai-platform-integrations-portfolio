# Scheduled Instagram Reel Edge Function Design

## Objective

Design an edge function that publishes a scheduled Instagram Reel using the Meta Graph API.

The system should be reliable, fault tolerant, and prevent duplicate publishing.

---

# Architecture

User
↓
Scheduling API
↓
Database
↓
Scheduler
↓
Edge Function
↓
Meta Graph API
↓
Instagram Professional Account

The Edge Function also communicates with:

- Secrets Manager
- Job Queue
- Logging Service

---

# Authentication Model

The user connects their Instagram Professional account using Meta OAuth.

The backend securely stores:

- Access Token
- Refresh information
- Expiration time
- Granted permissions
- Instagram Account ID

Tokens are encrypted and never exposed to the frontend.

Before publishing, the edge function checks whether the token is close to expiration.

If necessary, the credential is refreshed before continuing.

If the account has been disconnected, the job is marked:

REAUTH_REQUIRED

instead of retrying forever.

---

# Publishing Flow

1. Scheduler triggers Edge Function.

2. Edge Function loads scheduled post.

3. Validate:

- account
- media URL
- caption
- publish time

4. Create Instagram media container.

5. Wait until Meta finishes processing.

6. Publish container.

7. Save Instagram Media ID.

8. Mark post as Published.

---

# Retry Strategy

Retry only temporary failures.

Examples:

- network timeout
- HTTP 429
- temporary Meta outage

Use:

- exponential backoff
- jitter
- maximum retry count

Permanent failures such as revoked tokens or invalid media are not retried repeatedly.

---

# Rate Limits

Use:

- request queue
- per-account concurrency
- caching
- pagination
- monitoring

If Meta returns rate-limit errors, delay future jobs using exponential backoff.

---

# Error Handling

Monitor:

- authentication failures
- publishing failures
- retries
- queue delays
- API latency

Log request IDs but never log access tokens.

---

# Testing

Unit Tests

- token expiration
- retry logic
- duplicate prevention

Integration Tests

- successful Reel publishing
- expired token
- invalid media
- Meta timeout
- duplicate scheduler events

Failure Tests

- network outage
- queue failure
- revoked token

The system should guarantee that one scheduled Reel is published only once.
