# 🚀 Smart Gowala (Khabani) – Enterprise Livestock Management System

> **Architecture Showcase** - A production-ready mobile application demonstrating clean architecture, multi-backend integration, and enterprise-scale state management for a comprehensive livestock management system.

---

## 🚀 Key Highlights

- **🗄️ Multi-Database Strategy** – Build-time configured, runtime-resolved backend selection (Firebase, PostgreSQL, Spring Boot) via Factory Pattern..
- **📝 Metadata-Driven Forms** – Dynamic UI engine that renders 90+ complex forms from JSON-like schemas, drastically reducing boilerplate.
- **🔐 Dynamic RBAC** – Granular, real-time permission system controlling route access and UI visibility.
- **📊 Centralized Pagination** – Generic data handling module for scalable list views and search.
- **🏗️ Clean Architecture** – Feature-first modular design ensuring separation of concerns and testability.
- **⚡ High Performance** – Lazy loading, state optimization, and efficient caching for 1000+ concurrent users.

---

## 🏗️ Project Architecture

The application is built using **Clean Architecture** principles organized into a **feature-first modular structure**. This ensures that business logic remains independent of the UI and database implementations.

### **Clean Architecture Layers**
<div align="center">
  
```
┌─────────────────────────────────────────────────────────┐
│                    PRESENTATION LAYER                   │
│  (MetadataDrivenForm, Dynamic Routing, RBAC Guards)     │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│                     DOMAIN LAYER                        │
│  (Business Entities, Repository Interfaces)             │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│                      DATA LAYER                         │
│  (Repositories, Datasources, Models for 3 DB Systems)   │
└─────────────────────────────────────────────────────────┘
```

</div>

---

## 🧱 SOLID Principles in Practice (Production Usage)

Smart Gowala (Khabani) — it is designed using **SOLID principles applied at scale**, ensuring long-term maintainability as features, users, and backends grow.

The following table maps each SOLID principle directly to **real architectural decisions implemented in this codebase**:

| SOLID Principle | Where It Lives in Smart Gowala |
|----------------|--------------------------------|
| **S — Single Responsibility** | Feature-first folders, isolated UseCases, dedicated Validators, UI-only Widgets |
| **O — Open/Closed** | Repository pattern with backend switching (Firebase / PostgreSQL / Spring Boot) and (Metadata-Driven Form Engine,and the Pagination System) |
| **L — Liskov Substitution** | Multiple repository implementations interchangeable without UI or domain changes |
| **I — Interface Segregation** | Small, module-specific repository contracts (Auth, Cattle, Finance, Reproduction) |
| **D — Dependency Inversion** | UseCases depend on abstractions, injected via Riverpod providers |

### Why This Matters

- **Backend migration readiness** → Firestore → REST API without rewriting business logic
- **Team scalability** → UI, Domain, and Data layers evolve independently
- **Testability** → Business rules tested without Flutter or database dependencies
- **Enterprise longevity** → Domain logic survives framework, database, and infrastructure changes

This approach ensures that **business rules remain stable**, while UI frameworks, databases, and delivery mechanisms stay replaceable — a core requirement for enterprise and long-lived products.

---


### **Feature-First Modular Structure**

```
lib/
├── core/                         # App-wide reusable infrastructure
│   ├── config/                  # Environment & app configuration
│   ├── constants/               # Global constants
│   ├── data/                    # Data layer (implementations)
│   │   ├── datasources/         # Firebase, PostgreSQL, API, Cache
│   │   ├── models/              # Source-specific DTOs
│   │   └── repositories/        # Concrete repository implementations
│   ├── domain/                  # Business logic (framework-agnostic)
│   │   ├── entities/            # Core business entities
│   │   └── repositories/        # Abstract contracts
│   ├── network/                 # API clients & database clients
│   ├── router/                  # Centralized navigation & transitions
│   ├── service/                 # Bootstrap, pagination, role providers
│   ├── theme/                   # App theming
│   ├── utils/                   # Responsive helpers & utilities
│   └── widgets/                 # Reusable UI components
│
├── features/                     # Independent feature modules
│   ├── auth/                    # Authentication & session handling
│   ├── dashboard/               # Role-based dashboards
│   ├── config/                  # User, role & permission management
│   ├── master_setup/            # Dynamic, metadata-driven setup
│   ├── home/                    # Entry navigation hub
│   ├── splash_screen/           # App bootstrap & preload logic
│   ├── ...                      # Additional enterprise features
│
└── gen/                          # Generated assets
                                   # Generated code/assets

```

