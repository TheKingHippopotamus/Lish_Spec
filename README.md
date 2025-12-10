# LISH MVP Specifications

This repository contains the complete MVP specifications for LISH, an iOS-first sustainable fashion marketplace.

## Documentation Structure

### Core Specifications

- **[00_overview.md](mvp_specs/00_overview.md)** - MVP Overview
  - Project goals and scope
  - In-scope and out-of-scope features
  - Key assumptions and platform decisions

- **[01_architecture.md](mvp_specs/01_architecture.md)** - Architecture
  - System architecture diagram
  - Frontend, backend, and data layer design
  - Media handling, chat, payments, and notifications architecture

- **[02_data_models.md](mvp_specs/02_data_models.md)** - Data Models
  - MongoDB schema definitions
  - Collections: users, products, mediaAssets, carts, orders, chatThreads, chatMessages
  - Indexes and data relationships

- **[03_backend.md](mvp_specs/03_backend.md)** - Backend API
  - Node.js/TypeScript backend stack
  - API endpoints for auth, catalog, media, cart, orders, chat, and admin
  - Validation, error handling, and background jobs

- **[04_mobile.md](mvp_specs/04_mobile.md)** - Mobile App
  - React Native implementation details
  - Screen flows and user journeys
  - Component library and state management
  - Error handling and accessibility

### Infrastructure & Operations

- **[05_infra_ops.md](mvp_specs/05_infra_ops.md)** - Infrastructure & Operations
  - AWS infrastructure setup
  - CI/CD pipeline configuration
  - Networking, security, and observability
  - Storage and deployment strategies

- **[06_security_quality.md](mvp_specs/06_security_quality.md)** - Security, Quality & Performance
  - Security best practices
  - Testing strategy (unit, integration, E2E)
  - Performance optimization
  - Reliability and error handling

### Planning & Execution

- **[07_delivery_plan.md](mvp_specs/07_delivery_plan.md)** - Delivery Plan
  - 7-week MVP delivery timeline
  - Weekly milestones and checkpoints
  - Key approvals and decision points

- **[08_stack_options.md](mvp_specs/08_stack_options.md)** - Stack Options
  - Technology stack comparison
  - Frontend, backend, database, and infrastructure options
  - Recommendation pathways (speed-first vs control-first)

- **[09_execution_plan_aws.md](mvp_specs/09_execution_plan_aws.md)** - Execution Plan (AWS)
  - Detailed week-by-week plan for AWS-based implementation
  - Infrastructure as Code setup
  - Backend and mobile app development phases

- **[10_execution_plan_firebase.md](mvp_specs/10_execution_plan_firebase.md)** - Execution Plan (Firebase)
  - Detailed week-by-week plan for Firebase-based implementation
  - Firebase services configuration
  - Rapid development approach

## Quick Start

1. Start with **[00_overview.md](mvp_specs/00_overview.md)** to understand the project scope
2. Review **[01_architecture.md](mvp_specs/01_architecture.md)** for system design
3. Check **[08_stack_options.md](mvp_specs/08_stack_options.md)** to choose your tech stack
4. Follow the appropriate execution plan:
   - **[09_execution_plan_aws.md](mvp_specs/09_execution_plan_aws.md)** for AWS implementation
   - **[10_execution_plan_firebase.md](mvp_specs/10_execution_plan_firebase.md)** for Firebase implementation

## Key Features (MVP)

- **Authentication**: Email/password and Apple ID login
- **Product Feed**: Infinite scroll with filters (category, size, gender, condition, material, style)
- **Product Upload**: Simple seller uploads with up to 5 photos
- **Shopping Cart**: Add to cart and checkout flow
- **Payments**: Apple Pay integration via Stripe
- **Chat**: Admin-mediated chat system (buyer ↔ admin ↔ seller)
- **Orders**: Order creation, tracking, and status management
- **Notifications**: In-app notifications with optional push support

## Platform

- **Primary**: iOS (React Native)
- **Future**: Android support planned

