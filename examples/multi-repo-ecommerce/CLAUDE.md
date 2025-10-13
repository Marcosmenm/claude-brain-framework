# E-Commerce Platform - Context Engineering

**Multi-repository system: Backend + Web + Mobile architecture**

> This is an EXAMPLE showing how to use `CLAUDE_MD_MULTI_REPO_SYSTEM.md` template.
> In production, fill in actual details for your system.

## 🚨 CRITICAL WORKFLOW ENFORCEMENT

**CLAUDE: Automatically apply context engineering for ANY development request.**

### Automatic Behaviors
1. ✅ Check documentation automatically
2. ✅ Assess complexity
3. ✅ Generate PRP for complex work (>3 files or significant logic)
4. ✅ Follow established patterns
5. ✅ Suggest relevant agents
6. ✅ Update documentation

**User works naturally - methodology applies automatically.**

---

## 📋 PROJECT TYPE & CONTEXT

### Project Classification
**Primary Type:** Multi-Repository System

**Domain:** E-Commerce Platform

**Scale:** SMB / Growing Startup

**Organization:** Example E-Commerce Company

### Repository Structure

This is a **multi-repository system** containing 3 interconnected applications:

```
/ecommerce-platform/
├── backend/           → Node.js + Express + PostgreSQL
├── web-frontend/      → React + TypeScript
└── mobile-app/        → React Native
```

**IMPORTANT:** All repositories share the same business domain but serve different user types:
- **Backend**: RESTful API server for all frontends
- **Web Frontend**: Customer-facing web application for browsing and purchasing
- **Mobile App**: Native mobile experience for iOS and Android

### User Types & Access

**Customers (Web + Mobile):**
- **Users:** End customers browsing and purchasing products
- **Purpose:** Product discovery, cart management, checkout, order tracking
- **Authentication:** JWT tokens (email/password + OAuth social login)

**Admin Staff (Web Admin Panel - Future):**
- **Users:** Internal staff managing products, orders, customers
- **Purpose:** Product catalog management, order fulfillment, customer support
- **Authentication:** JWT with role-based access control

---

## 🛠️ TECHNOLOGY STACK

### Backend (backend/)

**Framework & Core:**
- **Express.js:** 4.18 (Node.js 18 LTS)
- **Architecture:** Layered (Controllers → Services → Repositories)
- **ORM/Database Access:** Prisma ORM
- **Database:** PostgreSQL 15
- **API Documentation:** Swagger/OpenAPI 3.0

**Key Dependencies:**
- `jsonwebtoken`: Authentication
- `bcrypt`: Password hashing
- `joi`: Request validation
- `stripe`: Payment processing

**Cloud/Infrastructure:**
- **Provider:** AWS
- **Services Used:**
  - S3: Product images storage
  - SES: Transactional emails
  - CloudFront: CDN for images

**Security:**
- **Authentication:** JWT tokens (HttpOnly cookies for web, token storage for mobile)
- **Authorization:** RBAC (customer, admin roles)
- **Secrets Management:** Environment variables (.env files, AWS Secrets Manager in production)

**Testing:**
- **Framework:** Jest + Supertest
- **Test DB:** PostgreSQL (Docker container for testing)

### Web Frontend (web-frontend/)

**Framework & Core:**
- **React:** 18.2 (TypeScript 5.2)
- **Build Tool:** Vite 4
- **State Management:** Zustand
- **Data Fetching:** TanStack Query (React Query)
- **Routing:** React Router 6

**UI Framework:**
- **Primary:** Tailwind CSS 3
- **Component Library:** shadcn/ui components

**Authentication:**
- **Provider:** Custom JWT implementation
- **Flow:** HttpOnly cookies + refresh token rotation

**Testing:**
- **Framework:** Vitest + React Testing Library
- **E2E:** Playwright

### Mobile App (mobile-app/)

**Framework & Core:**
- **Platform:** React Native 0.72
- **Framework:** Expo 49
- **Language:** TypeScript 5.2
- **Build System:** EAS Build

