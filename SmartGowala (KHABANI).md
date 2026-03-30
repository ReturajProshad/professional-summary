# 🌾 AgroTech (Previous Smart Gowala (Khabani)) — Enterprise Agricultural ERP System 

> **Full-Stack ERP Architecture Showcase** — A production-grade, multi-tenant agricultural management platform engineered with Clean Architecture, microservice-ready design, and metadata-driven UI — covering livestock, poultry, fisheries, and crop sectors across a single unified system.

---

<div align="center">

**Flutter · Firebase · PostgreSQL · Spring Boot · Microservices · Clean Architecture · RBAC · ERP**

`Android` `iOS` `Desktop` `Web` · `BN / EN` · `Multi-Backend` · `Multi-Tenant`

</div>

---

## 🎯 What Is AgroTech?

**AgroTech** is a comprehensive **Agricultural ERP (Enterprise Resource Planning)** system designed to digitize and automate every operational layer of modern farming enterprises — from livestock health tracking and milk production to financial accounting, procurement, HR, and real-time smart alerts.

This is not a simple CRUD app. AgroTech mirrors the complexity of commercial ERP systems (SAP, Oracle Agri) but is engineered for the ground realities of South Asian agricultural businesses — multilingual, offline-resilient, and deployable across Firebase, PostgreSQL, or a full Spring Boot microservice stack.

### 🌐 Agricultural Sectors Covered

| Sector | Coverage |
|--------|----------|
| 🐄 **Livestock** | Cattle, Buffalo, Camel, Horse, Goat, Sheep |
| 🐔 **Poultry** | Chicken, Duck, Turkey |
| 🐟 **Fisheries** | Sweet Water Fish, Sea Fish |
| 🌱 **Agro** | Crop, Vegetable, Fruit, Spices |

---

## 🚀 Engineering Highlights

- **🏗️ Clean Architecture** — Strict separation across Presentation, Domain, and Data layers. Business logic is completely framework-agnostic and database-agnostic.
- **🗄️ Multi-Backend Strategy** — Build-time configured, runtime-resolved backend selection: Firebase Firestore, PostgreSQL (direct), or Spring Boot Microservice API — without touching UI or domain code.
- **📝 Metadata-Driven Form Engine** — A single dynamic renderer handles **90+ complex forms** from JSON-like schema definitions, eliminating repetitive widget code entirely.
- **🔐 Dynamic RBAC** — Granular, real-time Role-Based Access Control with **10 distinct user roles**, controlling both route access and fine-grained UI element visibility.
- **📊 Centralized Pagination & Search** — Generic, reusable data module serving **30+ list views** with type-safe search, lazy loading, and state management.
- **📦 Full ERP Module Suite** — 14 integrated modules: Master Setup, Cattle Management, Reproduction, Health, Production, Feed & Nutrition, Buy & Sell, Inventory, Budget, Finance & Accounts (with GL), HR & Admin, Reports, and Smart Alerts.
- **🔔 Smart Alert Engine** — Push notifications for critical farm events: AI due, vaccination due, calving calendar, missed heat detection, and daily entry reminders.

---

## 🏗️ System Architecture

### Clean Architecture Layers

```
┌──────────────────────────────────────────────────────────────────┐
│                      PRESENTATION LAYER                          │
│   Flutter UI · GoRouter Navigation · RBAC Guards · Form Engine   │
└──────────────────────────────────────────────────────────────────┘
                               │
                               ▼
┌──────────────────────────────────────────────────────────────────┐
│                        DOMAIN LAYER                              │
│   Business Entities · Repository Interfaces · Pure Dart Logic    │
└──────────────────────────────────────────────────────────────────┘
                               │
                               ▼
┌──────────────────────────────────────────────────────────────────┐
│                         DATA LAYER                               │
│   Firebase / PostgreSQL / Spring Boot · DTOs · Cache · Mappers   │
└──────────────────────────────────────────────────────────────────┘
```

