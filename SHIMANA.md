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
│   ├── document_library/      # Document management (Asset Management Module)
│   │   ├── api/               # Document APIs (CRUD, search, etc.)
│   │   ├── models/            # File & document models
│   │   ├── state/             # Riverpod state providers
│   │   └── views/             # UI for library, PDF viewer, create file
│   ├── landsourcing/       # Land sourcing features (On going)
│   ├── configuration/        # App configuration (Access & Role Management)
│   ├── archive/               # Archived items module
│   └── ...more features       # (24+ independent modules in total)
│   └── homepage/           # Home screen module
│
├── l10n/arb/               # Translations (EN, BN, FR)
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

## 🌐 Localization
The app is fully localized with support for multiple languages:

- **Bangla (bn_BD) 🇧🇩 – Primary language (default for Bangladeshi users)**
- **English (en_GB) 🇬🇧 – Secondary language (international support)**
- **French (fr_FR) 🇫🇷 – International business language**


Implemented using Flutter's official `intl` package with ARB file structure.

## 📊 Module Highlights

### 🔐 Authentication Module
- **JWT authentication** with access & refresh token separation  
- **Access token** → Used for API authorization and role-based route management  
- **Refresh token** → Ensures seamless session renewal without re-login  
- **Automatic token refresh** via Dio interceptors  
- **Secure session storage** using Flutter Secure Storage

### 📈 Dashboard Module
- Real-time data visualization
- Role-specific content display
- Performance-optimized widgets
- Smooth animation transitions

### 📁 Document Library
- **Lazy loading with pagination** for efficient handling of large datasets  
- **Advanced search and filtering** by fields such as Thana, Mouza, and Country  
- **Offline access** for recently viewed documents  
- **Bulk operations** – *planned for future release* (select multiple documents for actions like delete, share, or export)

### 📁 PDF Viewer Highlights
- Memory-efficient PDF loading with **disk-based storage** and progress tracking
- Horizontal page swiping with snapping, previous/next buttons, and **direct page jump dialog**
- **Table of Contents drawer** for quick navigation to sections
- Dynamic **QR code overlay** with asset metadata on first page
- Responsive layout and scrollable overlays for metadata display
- State management handled via **Riverpod** (`ConsumerStatefulWidget` + `ChangeNotifierProvider`)
- Robust **error handling** and download cancellation support



## 🎯 Key Learnings & Engineering Decisions

### 🏗️ Architecture Choices
**Why Feature-First Modularization?**
- Instead of global folders, each feature owns its domain logic
- Enables parallel development and reduces merge conflicts
- Makes onboarding new team members more efficient

**State Management with Riverpod**
- **Riverpod** for structured state management and dependency injection  
- Provides **compile-time safety** for dependencies and state access  
- Chosen over Provider for superior **testability and scalability** in large applications  
- Trade-off: Steeper learning curve compared to Provider, but easier to maintain in enterprise-scale apps


### ⚡ Performance Optimization
- **Minimized Rebuilds** – Split widgets and structured providers to avoid unnecessary widget tree rebuilds  
- **Lazy Loading** – Implemented in heavy lists and data tables  
- **Memory Management** – Efficient disposal of controllers and listeners;disk-based PDF loading to reduce memory usage, and minimized widget rebuilds.  
- **Network Optimization** – Efficient API requests and data fetching strategies to reduce unnecessary network calls

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
