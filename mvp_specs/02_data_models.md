# Data Models (Mongo)

## users
- _id (ObjectId)
- email (unique, lowercase)
- passwordHash (nullable if Apple-only)
- appleSub (nullable)
- username (unique handle)
- role (user | admin)
- createdAt, updatedAt

## products
- _id
- sellerId (user)
- title/name
- brand (nullable)
- category
- size
- condition (enum)
- price (cents)
- descriptionShort
- mediaIds [ObjectId] (<=5)
- status (draft | active | sold | removed)
- tags (style/material/gender/event optional)
- createdAt, updatedAt

## mediaAssets
- _id
- ownerId (user)
- path (S3 key)
- mimeType
- sizeBytes
- width, height (optional)
- createdAt

## carts
- _id
- userId
- items: [{ productId, qty }]
- updatedAt

## orders
- _id
- userId (buyer)
- items: [{ productId, qty, priceAtPurchase }]
- amountTotal (cents)
- currency
- paymentProvider (stripe)
- paymentIntentId
- paymentStatus (requires_action | succeeded | failed | canceled)
- orderStatus (created | paid | fulfilled | canceled | refunded)
- shippingSummary (text) // minimal for MVP
- createdAt, updatedAt

## chatThreads
- _id
- buyerId
- sellerId
- adminId (optional if assigned)
- orderId (optional)
- status (open | closed)
- createdAt, updatedAt

## chatMessages
- _id
- threadId
- senderRole (buyer | seller | admin)
- text
- createdAt

## events/logs
- _id
- type (auth.login, product.create, order.pay, chat.send, etc.)
- actorId (optional)
- payload (json)
- createdAt

## indexes (high value)
- products: status+createdAt(desc), sellerId, category/size/condition, text index on name/brand (if needed)
- chatMessages: threadId+createdAt
- orders: userId+createdAt; paymentIntentId unique
- carts: userId unique
- users: email unique, username unique, appleSub unique
