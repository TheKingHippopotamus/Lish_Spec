# Execution Plan (AWS / Control-First)

Assumptions: Bare React Native, Node (Fastify/Nest), Mongo Atlas, AWS (API Gateway+Lambda or ECS Fargate), S3+CloudFront, Stripe Apple Pay, WebSocket chat.

## Week 1: Foundations & Infra Bootstrap
- Repos: app + api; TS configs; lint/format; husky hooks.
- CI/CD: GitHub Actions (lint/test/build) for both; env matrix (dev/stage/prod).
- IaC: choose runtime (Lambda+API GW via SST/Serverless, or ECS Fargate). Scaffold stacks: VPC (if ECS), API, S3 buckets (uploads/private, public), CloudFront distro, IAM roles, Secrets Manager/SSM params, Stripe webhook endpoint stub.
- Observability: Sentry keys wired, structured logs, base alerts (error rate, latency).
- Mobile shell: navigation, theme tokens, API client (React Query), auth context, error boundaries.
- Backend shell: project structure, Fastify/Nest bootstrap, health endpoint, request logging, validation pipe.

## Week 2: Auth & Feed
- Backend: user model (Mongo), JWT auth, refresh, Apple ID verify, rate limits. Routes: signup/login/refresh/me.
- Feed API: product schema, seed script, GET /products with cursor pagination + basic filters.
- App: Auth screens, token storage/refresh; feed screen with infinite scroll; loading/empty states.
- Infra: deploy auth/feed; CI deploy to dev; CloudFront hooked for static assets later.

## Week 3: Product & Cart Shell
- Backend: GET /products/:id; cart model + endpoints (add/update/remove, get cart).
- App: Product page (gallery, details, seller label); add-to-cart flows; cart screen shell; optimistic updates.
- Infra: tighten CORS, WAF rules for auth/cart.

## Week 4: Uploads & Media
- Backend: signed URL endpoint (S3), mime/size caps, media record persistence; product create/publish endpoints with validation (<=5 imgs).
- App: Image picker (cap 5), upload flow using signed URLs, form validation, publish product.
- Infra: S3 bucket policies; CloudFront paths; lifecycle for unused uploads.

## Week 5: Chat (Admin Relay)
- Backend: chat thread/message models, WS gateway (or long-poll fallback), endpoints for threads/messages; admin role enforcement; content length/PII guard.
- App: Chat UI, thread creation from product/order, unread indicator, reconnect/backoff.
- Admin: minimal CLI or protected endpoint to reply; logging for audit.
- Infra: WS support (API GW WebSocket or separate WS service), scale to zero config if Lambda.

## Week 6: Payments & Orders
- Backend: cart finalize, order creation, Stripe PaymentIntent for Apple Pay, webhook handler (idempotent); order statuses; receipts.
- App: Apple Pay sheet integration (Stripe), order confirmation, order details/tracking screen; error states.
- Infra: Stripe webhook deployed + secret rotation; alarms on payment failures.

## Week 7: QA, Perf, Launch
- E2E happy paths (login, feed→product→chat; feed→product→cart→Apple Pay; upload item).
- Fixes, perf (feed queries, image sizes via CloudFront headers), chat reconnect robustness.
- Analytics events; crash reporting confirmed; seed data for beta.
- TestFlight build; go/no-go checklist; stage->prod deploy.

## Key Tickets (sample granularity)
- IaC: provision API GW/Lambda (or ECS), S3 buckets, CloudFront, IAM, SSM params, Stripe webhook route.
- Backend: auth module (email/Apple), JWT/refresh + rate limits; catalog list/detail; cart CRUD; media signed URL + validation; product create/publish; chat threads/messages + WS; payments (PaymentIntent, webhook) + orders; notifications hooks.
- App: auth flow; feed with filters; product page; cart UI; Apple Pay integration; upload flow; chat UI; notifications/in-app banners.
- Ops: logging/alerts; admin role + endpoints; seed scripts; CI deploy pipelines; QA scripts.
