# MVP Overview

## Goal
Deliver an iOS-first sustainable fashion marketplace MVP with modern UX, Apple Pay checkout, admin-mediated chat, and simple seller uploads.

## In-Scope (MVP)
- Auth: email/password, Apple ID login; username capture.
- Feed: infinite scroll of products (image, brand/name, condition, price); basic filters (category, size, gender, condition, material, style) as per Figma.
- Product page: gallery (<=5 imgs), short description, price, seller label (no PII), actions: add to cart, ask via LISH (admin chat).
- Upload item: 5 photos max; required fields (category, size, price, quality note). Phase 2 fields (color/style/event/cut/material) gated.
- Chat: admin relay (buyer → LISH admin → seller); no direct user-to-user; no media in chat for now.
- Payments: Apple Pay only (via Stripe Payment Intents); cart; order creation; order status/tracking; basic receipt.
- Notifications: in-app; push if time (permission screen exists).

## Out of Scope (MVP)
- User ratings/reviews; follows/profiles; AI recs/similar items; complex filters; product video; rich logistics; non-Apple Pay processors; wallets/fees/reports.

## Assumptions
- Platform: iOS first; Android later.
- Infra: AWS (S3+CloudFront, Mongo Atlas, API on ECS/Lambda) unless explicitly switched to Firebase.
- Chat transport: WebSocket preferred; can ship polling first.
- Admin: minimal internal endpoints/CLI for replies + moderation.
- Data residency/compliance: standard; no sensitive PII stored beyond auth basics.
