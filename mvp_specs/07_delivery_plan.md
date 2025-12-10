# Delivery Plan (MVP)

## Week 1: Foundations
- Repos, CI, lint/format, env handling.
- Design tokens + base components.
- Auth skeleton (signup/login, Apple ID token verify stub), navigation, API client.

## Week 2: Feed
- Product schema, seed data, feed endpoint with pagination + basic filters.
- RN feed screen + filters; loading/empty states.

## Week 3: Product + Cart Shell
- Product detail endpoint; product page UI (gallery, details, seller label).
- Cart client state; cart endpoints stub.

## Week 4: Upload Item
- Image picker (cap 5), signed uploads, validations.
- Create/publish product endpoint + UI.

## Week 5: Chat (Admin Relay)
- Thread/message models; WS/polling; chat endpoints; admin role checks.
- RN chat UI; entry from product/order.

## Week 6: Payments & Orders
- Stripe Apple Pay integration; PaymentIntent creation.
- Order creation/status; cart backend; order detail page.
- Webhook handling; receipts/logging.

## Week 7: QA & Launch Prep
- E2E happy paths; fixes; perf passes (feed, images, chat reconnect).
- Analytics events; Sentry wired; seed data; TestFlight build; go/no-go checklist.

## Checkpoints/Approvals
- Confirm infra choice (AWS vs Firebase) and chat transport (WS vs polling) at start.
- Review Apple Pay sandbox test plan by Week 5.
- Admin ops flow confirmed by Week 5 (how admins reply).





echo "# Lish_Spec" >> README.md
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:TheKingHippopotamus/Lish_Spec.git
git push -u origin main