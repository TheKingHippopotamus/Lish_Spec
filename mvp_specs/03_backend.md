# Backend (Node TS)

## Stack
- Fastify or Nest; TS; Zod/class-validator; JWT; Stripe SDK; Socket.io (or polling); Mongoose/Prisma for Mongo.

## Modules & Key Endpoints

### Auth
- POST /auth/signup {email, password, username}
- POST /auth/login {email, password}
- POST /auth/apple {idToken}
- POST /auth/refresh
- GET /me (current user)

### Catalog
- GET /products?cursor=&limit=&category=&size=&gender=&condition=&material=&style=
- GET /products/:id

### Media
- POST /media/signed-url {mimeType, sizeBytes} -> {url, key}
- POST /media/complete {key, width, height}

### Upload/Product
- POST /products {title, brand?, category, size, condition, price, descriptionShort, mediaIds[]}
- PATCH /products/:id {fields...} (seller only)
- POST /products/:id/publish

### Cart
- GET /cart
- POST /cart/items {productId, qty}
- PATCH /cart/items/:productId {qty}
- DELETE /cart/items/:productId

### Orders/Payments
- POST /orders/checkout {cartId or items[]} -> creates order + Stripe PaymentIntent (Apple Pay)
- POST /orders/:id/confirm (optional if webhook handles)
- GET /orders/:id
- GET /orders (by user)
- Webhook /payments/stripe (intent succeeded/failed)

### Chat (Admin Relay)
- GET /threads (by user)
- POST /threads {productId?, orderId?, sellerId}
- GET /threads/:id/messages?cursor=&limit=
- POST /threads/:id/messages {text}
- Admin: GET /admin/threads, POST /admin/threads/:id/messages

### Notifications
- POST /notifications/test (internal)
- Hook for push token registration (if used)

### Admin
- Admin auth (role check)
- Product moderation endpoints (hide/remove)

## Validation & Limits
- Auth rate limits (per IP/email).
- Media: mime whitelist (jpeg/png/heic), size cap, count cap.
- Chat: text length cap; PII filter (phone/email regex guard) optional.
- Orders: price validation against product at purchase; stock handled by status (active/sold).

## Error Handling
- Consistent error envelope {error: {code, message, details}}.
- 401/403 for auth/role; 422 for validation; 409 for conflicts.

## Background Jobs (minimal)
- Stripe webhook processor.
- Order status updater (failed intents cleanup).
- Optional: daily log retention/cleanup.