### Multi-Backend Strategy (Build-Time Configured, Runtime Resolved)

AgroTech supports three fully interchangeable backend implementations through a **Bootstrap Factory** pattern. Backend selection is immutable per build — ensuring production predictability and strict Dependency Inversion.

```
┌──────────────────────┐     ┌──────────────────────┐     ┌──────────────────────┐
│   Release Version 1a │     │   Release Version 1b  │     │   Release Version 2  │
│                      │     │                       │     │                      │
│  Flutter App         │     │  Flutter App          │     │  Flutter App         │
│       +              │     │       +               │     │       +              │
│  Firebase Firestore  │     │  PostgreSQL (Direct)  │     │  Spring Boot API     │
│  (Cloud NoSQL DB)    │     │  (On-premise SQL DB)  │     │  + PostgreSQL DB     │
│                      │     │                       │     │  (Microservice Stack)│
└──────────────────────┘     └──────────────────────┘     └──────────────────────┘
```

```bash
# Firebase deployment
flutter build apk --dart-define=BACKEND_TYPE=firestore

# Direct PostgreSQL deployment
flutter build apk --dart-define=BACKEND_TYPE=direct_postgres

# Spring Boot microservice deployment
flutter build apk --dart-define=BACKEND_TYPE=spring_boot
```

### Repository Pattern — The Abstraction Core

```dart
// DOMAIN LAYER — Pure contract, zero dependencies
abstract class AuthRepository {
  Future<Either<AppError, UserEntity>> login(String email, String password);
  Future<Either<AppError, void>> logout();
}

// DATA LAYER — Three swappable implementations
class FirebaseAuthRepository   implements AuthRepository { /* Firestore */ }
class PostgresAuthRepository   implements AuthRepository { /* Direct SQL */ }
class SpringBootAuthRepository implements AuthRepository { /* REST API  */ }
```

The UI and Domain layers never know which backend is running. Switching from Firebase to a microservice requires **zero changes** in business logic.

---

## 🔧 Technology Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Frontend** | Flutter 3.x | Cross-platform UI (Android, iOS, Desktop, Web) |
| **State Management** | Riverpod 2.x | Reactive state & compile-time safe DI |
| **Navigation** | GoRouter | Declarative routing with RBAC guards |
| **Backend v1a** | Firebase Firestore | NoSQL cloud DB, real-time sync, auth |
| **Backend v1b** | PostgreSQL | Relational SQL, on-premise, auto-table creation |
| **Backend v2** | Spring Boot + PostgreSQL | JWT auth, multi-tenant, CRUD microservices |
| **Cloud Functions** | Firebase Functions | Business logic, report calculations |
| **Notifications** | Firebase Cloud Messaging | Smart push alerts |
| **Local Cache** | Hive + SharedPreferences | Dropdown caching, session persistence |
| **Architecture** | Clean Architecture + SOLID | Long-lived, testable, framework-independent |
| **Language** | Dart, Java | App + backend services |

---

## 🧱 SOLID Principles at ERP Scale

| Principle | Implementation in AgroTech |
|-----------|---------------------------|
| **S — Single Responsibility** | Feature-first folders, isolated repositories per domain (Cattle, Reproduction, Finance, Health) |
| **O — Open/Closed** | Metadata-Driven Form Engine and Pagination System are extended via configuration — never modified |
| **L — Liskov Substitution** | Firebase, PostgreSQL, and Spring Boot repositories are fully interchangeable without breaking domain or UI |
| **I — Interface Segregation** | Small, module-specific contracts: `CattleRepo`, `ReproductionRepo`, `FinanceRepo` — never one giant interface |
| **D — Dependency Inversion** | All business logic depends on abstractions, injected via Riverpod providers at runtime |

---

## 📁 Project Structure

