# Architecture Overview

This document describes the reference architecture for the **Business** applications and commerce platform (`apps shopping`).

---

## System Layers

```
+-------------------------------------------------------------------+
|                     Client & Presentation Layer                   |
|        Web Storefront / Mobile Shopping App / Admin Portal        |
+---------------------------------+---------------------------------+
                                  |
                                  v
+-------------------------------------------------------------------+
|                        API & Gateway Layer                        |
|           REST / GraphQL API, Auth, Rate Limiting, Webhooks       |
+----------------+----------------+----------------+----------------+
                 |                                 |
                 v                                 v
+---------------------------------+ +-------------------------------+
|      Core Business Engine       | |    External Integrations      |
| - Catalog & Product Discovery   | | - Stripe Payments & Billing   |
| - Cart, Orders & Fulfillment    | | - Affiliate Network Tracking  |
| - User Profiles & Wishlists     | | - Email & Push Notifications  |
+----------------+----------------+ +-------------------------------+
                 |
                 v
+-------------------------------------------------------------------+
|                       Data & Storage Layer                        |
|      PostgreSQL (Primary DB) / Redis (Cache & Sessions) / CDN     |
+-------------------------------------------------------------------+
```

---

## Component Responsibilities

### 1. Front-End Layer (Client Applications)
- **Shopping App & Storefront:** Responsive web and mobile interfaces focused on fast product discovery, search filtering, cart management, and high-conversion checkout flows.
- **Attribution & Analytics:** Captures referral parameters, UTM tags, and affiliate link redirects cleanly while respecting user privacy.

### 2. Back-End Layer (Core Domain Logic)
- **Catalog & Inventory Service:** Manages product listings, categories, pricing tiers, SKU availability, and merchant feeds.
- **Order & Subscription Management:** Orchestrates shopping carts, tax/shipping calculation, order state transitions, and digital receipts.
- **Identity & Access Control:** Role-based access control (RBAC) separating customers, affiliate partners, and system administrators.

### 3. Payment & Monetization Layer
- **Stripe Integration:**
  - Uses `PaymentIntents` and Stripe Checkout for PCI-DSS compliant card and wallet payments.
  - Processes asynchronous webhook events (`payment_intent.succeeded`, `charge.refunded`, `customer.subscription.updated`) with idempotency keys and signature verification (`STRIPE_WEBHOOK_SECRET`).
- **Affiliate Attribution Engine:**
  - Tracks outbound and inbound partner referrals mapped to networks documented in [`Affiliate-Marketing-Vault/`](./Affiliate-Marketing-Vault/Index.md).

### 4. Data & Infrastructure Layer
- **Primary Database:** Relational storage (PostgreSQL) with strict transactional integrity for orders, ledgers, and inventory.
- **Caching & Queues:** Redis for session state, rate limiting, catalog caching, and background webhook processing.