**Navigation:**
- **Library:** React Navigation 6

**State Management:**
- **Library:** Zustand (same as web)

**Platform-Specific:**
- **iOS:** Min version 14.0
- **Android:** Min SDK 23 (Android 6.0)
- **App Store Info:** com.example.ecommerce

---

## ⚙️ DEVELOPMENT COMMANDS

### Backend (backend/)

```bash
# Environment Setup
cd backend
npm install

# Development
npm run dev              # Runs on port 3001
npm run build

# Testing
npm test
npm run test:coverage

# Database
npx prisma migrate dev   # Run migrations
npx prisma db seed       # Seed database
```

### Web Frontend (web-frontend/)

```bash
# Environment Setup
cd web-frontend
npm install

# Development
npm run dev              # Runs on port 5173

# Build
npm run build
# Output: dist/

# Testing
npm test
npm run test:e2e
```

### Mobile App (mobile-app/)

```bash
# Environment Setup
cd mobile-app
npm install

# Development
npm start                # Start Expo dev server
npm run ios              # Run on iOS simulator
npm run android          # Run on Android emulator

# Build
eas build --platform ios
eas build --platform android

# Testing
npm test
```

### Validation (run after changes)

```bash
# Backend
cd backend && npm test && npm run build

# Web Frontend
cd web-frontend && npm test && npm run build

# Mobile
cd mobile-app && npm test
```

---

## 🏗️ PROJECT ARCHITECTURE

### Multi-Repository Overview

```
┌─────────────────────────────────────────────────────────────┐
│                    PRESENTATION LAYER                        │
├─────────────────────────┬───────────────────────────────────┤
│   Web Frontend          │   Mobile App                      │
│   React + TypeScript    │   React Native + Expo             │
│   For: Customers        │   For: Customers                  │
└─────────────────────────┴───────────────────────────────────┘
                             ↓
                      HTTP REST API (/api/v1/*)
                             ↓
┌─────────────────────────────────────────────────────────────┐
│                    APPLICATION LAYER                         │
│              Backend (Express.js)                            │
│              Layered Architecture                            │
│              Single API version for now                      │
└─────────────────────────────────────────────────────────────┘
                             ↓
                        Prisma ORM
                             ↓
┌─────────────────────────────────────────────────────────────┐
│                        DATA LAYER                            │
│                    PostgreSQL 15                             │
│              Normalized schema (products, orders, users)     │
└─────────────────────────────────────────────────────────────┘
```

### Directory Structure

**Backend:**
```
/backend/
├── src/
│   ├── controllers/     # Request handlers
│   ├── services/        # Business logic
│   ├── repositories/    # Data access
│   ├── middleware/      # Auth, validation, error handling
│   └── routes/          # API route definitions
├── prisma/              # Database schema
├── tests/
└── package.json
```

**Web Frontend:**
```
/web-frontend/
├── src/
│   ├── components/      # Reusable UI components
│   ├── pages/           # Page-level components
│   ├── api/             # API client
│   ├── stores/          # Zustand state stores
│   └── lib/             # Utilities
├── public/
└── package.json
```

**Mobile App:**
```
/mobile-app/
├── src/
│   ├── screens/         # App screens
│   ├── components/      # Reusable components
│   ├── navigation/      # Navigation setup
│   └── api/             # API client
├── assets/
└── package.json
```

---

## 🎯 DOMAIN KNOWLEDGE

### Business Domain

**Primary Business:** Online retail e-commerce platform selling consumer goods

**Core Business Entities:**
1. **Product** - Items for sale with SKU, price, inventory
2. **Category** - Product organization and navigation
3. **User** - Customer accounts with auth and profile
4. **Cart** - Shopping cart for adding products before checkout
5. **Order** - Completed purchases with payment and fulfillment status
6. **Payment** - Stripe payment processing and transaction records

### Critical Workflows