```
lib/
├── core/                            # App-wide infrastructure
│   ├── config/                      # Environment & backend configuration
│   ├── constants/                   # App-wide constants & strings
│   ├── data/
│   │   ├── datasources/
│   │   │   ├── api/                 # REST API clients
│   │   │   ├── cache/               # Dropdown & entity caching (Hive)
│   │   │   ├── firebase/            # Firestore data sources
│   │   │   └── postgres/            # PostgreSQL data sources
│   │   ├── models/
│   │   │   ├── firebase/            # Firestore-specific DTOs
│   │   │   ├── pgres/               # PostgreSQL DTOs
│   │   │   └── spring/              # Spring Boot DTOs
│   │   └── repositories/            # Concrete implementations
│   │       ├── auth/                # Firebase / Postgres / Spring Boot auth
│   │       ├── cattle/              # Cattle data operations
│   │       ├── reproduction/        # AI, HD, PD, Calving
│   │       ├── health_record/       # Events & Treatment records
│   │       ├── milk_production/     # Daily milk records
│   │       ├── feed_item_repo/      # Feed & nutrition data
│   │       ├── dropdown/            # Cached dropdown lookups
│   │       └── ...                  # 14+ domain repositories
│   ├── domain/
│   │   ├── entities/                # 18+ pure business entities
│   │   ├── mappers/                 # DTO ↔ Entity conversion
│   │   └── repositories/            # Abstract contracts per domain
│   ├── form/                        # Metadata-Driven Form Engine core
│   ├── internal/                    # Bootstrap factory & schema management
│   ├── router/                      # GoRouter + RBAC route guards
│   ├── service/                     # Providers: bootstrap, RBAC, dropdowns
│   └── utils/                       # Pagination, date pickers, responsive helpers
│
├── features/                        # 14 independent ERP modules
│   ├── auth/                        # Login, registration, session management
│   ├── dashboard/                   # Role-based KPI dashboard
│   ├── config/                      # Users, roles, permissions management
│   ├── master_setup/                # 30+ master data forms (metadata-driven)
│   ├── cattle_management/           # Cattle profiles, history, lifetime view
│   ├── reproduction/                # HD → AI → PD → Calving lifecycle
│   ├── health_checkup/              # Events, treatment, disease tracking
│   ├── production/                  # Daily milk records & stock
│   ├── feed_and_nutrition/          # Feed issuance, recipes, history
│   ├── home/                        # Navigation hub
│   └── splash_screen/               # Bootstrap & preload logic
│
└── gen/                             # Generated assets
```

---

## 🎯 Key Technical Features

### 1. 📝 Metadata-Driven Form Engine

The most powerful architectural decision in AgroTech. Instead of building each of the **90+ complex forms** manually, a dynamic rendering engine reads `FieldMetadata` schemas and generates fully validated, styled, and connected UI automatically.

```dart
enum FieldType { text, number, date, dropdown, image, textArea }

class FieldMetadata {
  final String key;
  final String label;
  final FieldType type;
  final bool required;
  final DropDownKeys? dropdownKey;
  final String? dependsOn;       // Cascading field logic
  final ValidationRule? rule;    // Dynamic validation per field
}

// One widget renders all 90+ forms — text, dropdowns, dates, image uploads
class MetadataDrivenForm extends ConsumerWidget {
  final List<FieldMetadata> fields;
  // Auto-renders based on field.type, applies validation, handles cascades
}
```

**Real Impact:** Adding a new form (e.g., a new master setup entity) requires **only schema definition** — no new widgets, no new validation logic, no new state management code.

---

### 2. 🔐 Dynamic RBAC — 10-Role Permission System

AgroTech supports **10 distinct user roles** across the farm organizational hierarchy. Every route and UI element is permission-gated in real time.

**User Roles:** Super Admin · Farm Manager · Milk Supervisor · Vet Officer · AI Technician · Sales Executive · Purchase Executive · Finance Officer · Field Staff · Report Viewer

