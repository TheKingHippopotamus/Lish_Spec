# Diagrams (Mermaid)

## User Flow (Buyer)
```mermaid
flowchart TD
    A[Welcome/Sign In] --> B[Feed]
    B --> C[Product Detail]
    C --> D[Ask via LISH Chat]
    C --> E[Add to Cart]
    E --> F[Cart Review]
    F --> G[Apple Pay Checkout]
    G --> H[Order Confirmation]
    H --> I[Order Details/Tracking]
    B -->|No products| B1[Empty State: friendly no-results UI with reset filters/refresh CTA]
```

## User Flow (Seller Upload)
```mermaid
flowchart TD
    A[Signed In Seller] --> B[Upload Item]
    B --> C["Pick Images (max 5)"]
    C --> D[Fill Required Fields]
    D --> E[Publish Product]
    E --> F[Product Active in Feed]
```

## System Architecture (Control-First AWS)
```mermaid
flowchart LR
    subgraph Client
    RN[React Native App]
    end

    subgraph Edge
    CF[CloudFront CDN]
    APIGW[API Gateway/Ingress]
    end

    subgraph Services
    AUTH[Auth Module]
    CAT[Catalog]
    MEDIA[Media]
    ORD[Orders/Payments]
    CHAT[Chat]
    NOTIF[Notifications]
    ADMIN[Admin]
    end

    subgraph Data
    DB[(Mongo Atlas)]
    S3[S3 Media]
    STRIPE[Stripe]
    LOGS[(Logs/Events)]
    end

    RN -- HTTPS --> APIGW
    RN -- Images --> CF
    APIGW --> AUTH
    APIGW --> CAT
    APIGW --> MEDIA
    APIGW --> ORD
    APIGW --> CHAT
    APIGW --> NOTIF
    APIGW --> ADMIN

    AUTH --> DB
    CAT --> DB
    MEDIA --> S3
    ORD --> DB
    ORD --> STRIPE
    CHAT --> DB
    NOTIF --> DB
    ADMIN --> DB

    APIGW --> LOGS
```

## Upload & Media Flow
```mermaid
sequenceDiagram
    participant App as RN App
    participant API as API (Media/Product)
    participant S3 as S3
    participant DB as Mongo

    App->>API: Request signed URL (mime/size)
    API->>S3: Generate pre-signed PUT
    API-->>App: {url, key}
    App->>S3: PUT image (max 5)
    App->>API: Create Product {fields, mediaKeys}
    API->>DB: Save product + media refs
    API-->>App: Product created/published
```

## Chat Flow (Admin Relay)
```mermaid
sequenceDiagram
    participant Buyer as Buyer App
    participant API as API (Chat)
    participant Admin as LISH Admin
    participant Seller as Seller App
    participant DB as Mongo

    Buyer->>API: Create thread / Send message
    API->>DB: Persist thread/message
    API-->>Admin: Deliver (WS/poll)
    Admin->>API: Reply
    API->>DB: Persist admin reply
    API-->>Seller: Deliver (WS/poll)
    Seller->>API: Reply
    API->>DB: Persist seller reply
    API-->>Buyer: Deliver (WS/poll)
```

## Payments & Orders Flow (Apple Pay via Stripe)
```mermaid
sequenceDiagram
    participant App as RN App
    participant API as Orders/Payments
    participant Stripe as Stripe
    participant Webhook as Webhook Handler
    participant DB as Mongo

    App->>API: Create checkout (cart)
    API->>Stripe: Create PaymentIntent (Apple Pay)
    Stripe-->>API: client_secret
    API-->>App: Payment sheet params
    App->>Stripe: Present Apple Pay / confirm
    Stripe-->>App: Success/Fail
    Stripe-->>Webhook: intent.succeeded/failed
    Webhook->>DB: Update order/payment status
    Webhook-->>App: (via API push/poll) status update
```
