# Architecture

```
[iOS App]
  React Native (TS)
    |-- React Query (API)
    |-- Navigation
    |-- Apple Pay / Stripe SDK
    |-- WebSocket (chat) or polling
         |
[API Gateway]
   -> Auth Controller
   -> Catalog Controller
   -> Media Controller
   -> Orders/Payments Controller
   -> Chat Controller
   -> Notifications Hook
         |
[Backend (Node TS: Fastify/Nest)]
   Modules: auth, catalog, media, orders, chat, notifications, admin
         |
[Services]
   - Mongo Atlas (users/products/orders/chats)
   - S3 (+CloudFront) for media
   - Stripe (Apple Pay Payment Intents)
   - Sentry/Logging
```

## Frontend
- React Native (TS), React Navigation, React Query; Zustand/Context for session-only.
- Component library: lightweight atoms + theme tokens.
- Native modules: Apple Pay (Stripe SDK), image picker.

## Backend
- Node.js (TS) using Fastify or Nest for structured modules + validation.
- Modular services within one codebase; clear boundaries for future split.
- Validation: Zod/class-validator per DTO; rate limits on auth and chat.
- Auth: JWT access + refresh, Apple ID token verification.

## Data
- Mongo Atlas collections: users, products, mediaAssets, carts, orders, chatThreads, chatMessages, events/logs.
- Indexes: feed pagination (createdAt, status), products by seller, chat by thread, orders by user.

## Media
- Signed PUT uploads to S3; whitelist mime; cap size/count (<=5 per product).
- Public delivery via CloudFront; private originals optional later.

## Chat
- Admin-relay: enforce participant roles; block PII patterns; store audit log.
- Transport: WebSocket channel; polling fallback.

## Payments
- Apple Pay via Stripe Payment Intents; store Stripe IDs on orders; webhook for confirmation.

## Notifications
- In-app bus via API; push optional; email fallback for order receipts if needed.

## Observability
- Sentry for app + API; structured logs; minimal dashboards/alerts (errors, latency, payment failures).
