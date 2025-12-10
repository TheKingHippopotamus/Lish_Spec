# Infra & Ops (MVP)

## Core
- AWS: API on ECS Fargate or Lambda+API Gateway; S3 + CloudFront for media; Mongo Atlas for DB.
- CI/CD: GitHub Actions (lint/test/build), deploy API (IaC), build RN (fastlane/EAS if Expo bare).
- Secrets: SSM/Secrets Manager; .env for local.

## Networking/Security
- HTTPS everywhere; CORS restricted to app origins.
- IAM least privilege for S3/Stripe keys.
- WAF/rate limits on auth/chat endpoints.

## Observability
- Logging: structured JSON to CloudWatch; request IDs.
- Error tracking: Sentry (app + API).
- Metrics/alerts: error rate, latency p95, Stripe webhook failures, chat WS disconnect spikes.

## Storage
- Buckets: media-uploads (private) and media-public (served via CloudFront). Optionally same bucket with different prefixes + policies.
- Lifecycle: consider expiry for unused uploads.

## Deploy
- Envs: dev/stage/prod; separate DBs/buckets/keys.
- Database backups enabled.

## Admin Access
- Admin role in auth; restricted endpoints; optional basic web UI later.

## Compliance/Safety
- Minimal PII; no sensitive data stored; log redaction for tokens.