---

## 🔧 Tech Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Frontend** | Flutter 3.x | Cross-platform UI development |
| **State Management** | Riverpod 2.x | Reactive state & dependency injection |
| **Navigation** | GoRouter | Declarative routing with guards |
| **Networking** | Dio | HTTP client with interceptors |
| **Database Strategy** | Firebase, PostgreSQL, Spring Boot | Multi-backend orchestration |
| **Local Storage** | Hive, SharedPreferences | Caching & session persistence |
| **Architecture** | Clean Architecture | Separation of concerns |

---

## 📸 Application Preview
- Available Soon

## 🗄️ Multi-Database Architecture

The application utilizes a **Bootstrap Factory** pattern to initialize the correct backend at runtime during app bootstrap, based on build-time environment configuration. This ensures that the UI layer interacts with a generic interface, regardless of the underlying database technology.

### **Repository Pattern: The Abstraction Layer**
The Data layer implements the Repository pattern to swap backends without affecting the Domain or Presentation layers.

```dart
// DOMAIN LAYER - Pure business contract
abstract class AuthRepository {
  Future<Either<AppError, UserEntity>> login(String email, String password);
  Future<Either<AppError, void>> logout();
}

// DATA LAYER - Swappable implementations
class FirebaseAuthRepository implements AuthRepository {
  // Firebase-specific implementation
}

class PostgresAuthRepository implements AuthRepository {
  // PostgreSQL-specific implementation
}

class SpringBootAuthRepository implements AuthRepository {
  // REST API implementation
}
```

### **Bootstrap Implementation**
```dart
// lib/main.dart
void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  
  // Initialize specific platform (e.g., Firebase)
  await Firebase.initializeApp(options: DefaultFirebaseOptions.currentPlatform);
  AppConfig.logBackendType();

  // Factory returns the correct implementation (Firebase, Postgres, etc.)
  final bootstrap = BootstrapFactory.createBootstrap();
  final isReady = await bootstrap.initialize();

  if (!isReady) {
    runApp(const ErrorApp());
    return;
  }

  runApp(const ProviderScope(child: MyApp()));
}
```

---

## 🔄 Backend Selection Strategy (Build-Time Configured, Runtime Resolved)

Smart Gowala supports multiple backend implementations (**Firebase**, **PostgreSQL**, **Spring Boot**) using a **controlled environment-based selection strategy**.

**Backend selection is:**

* **Configured at build-time** using `--dart-define`
* **Resolved at runtime** during application bootstrap
* **Immutable for the entire app lifecycle**

### Build Commands

```bash
# Firebase version
flutter build apk --dart-define=BACKEND_TYPE=firestore

# PostgreSQL version
flutter build apk --dart-define=BACKEND_TYPE=direct_postgres

# Spring Boot version
flutter build apk --dart-define=BACKEND_TYPE=spring_boot
```

At runtime, the application reads the environment value and injects the corresponding repository implementation via a **Bootstrap Factory**, while keeping the **UI** and **Domain** layers fully decoupled.

### This approach ensures:

* **Predictable production behavior**
* **Security and stability** (no live backend mutation)
* **Client-specific builds** without code changes
* **Strict adherence to Dependency Inversion**

> ⚠️ **Note:** Backend switching does **not** occur dynamically while the app is running.
> Each build is intentionally bound to a **single backend** for its entire lifecycle.

---
## 🎯 Key Technical Features