```dart
final userRolePermissionProvider =
    StateNotifierProvider<UserRPProvider, UserRoleAndPermissionsServiceState>((ref) {
  return UserRPProvider();
});

class UserRPProvider extends StateNotifier<UserRoleAndPermissionsServiceState> {
  bool isPermitted(dynamic permission) {
    if (permission is String)
      return state.permissions.any((p) => p.apiKey == permission);
    if (permission is List<String>)
      return permission.every((p) => state.permissions.any((perm) => perm.apiKey == p));
    return false;
  }
}

// Usage — widget visibility controlled by permission
Visibility(
  visible: ref.watch(userRolePermissionProvider.notifier).isPermitted('delete_cattle'),
  child: DeleteButton(),
);
```

---

### 3. 📊 Centralized Pagination & Search Engine

One generic module powers **all list views** across the system — consistent UX, consistent performance, zero duplication.

```dart
final paginationProvider = StateNotifierProvider.family<
    PaginationNotifier, PaginationState, String>((ref, key) =>
  PaginationNotifier(const PaginationState()));

class PaginationState {
  final int currentPage;
  final int rowsPerPage;
  final int totalRows;
  final List<dynamic> data;      // Type-generic — works for any entity
  final String searchQuery;
}
```

**Handles:** lazy loading · field-aware search · 10,000+ record datasets · reusable `PaginationBar` widget across all 30+ modules.

---

### 4. 💰 Integrated Finance & General Ledger Engine

AgroTech implements a **double-entry accounting system** directly within the app — an ERP-grade financial engine that auto-posts transactions to the General Ledger.

```
Sales Transaction    ──► Auto-post ──► General Ledger (Debit/Credit)
Purchase Transaction ──► Auto-post ──► General Ledger (Debit/Credit)
Expense Transaction  ──► Auto-post ──► General Ledger (Debit/Credit)
Income Transaction   ──► Auto-post ──► General Ledger (Debit/Credit)
Journal Voucher      ──► Auto-post ──► General Ledger (manual adjustments)
```

Supported reports generated from the GL: Supplier Ledger · Customer Ledger · Cash/Bank Ledger · Profit & Loss (Monthly/Yearly) — all derived **automatically** from the centralized ledger, with no manual report entry.

---

### 5. 🐄 Full Livestock Lifecycle Tracking

AgroTech models the **complete biological and economic lifecycle** of every animal in the herd:

```
[Purchase / Born on Farm]
        │
        ▼
[Cattle Basic Profile]  ← Tag No, Breed, Gender, DoB, Acquisition, Purpose
        │
        ├──► [Reproduction Lifecycle]
        │         Heat Detection → Artificial Insemination → Pregnancy Diagnosis → Calving
        │         (With auto-calculated pregnancy stages, expected calving dates)
        │
        ├──► [Health & Wellness]
        │         Event Record → Treatment Record
        │         (Disease tracking, vaccination, surgery, quarantine)
        │
        ├──► [Daily Milk Production]
        │         Morning / Afternoon / Evening / Whole Day sessions
        │         Milk stock auto-calculated: Total Production – Sales
        │
        ├──► [Feed & Nutrition]
        │         Daily feed issuance per cow, feed cost tracking, recipe management
        │
        ├──► [Weight Monitoring]
        │         Monthly weight records, growth tracking
        │
        └──► [Revenue & Expenditure]
                  Profit per cow, lifetime financial summary
```

The **Cattle Details** view provides a unified lifetime history — reproduction, milk production, health events, feed consumption, and financials — in a single screen per animal.

---

### 6. 📈 Dashboard KPI Engine

A role-sensitive dashboard surfaces real-time operational intelligence across 7 KPI sections:

