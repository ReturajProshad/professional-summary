# 📘 Shimana – Large-scale Enterprise Application

> A feature-rich, modular Flutter application built for **One Direction Companies Limited (ODCL)** demonstrating professional mobile development practices at scale.

## 🚀 Key Highlights

- **🧩 24 Independent Modules** – Feature-first modular architecture for maximum scalability
- **🔑 Secure Authentication** – Role-based access control with Dio interceptors for token management
- **📦 Asset Management Module** – Lazy loading, advanced filtering, and pagination
- **🌍 Full Localization** – English (EN), Bangla (BN), and French (FR) support
- **🛠 Spring Boot Integration** – RESTful API communication with secure backend
- **🎨 Smooth UI/UX** – Custom widgets, Flutter animations, and consistent theming
- **⚡ Performance-focused** – Optimized rebuilds and efficient data loading

## 🏗️ Project Architecture

The application follows a **feature-first clean architecture** pattern for maintainability and scalability:

```
lib/
├── core/                    # Reusable app-wide utilities
│   ├── constants/          # App constants and configurations
│   ├── theme/              # Theme data and styling
│   ├── l10n/               # Localization helpers
│   ├── services/           # Core services (API, auth, storage)
│   └── utils/              # Shared utilities
│       ├── widgets/        # Reusable custom widgets
│       ├── dialogs/        # Common dialog components
│       ├── slices/         # State management slices
│       └── models/         # Shared data models
│
├── features/               # Independent feature modules
│   ├── authentication/     # Auth flow with role-based access
│   │   ├── api/           # Feature-specific API calls
│   │   ├── models/        # Auth domain models
│   │   ├── state/         # Riverpod state management
│   │   └── views/         # UI screens and components
│   ├── dashboard/          # Main dashboard module
│   ├── document_library/   # Document management
│   ├── landsourcing/       # Land sourcing features (On going)
│   ├── configuration/      # App configuration
|   |...................    #More Features
|   |...................
│   └── homepage/           # Home screen module
│
├── l10n/arb/               # ARB files for localization
└── generated/              # Auto-generated intl files
```

### 🧠 Architectural Benefits

- **Core vs Features Split** – Clear separation between shared utilities and business logic
- **Feature Independence** – Each module owns its API, models, state, and UI
- **Scalable & Testable** – Easy to add features without breaking existing functionality
- **Team Collaboration** – Multiple developers can work on different features simultaneously

## 🔧 Tech Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Frontend** | Flutter 3.x | Cross-platform UI development |
| **State Management** | Riverpod | Predictable state management & DI |
| **Navigation** | GoRouter | Declarative routing with guards |
| **Networking** | Dio | HTTP client with interceptors |
| **Backend** | Spring Boot | REST API services |
| **Localization** | Flutter Intl | Multi-language support |

## 🌐 Localization Support

- **English (EN)** 🇬🇧 – Primary language
- **Bangla (BN)** 🇧🇩 – Regional language support  
- **French (FR)** 🇫🇷 – International business language

Implemented using Flutter's official `intl` package with ARB file structure.

## 📊 Module Highlights

### 🔐 Authentication Module
- JWT token-based authentication
- Automatic token refresh via Dio interceptors
- Role-based route protection
- Secure local storage for session management

### 📈 Dashboard Module
- Real-time data visualization
- Role-specific content display
- Performance-optimized widgets
- Smooth animation transitions

### 📁 Document Library
- Lazy loading with pagination
- Advanced search and filtering
- Offline capability for recent documents
- Bulk operations support

## 🎯 Key Learnings & Engineering Decisions

### 🏗️ Architecture Choices
**Why Feature-First Modularization?**
- Instead of global folders, each feature owns its domain logic
- Enables parallel development and reduces merge conflicts
- Makes onboarding new team members more efficient

**State Management with Riverpod**
- Chosen over Provider/BLoC for superior testability and DI
- Trade-off: Steeper learning curve but excellent for large applications
- Provides compile-safe dependency injection

### ⚡ Performance Optimization
- **Minimized Rebuilds** – Strategic widget splitting using `Consumer`/`Selector`
- **Lazy Loading** – Implemented in heavy lists and data tables
- **Memory Management** – Efficient disposal of controllers and listeners
- **Network Optimization** – Request deduplication and caching strategies

### 🔄 Backend Communication
- **Dio Interceptors** – Automated token refresh and request retry logic
- **Error Handling** – Unified error handling across all API calls
- **Type Safety** – Full model serialization/deserialization

## 📸 Application Preview

*(Screenshots would be placed here in an actual portfolio)*

| Login Screen | Dashboard | Document Management |
|-------------|-----------|---------------------|
| *Modern auth UI with validation* | *Role-based dashboard layout* | *Advanced filtering interface* |

## 🚀 Getting Started (Development Perspective)

```dart
// Example of feature-first approach
class AssetManagementScreen extends ConsumerWidget {
  const AssetManagementScreen({super.key});
  
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final assetsAsync = ref.watch(assetsProvider);
    
    return assetsAsync.when(
      loading: () => const LoadingSlice(),
      error: (error, stack) => ErrorView(error: error),
      data: (assets) => AssetListView(assets: assets),
    );
  }
}
```

## 👨‍💻 Author

**Returaj**  
Flutter Developer specializing in large-scale applications, clean architecture, and performance optimization.

---

## ⚠️ Disclaimer

> **Confidentiality Notice**: This project was developed as part of my professional work at **One Direction Companies Limited (ODCL)**.  
> The actual codebase, proprietary business logic, and company-specific implementations remain **private and confidential**.  
> This documentation showcases only the **architectural patterns, technical decisions, and engineering practices** I implemented and can discuss professionally.

---

<div align="center">

*"Building scalable Flutter applications with clean architecture and maintainable codebases"*

</div>
