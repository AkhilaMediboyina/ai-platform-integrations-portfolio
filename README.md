# AI and Platform Integrations Portfolio

This portfolio contains examples of my work and technical designs involving:

- OAuth 2.0 authorization and token lifecycle management
- REST API integrations
- LLM prompt engineering and structured JSON outputs
- Retry handling, rate limits, and idempotency
- Meta Graph API publishing architecture
- Production monitoring and error handling

## Projects

### OAuth 2.0 Integration Service

A reusable OAuth 2.0 integration design supporting:

- Authorization Code Flow
- Secure token storage
- Token expiration handling
- Refresh-token rotation
- Scope validation
- Reauthorization handling
- Audit logging
- Concurrent refresh protection

### AI Brand Voice and Creative Workflow

An AI content workflow designed with:

- Structured JSON responses
- Prompt templates
- Brand rules
- Schema validation
- Human approval checkpoints
- Retry and repair logic

### LLM Gateway

An LLM gateway architecture supporting:

- Multiple model providers
- Token and cost tracking
- Model routing
- Response caching
- Fallback models
- JSON schema validation
- Latency monitoring

### Meta and Google Integration Prototype

A prototype integration design covering:

- OAuth-based account connections
- API pagination
- Campaign-data retrieval
- Webhook processing
- Rate-limit handling
- Token-expiry management
- Retry policies

## Instagram Scheduled Reel Design

The repository also includes a system design for publishing a scheduled Reel through the Meta Graph API.

This is a design and prototype portfolio. It does not represent a production deployment for an external customer.

---

## Portfolio Contents

### OAuth 2.0 Integration Service
Location: `/oauth-integration`

Topics covered:

- Authorization Code Flow
- Secure token storage
- Token refresh
- Token expiration
- Reauthorization
- Retry strategy

---

### Structured LLM Prompt Engineering
Location: `/structured-output-prompt`

Topics covered:

- JSON schema
- Prompt engineering
- Structured outputs
- Validation
- Reliability

---

### Instagram Reel Publishing System Design
Location: `/meta-reel-design`

Topics covered:

- Meta Graph API
- Edge Functions
- Scheduling
- Retry strategy
- Authentication
- Rate limits
- Error handling