### 1. 📝 Metadata-Driven Form Engine

To avoid repetitive code for 90+ administrative forms, I engineered a dynamic form renderer. Instead of hardcoding widgets, the UI is generated from `FieldMetadata` schemas.

**Core Definition:**
```dart
// lib/features/cattle_management/presentation/widgets/metadata_driven_form.dart
enum FieldType { text, number, date, dropdown, image, textArea }

class FieldMetadata {
  final String key;
  final String label;
  final FieldType type;
  final bool required;
  final DropDownKeys? dropdownKey;
  final String? dependsOn; // Enables cascading logic
}

class MetadataDrivenForm extends ConsumerWidget {
  final List<FieldMetadata> fields;
  // Renders widgets based on field.type automatically
}
```

**Benefits:**
- **Drastic Code Reduction:** One widget handles text, dropdowns, dates, and image uploads.
- **Dynamic Validation:** Rules are applied based on metadata configuration.
- **Cascading Logic:** Fields can appear/disappear based on parent selection (e.g., `dependsOn`).

### 2. 🔐 Dynamic Role-Based Access Control (RBAC)

A centralized provider manages user permissions. Routes and widgets check permissions in real-time against the user's active role.

**Permission Provider:**
```dart
// lib/core/service/rbac/user_role_provider.dart
final userRolePermissionProvider = StateNotifierProvider<UserRPProvider, UserRoleAndPermissionsServiceState>((ref) {
  return UserRPProvider();
});

class UserRPProvider extends StateNotifier<UserRoleAndPermissionsServiceState> {
  // Checks single or multiple permissions
  bool isPermitted(dynamic permission) {
    if (permission is String) {
      return state.permissions.any((p) => p.apiKey == permission);
    } else if (permission is List<String>) {
      return permission.every((p) => state.permissions.any((perm) => perm.apiKey == p));
    }
    return false;
  }
}
```

**Usage:**
```dart
// Hiding a widget if the user lacks permission
Visibility(
  visible: ref.watch(userRolePermissionProvider.notifier).isPermitted('delete_cattle'),
  child: DeleteButton(),
);
```

### 3. 📊 Centralized Pagination & Tabulation

A generic, reusable pagination module handles data loading, search, and state management for all list views, ensuring consistency across the app.

**Pagination Logic:**
```dart
// lib/core/utils/pagination/pagination_providers.dart
final paginationProvider = StateNotifierProvider.family<PaginationNotifier, PaginationState, String>((ref, key) => 
  PaginationNotifier(const PaginationState())
);

class PaginationState {
  final int currentPage;
  final int rowsPerPage;
  final int totalRows;
  final List<dynamic> data;
  // Generic state holds any data type
}
```

**Features:**
- **Generic Search:** Filter any list based on defined fields.
- **Lazy Loading:** Efficiently handles large datasets (10,000+ records).
- **Reusable UI:** A single `PaginationBar` widget is utilized across all modules.

### 4. 🧭 Dynamic Routing

Instead of manually defining 30+ routes, the routing table is generated dynamically based on module metadata and user permissions. This keeps the router file clean and modular.

---

## 🚀 Development Example (Integrating Features)

Here is how the components come together in a feature module like "Master Setup":

```dart
class MasterSetupScreen extends ConsumerWidget {
  const MasterSetupScreen({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    // 1. Check Permissions using RBAC provider
    final authState = ref.watch(authProvider);
    if (!authState.isPermitted('access_master_setup')) {
      return const ForbiddenScreen();
    }

    // 2. Fetch Metadata (Defines form fields dynamically)
    final metadataAsync = ref.watch(formMetadataProvider('cattle_breeds'));

    return Scaffold(
      body: metadataAsync.when(
        data: (metadata) => Column(
          children: [
            // 3. Render Form using Metadata Engine
            Expanded(
              child: MetadataDrivenForm(fields: metadata.fields),
            ),
            // 4. Reuse Pagination Logic for history/logs
            const PaginationBar(key: 'breed_logs'),
          ],
        ),
        loading: () => const Loader(),
        error: (e, _) => ErrorText(e),
      ),
    );
  }
}
```

