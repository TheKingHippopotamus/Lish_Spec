# Security, Quality, Performance

## Security
- Validation on all inputs; schema-based DTOs.
- JWT signing with rotation; refresh tokens; revoke on logout.
- Rate limits: auth (per IP/email), chat sends, uploads.
- PII minimization: only email + username; block phone/email patterns in chat.
- Storage permissions: signed URLs for uploads; read via CDN; no public write.
- Stripe webhook verification; idempotent handlers.
- Audit logs for orders, chats, admin actions.

## Testing
- Unit: services (auth, catalog, orders, chat).
- Integration: API endpoints (signup/login, feed, product detail, upload, cart, checkout, chat).
- E2E (happy paths): login, feed→product→chat; feed→product→cart→Apple Pay (sandbox); upload item.
- Mobile UI: key screens smoke (auth, feed, product, cart, chat, upload).

## Performance
- Feed pagination with cursors; indexes on products.
- CDN for images; size caps + compression client-side.
- App startup: lazy load heavy modules; cache tokens.
- Chat: WS preferred for reduced polling load.

## Reliability
- Retry policies on network calls (client + server to Stripe).
- Graceful degradation: if push unavailable, keep in-app notifications.
- Backoff on chat reconnects.
