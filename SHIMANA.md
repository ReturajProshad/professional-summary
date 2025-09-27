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
- **Memory Management** – Efficient disposal of controllers and listeners; disk-based PDF loading to reduce memory usage, and minimized widget rebuilds.  
- **Network Optimization** – Efficient API requests and data fetching strategies to reduce unnecessary network calls

### 🔄 Backend Communication
- **Dio Interceptors** – Automated token refresh and request retry logic
- **Error Handling** – Unified error handling across all API calls
- **Type Safety** – Full model serialization/deserialization

## 📸 Application Preview
Shimana features a multilingual, dynamic, and visually rich interface. Below are some previews of key screens across different locales (🇧🇩 Bengali, 🇫🇷 French, 🇬🇧 English).

## 🧭 Splash & Authentication
| Splash Screen                                                                                                                 | Login Screen                                                                                                                 |
| ----------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| <img width="300" alt="splash_screen" src="https://github.com/user-attachments/assets/1a4a9772-6292-4a31-8f78-dbf1c8454a5d" /> | <img width="300" alt="login_screen" src="https://github.com/user-attachments/assets/f18d6901-402a-4d49-8b1e-f73469c1f57a" /> |

✨ A sleek splash screen transitions smoothly into a modern login interface with validation and localization support.

## 🏠 Dashboard & Navigation
| Locale           | Dashboard                                                                                                                     | Drawer                                                                                                                       |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 🇧🇩 **Bangla**  | <img width="300" alt="dash_board_BN" src="https://github.com/user-attachments/assets/b79f09f0-b4af-47f5-89ec-dfc7b6691420" /> | <img width="300" alt="appdrawer_BN" src="https://github.com/user-attachments/assets/64e84e41-5b22-4997-8cdd-35c1d10f8bdd" /> |
| 🇫🇷 **French**  | <img width="300" alt="dash_board_FR" src="https://github.com/user-attachments/assets/d3a275ac-49cd-4161-a7f0-8e0a8fb4f7cb" /> | <img width="300" alt="appDrawer_FR" src="https://github.com/user-attachments/assets/73813bb3-d77f-4b8b-ac65-18f0680f0d49" /> |
| 🇬🇧 **English** | <img width="300" alt="dash_board_EN" src="https://github.com/user-attachments/assets/2bced5b3-72eb-4248-8f30-abb2b77ab3ac" /> | <img width="300" alt="appdrawer_EN" src="https://github.com/user-attachments/assets/a05034cf-40e2-4c6e-9002-6f61d5b7bd6e" /> |

🌐 Multilingual UI: Shimana supports multiple languages dynamically with localized dashboards and menus.

## 🧭 Filtering & Dynamic Views
| Project List With Pagination (BN)                                                                                                               | Filter (EN)                                                                                                               |
| ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| <img width="300" alt="dashboard_BN" src="https://github.com/user-attachments/assets/4cff114b-54c5-4cfd-bf8d-8baab99cef19" /> | <img width="300" alt="Filter_EN" src="https://github.com/user-attachments/assets/4d2af058-a69b-4ced-be4d-686db88bbb6c" /> |

🔍 Powerful filtering and adaptive dashboards make navigation effortless.

## 📚 Document Management & PDF Handling
| PDF Loading                                                                                                                 | Table of Contents                                                                                                       | Overlay View                                                                                                                |
| --------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| <img width="300" alt="Pdf_loading" src="https://github.com/user-attachments/assets/6c014f5a-f52c-437f-8710-7d71808d1773" /> | <img width="300"  alt="pdf_TOC" src="https://github.com/user-attachments/assets/196d43e4-4ec3-4fa0-a23a-b82bfd74d0fd" /> | <img width="300"  alt="PDF_Overlay" src="https://github.com/user-attachments/assets/9bf755b4-40ce-44af-9977-cabbb875f51f" /> |

## 🚀 Getting Started (Development Perspective)

```dart
// Example of feature-first approach
class AssetManagementScreen extends ConsumerWidget {
  const AssetManagementScreen({super.key});
  
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final assetState = ref.watch(assetsProvider);

    return Scaffold(
      appBar: AppBar(title: const Text('Asset Management')),
      body: Column(
        children: [
          if (assetState.isLoading) const LoadingSlice(),
          if (assetState.error != null)
            ErrorView(error: assetState.error!),
          Expanded(
            child: AssetListView(assets: assetState.assetList),
          ),
        ],
      ),
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