---

## 🎯 Architecture Decisions & Trade-offs

### **Why Clean Architecture?**
**Pros:**
- **Framework Independence:** Business logic survives framework changes (Flutter → React Native → Web).
- **Testability:** Business logic is testable without Flutter dependencies.
- **Scalability:** Independent team scaling (Domain team, UI team, Data team).

**Cons:**
- Initial setup complexity.
- More boilerplate code compared to simple MVC.

### **Why Metadata-Driven UI?**
- **Agility:** Business requirements for form changes happen frequently. Updating metadata is faster than a code deploy.
- **Consistency:** Ensures all forms follow the same validation, styling rules automatically.

### **Why Riverpod?**
- **Compile-Time Safety:** Catches provider dependency errors during compilation.
- **Testability:** Easy to override providers for unit/widget testing without complex setup.

---

## 🧪 Testing Strategy

Comprehensive testing ensures reliability across the clean architecture layers.

### **Unit Tests (Domain Layer)**
Testing pure business logic without Flutter.
```dart
test('User entity validation', () {
  final user = UserEntity(id: '1', email: 'test@example.com', roles: [RoleEntity.admin()]);
  expect(user.isAdmin, true);
});
```

### **Integration Tests (Data Layer)**
Testing repository implementations.
```dart
test('PostgresAuthRepository login', () async {
  final repository = PostgresAuthRepository(dataSource: mockPostgresDataSource, mapper: UserMapper());
  final result = await repository.login('test@example.com', 'password');
  expect(result.isRight(), true);
});
```

---

## 🏆 Skills Demonstrated

| Category | Specific Skills |
|----------|----------------|
| **Flutter Expertise** | Riverpod, Custom Painters, Animations, Performance Optimization |
| **Architecture** | Clean Architecture, Repository Pattern, Multi-Tier Design |
| **Backend Integration** | Firebase, PostgreSQL, REST APIs, WebSockets |
| **State Management** | Complex State Orchestration, Side Effects, Persistence |
| **Database Design** | Schema Design, Optimization, Migration Strategies |
| **Testing** | Unit, Integration, Widget Tests |

---

## 👨‍💻 Author

**Returaj**  
**Mobile Software Engineer** focused on **scalable Flutter architecture, multi-backend systems, and long-lived business logic.**

---

## ⚠️ Professional Disclosure

> **Confidentiality Notice**: This project represents architectural patterns and engineering decisions developed during professional work.  
>   
> **Confidential Information**:  
> - Company-specific business logic has been abstracted.  
> - Proprietary algorithms have been replaced with generic implementations.  
> - Sensitive data models have been sanitized.  
>   
> **What's Shown**:  
> - Clean Architecture implementation.  
> - Multi-database strategy.  
> - Metadata-driven form engine.  
> - Dynamic RBAC patterns.
>   
> **Intellectual Property**: All architectural patterns and code organization demonstrated are original work. Database schemas, business models, and proprietary algorithms remain confidential property of One Direction Companies Limited.


---


## 📞 Let's Connect

**I'm actively seeking Flutter roles where I can grow as an engineer while contributing at scale, including opportunities to:**
- Learn from experienced engineers and evolve my approach to large-scale mobile architecture
- Contribute to designing scalable, maintainable Flutter systems in real-world products
- Deepen my understanding of clean architecture, backend integration, and performance optimization
- Collaborate closely with product, backend, and design teams to solve complex business problems
- Gradually take on more ownership and technical responsibility while mentoring where appropriate

**Available for:**
- Full-time, part-time, or contract senior/mid-level Flutter roles
- Architecture consulting and technical due diligence
- Legacy application modernization
- Performance optimization projects

---

<div align="center">

*"Building scalable enterprise solutions with robust architecture and dynamic user experiences."*

</div>
