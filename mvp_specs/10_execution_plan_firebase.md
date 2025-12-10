# Execution Plan (Firebase / Speed-First)

Assumptions: Expo-managed or bare RN (with custom dev client for Apple Pay), Firebase Auth/Firestore/Storage/Functions, Stripe for Apple Pay, chat via Firestore realtime or polling.

## Week 1: Foundations & Firebase Setup
- Repos: app + minimal functions; TS, lint/format, CI (GitHub Actions) for app/functions.
- Firebase project(s): dev/stage/prod; enable Auth (email/password, Apple ID), Firestore, Storage, Functions. Set security rules skeletons.
- App shell: navigation, theme tokens, API layer using Firebase SDK (Auth, Firestore, Storage), React Query wrappers, error boundaries.
- Stripe keys/config for Apple Pay (test mode); create Functions project scaffold.

## Week 2: Auth & Feed
- Auth flow in app: email login/signup, Apple ID; token persistence/refresh.
- Firestore: collections for users/products; seed script; indexes for feed.
- Feed screen: Firestore paginated query (startAfter) with basic filters.
- Functions (if needed): cloud callable for feed to encapsulate rules.
- Rules: read access for active products; write constraints per owner.

## Week 3: Product & Cart Shell
- Product detail fetch; product page UI.
- Cart: client-side state first; Firestore cart doc per user (optional to persist).
- Firestore rules: limit cart writes to owner.

## Week 4: Uploads & Media
- Storage: upload rules (auth required, path by user, size/type caps); upload via client SDK; store media metadata in Firestore.
- Product creation: Firestore write with validation (<=5 media refs); draft/publish flags.
- Rules: enforce media ownership and product ownership.

## Week 5: Chat (Admin Relay)
- Model: threads/messages collections with roles; Firestore realtime listeners.
- App: chat UI using snapshot listeners; unread indicators.
- Admin: dedicated admin account with separate app/CLI; role stored in user doc; rules to allow admin to post on any thread.
- Moderation: optional PII regex check in client/Function.

## Week 6: Payments & Orders
- Functions: create Stripe PaymentIntent (Apple Pay), verify client_secret, write order doc with statuses; Stripe webhook via HTTPS Function to update order/payment status (idempotent).
- App: Apple Pay sheet (Stripe), order confirmation, order details/tracking screen.
- Rules: restrict order read to buyer; prevent edits post-creation.

## Week 7: QA & Launch
- E2E happy paths; fix issues; perf passes on Firestore queries (indexes, limits) and Storage sizes.
- Analytics events (Firebase Analytics) + crash reporting (Crashlytics/Sentry optional).
- Seed data; TestFlight build; go/no-go checklist.

## Key Tickets (sample granularity)
- Firebase: projects, Auth providers, Firestore rules (products, carts, orders, chats), Storage rules, Functions deploy, indexes.
- Functions: feed callable (optional), PaymentIntent creation, Stripe webhook handler, order state updates, admin tools (optional callable), PII guard (optional).
- App: auth flow; feed w/ Firestore pagination; product page; cart (client/Firestore); upload flow with Storage + Firestore; chat with snapshot listeners; Apple Pay integration with Stripe; notifications (Firebase push if time) or in-app banners.
- Ops: CI for app + functions; environment configs per project; seed scripts; QA scripts.
