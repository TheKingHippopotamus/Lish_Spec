# Stack Options (choose later)

## Frontend
- React Native (default):
  - Option A: Bare RN + React Navigation + Stripe Apple Pay SDK. Pros: full control; Cons: more native setup.
  - Option B: Expo (bare or managed with custom dev client). Pros: faster DX; Cons: need custom builds for Apple Pay, extra config for native modules.

## Backend Runtime
- Option A: Node.js (TS) with Fastify/Nest (default). Pros: structured modules, great ecosystem; Cons: managing infra yourself.
- Option B: Firebase Functions. Pros: zero-ops, tight with Firebase Auth/Storage; Cons: Apple Pay via Stripe still required, Firestore pricing patterns, less control for chat WS.
- Option C: Serverless on AWS Lambda (API Gateway) with SST/Serverless Framework. Pros: low ops, pay-per-use; Cons: cold starts, WS setup overhead.

## Data Store
- Option A: Mongo Atlas (default). Pros: flexible schema, fast iteration; Cons: relational queries require care.
- Option B: Postgres (RDS/Aurora or Supabase). Pros: strong consistency/relations; Cons: more upfront modeling, media refs still in S3.
- Option C: Firestore (with Firebase stack). Pros: managed, realtime built-in; Cons: pricing on queries, complex aggregations, Apple Pay still via Stripe.

## Media Storage
- Option A: S3 + CloudFront (default). Pros: standard, configurable; Cons: setup required.
- Option B: Firebase Storage + CDN. Pros: integrated with Firebase; Cons: if not on Firebase, mixed stack.

## Payments
- Stripe Payment Intents with Apple Pay (required either way). No real alternative in MVP; Braintree/Adyen would add overhead.

## Chat Transport
- Option A: WebSocket (Socket.io or native WS) on Node/WS Gateway. Pros: realtime UX; Cons: infra complexity if serverless.
- Option B: Short polling (5–10s). Pros: simplest; Cons: more requests, less snappy.
- Option C: Firestore realtime (if Firebase). Pros: baked-in sync; Cons: lock-in, pricing considerations.

## Hosting/Infra
- Option A: AWS (default). Pros: flexibility, S3/CF, Stripe fits, Mongo Atlas peering; Cons: more setup.
- Option B: Firebase (Functions/Auth/Firestore/Storage). Pros: fastest start; Cons: WS complexity, pricing at scale, still need Stripe and Apple Pay entitlements.
- Option C: Render/Fly.io for API + Mongo Atlas + S3. Pros: simpler than AWS; Cons: fewer enterprise controls.

## Admin Interface
- Option A: Minimal internal web (React) hosted alongside API. Pros: control; Cons: build it.
- Option B: CLI/admin scripts hitting admin endpoints. Pros: fastest; Cons: poor UX.
- Option C: Retool-like tool on top of admin APIs. Pros: rapid; Cons: extra cost, permissions to manage.

## Recommendation Pathways
- Speed-first: Expo managed + Firebase (Auth/Firestore/Storage) + Functions + Stripe Apple Pay; polling chat. Risk: WS/chat nuance, pricing.
- Control-first (default): Bare RN + Node/Fastify on AWS (Lambda or ECS) + Mongo Atlas + S3/CF + Stripe; chat via WS. Balanced for growth.
- Middle-ground: Bare RN + Node on Render/Fly + Mongo Atlas + S3; chat via polling; fastest infra without Firebase lock-in.