| Dashboard Section | Key Metrics |
|-------------------|-------------|
| 🔴 **High Priority Alerts** | Vaccination Due, AI Due Today, Sick Cattle, Pending Entry, Calving Due |
| 💰 **Financial Summary** | Net Profit, Monthly Sale/Expense, Pending Due, Cash in Hand |
| 🐄 **Herd Inventory** | Total Cattle, Lactating, Pregnant, Dry, Calves/Heifers/Bulls |
| 🥛 **Production & Efficiency** | Today's Milk (L), Avg per Cow, 7-Day Total, Milk Stock, Monthly Production |
| 🔬 **Reproduction & Health** | AI Success Rate %, PD Due, Heat Due, Sick Count |
| 🌾 **Feed & Nutrition** | Today's Feed Cost, Feed Efficiency (L/Kg), Deworming Due, Total Consumed |
| 📊 **Smart Insights** | Top 5 Producers, Least Producers, High Risk Cows, Milk Sale Trend, Profit Trend |

---

### 7. 🔔 Smart Alert & Reminder System

AgroTech proactively prevents operational failures through automated push notifications:

- **AI Due Today/Tomorrow** — Prevents missed insemination windows
- **Vaccination Due** — Tracks herd vaccination schedules
- **Pregnancy Check Due** — Ensures no PD is overlooked
- **Expected Calving ±7 Days** — Prepares farm staff in advance
- **Missed Heat Detection** — Flags cows showing no heat cycle
- **Daily Entry Reminders** — Ensures data completeness

---

## 📋 Master Setup — 30+ Configurable Entities

AgroTech's master data layer covers every configuration dimension an agricultural ERP requires:

| Category | Entities |
|----------|----------|
| **Farm** | Farm Profile, Branch |
| **People** | Employee, Customer, Supplier, Supplier Type |
| **Livestock** | Breed, Origin, Group, Birth Type, Birth Status, Health Status |
| **Reproduction** | Heat Type, Breeding Symptoms |
| **Medical** | Diseases & Symptoms, Disease Type, Medicine, Vaccine, Dose, Route |
| **Production** | Milk Production Type, Feed Item, Feed Type, Unit |
| **Events** | Event Type, Event Disposal Type, Event Quarter |
| **Finance** | Expense Head, Expense Sub Head, Income Head, Income Source, GL Head, GL Transaction Type, Payment Type, Sale Type, Purchase Type, Payment Status |

All master entities use the **Metadata-Driven Form Engine** — consistent validation, consistent UI, zero boilerplate per entity.

---

## 📊 Reports Engine — 16+ Business Reports

| Report | Data Source |
|--------|-------------|
| D/M/Y/Lifetime Milk History (per cow / farm) | Production Table |
| Top 10 Milk Producers | Production Aggregation |
| Pregnant List + Calving Calendar | Reproduction Table |
| AI Success Rate % | AI + PD Tables |
| Cattle Age-wise Report | Cattle Profile |
| Weight History | Monthly Weight Table |
| Feed Consumption Report | Feed Issue Table |
| Profit per Cow Report | GL Aggregation |
| Cattle Sale Report | Sales Transaction Table |
| Customer-wise Milk Sales | Sales + Customer Tables |
| Expense Head-wise Report | Expense Transaction Table |
| Stock Valuation (Cattle + Feed + Milk) | Multi-table Aggregation |
| Supplier Ledger | General Ledger |
| Customer Ledger | General Ledger |
| Cash/Bank Ledger | General Ledger |
| Profit & Loss (Monthly/Yearly) | General Ledger |

---

## 🧪 Testing Strategy

```dart
// Domain Layer — Pure business logic, no Flutter dependency
test('Cattle entity reproduction stage', () {
  final cattle = CattleEntity(tagNo: 'T001', gender: Gender.female);
  expect(cattle.isEligibleForAI, true);
});

// Data Layer — Repository integration
test('PostgresCattleRepo fetch active herd', () async {
  final repo = PostgresCattleRepo(dataSource: mockDataSource, mapper: CattleMapper());
  final result = await repo.getActiveCattle();
  expect(result.isRight(), true);
  expect(result.getOrElse(() => []).isNotEmpty, true);
});

// Presentation Layer — RBAC permission check
test('VetOfficer cannot access finance module', () {
  final provider = UserRPProvider()..setRole(Role.vetOfficer);
  expect(provider.isPermitted('access_finance'), false);
});
```

