# Mobile App (React Native)

## Stack
- React Native (TS), React Navigation, React Query, minimal Zustand/Context for auth, Stripe Apple Pay, image picker, Socket.io (or polling).

## Flows & Screens
- Onboarding/Auth: welcome_page, email_sign_in (+ variant), otp (if needed), username, notification_permission.
- Feed: offers_page + filters (category/size/gender/condition/material/style/sizes screen) with infinite scroll.
- Product: product detail (from feed) with gallery (<=5), description, price, seller label; actions: add to cart, Ask via LISH (chat entry).
- Upload item: sell_product flow; image picker (5 max), required fields (category, size, price, quality note), submit/publish.
- Cart & Checkout: shopping_cart_* screens, payment, order_completed, order_details_tracking; Apple Pay sheet.
- Chat: chat screen for admin relay; entry from product/order; unread indicator.
- Profile: profile_self_* and profile_other_* (listings, basic info), no follows/ratings.
- Notifications: notifications/messages_page; in-app banners; push prompt if enabled.

## Components (reuse)
- Buttons, Inputs, Form controls, ProductCard, MediaCarousel, ChatBubble, Badge, Toast/Sheet.
- Hooks: useAuth, useFeed, useProduct, useCart, useUpload, useChatThread, useNotifications.

## State/Data
- React Query caches for feed/products/cart/orders/chat.
- Secure storage for tokens; refresh flow on app start.
- Optimistic UI: cart edits; chat send.

## Error/Empty States
- Loading skeletons, empty feed, empty cart, upload validation errors, chat offline banner.

## Accessibility
- Text scaling, proper touch targets, VoiceOver labels on buttons/images.