**Product Discovery & Purchase:**
- **Trigger:** Customer browses website or mobile app
- **Steps:** Browse categories → View product → Add to cart → Checkout → Payment → Order confirmation
- **Success Criteria:** Order created, payment processed, confirmation email sent
- **Involved Repositories:** All three (backend API, web UI, mobile UI)
- **Key Files:**
  - Backend: `src/controllers/products.controller.js`, `src/services/cart.service.js`, `src/services/orders.service.js`
  - Web: `src/pages/ProductPage.tsx`, `src/pages/Checkout.tsx`
  - Mobile: `src/screens/ProductScreen.tsx`, `src/screens/CheckoutScreen.tsx`

---

## 📚 DOCUMENTATION

### System Documentation
**Location:** `/.claude/documentation/`

**CLAUDE: ALWAYS check relevant documentation before implementation.**

**Quick Access:**
- **📑 Start Here:** [@.claude/documentation/DOCUMENTATION_INDEX.md](.claude/documentation/DOCUMENTATION_INDEX.md) - Complete documentation catalog
- **🏗️ Architecture:** [@.claude/documentation/Architecture/Multi_Repository_Architecture.md](.claude/documentation/Architecture/Multi_Repository_Architecture.md) - System overview

**Available Documentation:**

**Core Systems (Example - TODO in real project):**
- 📝 Authentication_System.md - JWT auth, social login, session management (TODO)
- 📝 Product_Catalog.md - Product management, categories, search (TODO)
- 📝 Shopping_Cart.md - Cart state, persistence, checkout (TODO)
- 📝 Order_Processing.md - Order creation, payment, fulfillment (TODO)

**Architecture (Example - TODO in real project):**
- 📝 Multi_Repository_Architecture.md - How the three repos coordinate (TODO)
- 📝 API_Design.md - REST conventions, versioning strategy (TODO)

**Workflows (Example - TODO in real project):**
- 📝 Purchase_Workflow.md - End-to-end purchase flow (TODO)

---

## 🔄 FEATURE DEVELOPMENT WORKFLOW

### Simple Changes (Single repo, <3 files)

1. **Check documentation:** Review relevant `@.claude/documentation/` files
2. **Identify repository:** Backend, web frontend, or mobile
3. **Implement following patterns:** Match existing code style
4. **Run validation:** Tests + build for affected repository
5. **Update docs if needed:** Document new behavior

### Complex Features (Multi-file, business logic, >1 repository)

1. **CLAUDE AUTO-GENERATES PRP** (Product Requirements Prompt)
   - Asks for ticket number (e.g., ECOM-XXX)
   - Creates `/.claude/prps/active/[TICKET]-[feature].md`
   - Documents requirements, acceptance criteria, affected repos

2. **Clarify business/technical decisions**
   - Which repositories affected (backend/web/mobile)?
   - API changes required?
   - Database schema changes?

3. **Implement systematically**
   - Backend first (API contracts)
   - Web/Mobile frontend integration
   - Update all repositories in sync

4. **Full validation**
   - Backend: `cd backend && npm test && npm run build`
   - Web: `cd web-frontend && npm test && npm run build`
   - Mobile: `cd mobile-app && npm test`

5. **Update documentation**
   - Add/update `@.claude/documentation/` files
   - Update CLAUDE.md if architecture changed
   - Document new API endpoints

### Multi-Repository Feature Coordination

**When feature spans multiple repos:**

1. **Backend changes first:**
   - Create/modify API endpoints
   - Update database schema
   - Deploy to staging

2. **Frontend integration (parallel for web + mobile):**
   - Update API clients
   - Add UI components
   - Test against staging backend

3. **Deployment sequence:**
   - Backend deployed first (backward compatible)
   - Web frontend deployed second
   - Mobile submitted to app stores

---

**Context Engineering Version:** 1.1.0
**Last Updated:** 2025-10-13
**Project Type:** Multi-Repository E-Commerce Platform
**Organization:** Example Company

---

**This is an EXAMPLE. Replace with your actual system details when applying to your project.**