---

## 🏆 Architecture Decisions & Trade-offs

### Why Clean Architecture for an Agricultural App?

Most farm management apps are built as simple CRUD systems. AgroTech is engineered as a **long-lived ERP platform** — which demands:

- **Business logic that survives framework changes** (Flutter → Web → desktop)
- **Backend migration without rewriting features** (Firebase → REST API → microservices)
- **Independent team scaling** — UI, Domain, and Data evolve separately
- **Testable business rules** — domain logic verifiable without Flutter or a database

### Why Metadata-Driven Forms?

Agricultural ERP systems have inherently volatile form requirements — regulations change, new livestock categories are added, financial fields evolve. The metadata engine ensures:

- **Form changes are configuration, not code** — no deploy needed for field additions
- **Automatic consistency** — every form inherits the same validation, styling, and UX rules
- **Near-zero UI maintenance cost** for 90+ forms

### Why Multi-Backend Strategy?

Different clients have different infrastructure realities:
- Small farms → Firebase (zero ops, instant setup)
- Mid-size enterprises → Direct PostgreSQL (data control, performance)
- Large enterprises → Spring Boot microservices (multi-tenancy, scalability, JWT)

One codebase serves all three without compromise.

---

## 🏅 Skills Demonstrated

| Domain | Specific Capabilities |
|--------|-----------------------|
| **Flutter Engineering** | Riverpod 2.x, Custom Painters, GoRouter, Performance Optimization, Multi-platform (Android/iOS/Desktop/Web) |
| **ERP Architecture** | Double-entry GL, RBAC, Multi-tenant design, Module federation |
| **Clean Architecture** | Repository Pattern, Entity/DTO separation, Dependency Inversion at scale |
| **Backend Integration** | Firebase Firestore, PostgreSQL, Spring Boot REST APIs, JWT Auth |
| **State Management** | Complex async state, Side effects, Caching strategies, Provider scoping |
| **Database Design** | Schema design, Auto-migration, Multi-backend abstraction |
| **Form Engineering** | Dynamic metadata-driven UI, Cascading dropdowns, Runtime validation |
| **Financial Systems** | Sales/Purchase/Expense transactions, Auto GL posting, Ledger derivation |
| **Testing** | Unit (Domain), Integration (Data), Widget (Presentation) |

---

## 👨‍💻 Author

**Returaj Proshad Shornocar**
**Flutter & Mobile Software Engineer** — specializing in scalable ERP architecture, multi-backend Flutter systems, and enterprise-grade clean architecture for long-lived business applications.

📧 returajsumon0808@gmail.com
🔗 [LinkedIn](https://www.linkedin.com/in/returaj-proshad) · [GitHub](https://github.com/ReturajProshad)

---

## ⚠️ Professional Disclosure

> **Confidentiality Notice:** This project represents architectural patterns and engineering decisions developed during professional engagement.
>
> - Company-specific business logic has been abstracted
> - Proprietary algorithms replaced with generic implementations
> - Sensitive data models sanitized
>
> **What's Demonstrated:** Clean Architecture implementation · Multi-database strategy · Metadata-driven form engine · Dynamic RBAC · Full ERP module design · Double-entry GL engine
>
> **Intellectual Property:** All architectural patterns and code organization are original work. Database schemas, business models, and proprietary algorithms remain confidential property of **One Direction Companies Limited**.

---

<div align="center">

*"Designing systems that outlive frameworks, databases, and infrastructure changes — because great architecture is the only form of future-proofing."*

</div>
