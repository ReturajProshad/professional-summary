# 📱 FoodExpo – Cross-Platform Kiosk Application

> A high-performance kiosk application built for **One Direction Companies Limited (ODCL)** enabling seamless restaurant ordering experiences on both Windows and Android platforms with robust POS integration.

## 🚀 Key Highlights

- **🖥️📱 Cross-Platform Kiosk** – Single codebase for Windows & Android with platform-specific optimizations
- **🍕 Intuitive Ordering Flow** – Streamlined menu browsing, customization, and order management
- **🧾 POS Integration** – Direct invoice generation and receipt printing capabilities
- **🏗️ Modular Architecture** – Feature-first design with clean separation of concerns
- **⚡ Performance Optimized** – Fast loading and smooth animations for kiosk usage
- **🛠️ Hardware Integration** – Platform-specific printer services and device management

## 🏗️ Project Architecture

The application follows a **feature-first modular architecture** designed for maintainability and cross-platform compatibility:

```
lib/
├── core/                        # Shared utilities and platform abstraction
│   ├── enums/                   # Application-wide enums
│   ├── global_service/          # Platform-specific services
│   │   ├── android/             # Android-specific implementations
│   │   └── windows/             # Windows-specific implementations
│   ├── global_widgets/          # Reusable cross-platform widgets
│   ├── util/                    # Utility functions and helpers
│   └── widgets/                 # Common widget components
│
├── features/                    # Independent feature modules
│   ├── booking/                 # Table booking functionality
│   │   ├── model/              # Booking data models
│   │   ├── state/              # Riverpod state management
│   │   ├── view/               # UI screens
│   │   └── widget/             # Feature-specific widgets
│   ├── cart/                    # Shopping cart management
│   │   ├── api/                # Cart-related API calls
│   │   ├── model/              # Cart data models
│   │   ├── states/             # Cart state providers
│   │   ├── view/               # Cart UI screens
│   │   └── widgets/            # Cart components
│   ├── food_list/               # Menu and product management
│   │   ├── api/                # Product API integration
│   │   ├── model/              # Product data models
│   │   │   └── full_product_data_model/
│   │   ├── states/             # Product state management
│   │   ├── view/               # Menu screens
│   │   └── widgets/            # Product components
│   │       └── variant/        # Product variant handling
│   ├── home/                    # Home dashboard
│   │   ├── state/              # Home screen state
│   │   └── view/               # Main landing screen
│   ├── on_board/                # Onboarding flow
│   │   ├── model/              # Onboarding models
│   │   ├── state/              # Onboarding state
│   │   └── view/               # Onboarding screens
│   └── order/                   # Order management
│       ├── models/              # Order data models
│       └── services/            # Order processing services
│
└── gen/                         # Generated code
```

### 🧠 Architectural Benefits

- **Platform Abstraction** – Clean separation between shared logic and platform-specific implementations
- **Feature Independence** – Each module can be developed and tested independently
- **Scalable Structure** – Easy to add new features without impacting existing functionality
- **Team Collaboration** – Multiple developers can work on different features simultaneously

## 🔧 Tech Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Frontend** | Flutter 3.x | Cross-platform UI development |
| **State Management** | Riverpod | Reactive state management & dependency injection |
| **Navigation** | GoRouter | Declarative routing with deep linking |
| **Networking** | Dio | HTTP client with interceptors and error handling |
| **POS Printing** | Platform-specific APIs | Receipt and invoice generation |
| **Platform Support** | Flutter Windows + Android | Native kiosk deployment |

## 🖨️ POS Printing Integration

### Windows Implementation
```dart
// core/global_service/windows/pos_service.dart
class WindowsPOSService {
  // Win32 API integration for printer discovery
  // ESC/POS utils for byte data generation
  // Direct printer communication
}
```

### Android Implementation
```dart
// core/global_service/android/pos_service.dart  
class AndroidPOSService {
  // flutter_pos_platform integration
  // Bluetooth/USB printer discovery
  // ESC/POS command generation
}
```

## 📊 Feature Highlights

### 🍽️ Food List Module
- **Product Catalog** – Comprehensive menu display with categories
- **Variant Support** – Size, toppings, and customization options
- **Real-time Updates** – Live pricing and availability
- **Image Management** – High-quality food imagery with caching

### 🛒 Cart Module
- **Interactive Cart** – Add/remove items with quantity management
- **Customization Tracking** – Preserve item modifications
- **Price Calculation** – Real-time total with tax and discounts
- **Session Management** – Maintain cart state across navigation

### 📅 Booking Module
- **Table Reservation** – Time-based booking system
- **Capacity Management** – Real-time table availability
- **Customer Details** – Guest information capture
- **Confirmation Flow** – Booking confirmation and reminders

### 📋 Order Management
- **Order Processing** – Kitchen order generation
- **Status Tracking** – Preparation to completion flow
- **Invoice Generation** – Professional receipt creation
- **Print Integration** – Direct POS printing capability

## 🎯 Key Technical Decisions

### 🏗️ Architecture Choices
**Why Feature-First Modular Approach?**
- Enables parallel development across feature teams
- Isolated testing and deployment capabilities
- Clear boundaries for platform-specific implementations

**State Management with Riverpod**
- **Predictable State Flow** – Clear data flow from API to UI
- **Dependency Injection** – Clean service injection across features
- **Testability** – Easy mocking and unit testing
- **Performance** – Optimized rebuilds using *ConsumerWidget* for reactive UI updates.

### ⚡ Performance Optimizations
- **Lazy Loading** – Menu and images loaded on-demand
- **Efficient Rebuilds** – Strategic use of Consumer and Selector
- **Memory Management** – Proper controller disposal and state cleanup
- **Network Optimization** – Cached responses and efficient API calls

### 🔧 Platform-Specific Implementations
- **Unified Interface** – Common API across platforms
- **Native Capabilities** – Leverage platform-specific hardware features
- **Consistent UX** – Platform-appropriate UI while maintaining brand consistency

## 🌐 User Experience Features

### Intuitive Ordering Flow
1. **Onboarding Screen** – Video & image slideshow with a chef Lottie animation
2. **Welcome Screen** – Clear call-to-action for starting orders
3. **Category Navigation** – Easy menu browsing by food types
4. **Product Customization** – Visual modifiers and options selection
5. **Cart Review** – Clear summary before checkout
6. **Order Confirmation** – Immediate feedback and receipt generation  
   - Users can **scan a QR code** to get the invoice on their mobile phone

### Kiosk-Optimized Design
- **Touch-Friendly** – Large buttons and intuitive gestures
- **High Contrast** – Readable in various lighting conditions
- **Minimal Navigation** – Streamlined user journey
- **Offline Resilience** – Graceful degradation when connectivity issues occur

## 🧭 Development Example (Feature-first Implementation)


```dart
// Example of feature implementation
class FoodListScreen extends ConsumerWidget {
  const FoodListScreen({super.key});
  
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final productsAsync = ref.watch(productsProvider);
    
    return productsAsync.when(
      loading: () => const KioskLoadingIndicator(),
      error: (error, stack) => ErrorView(error: error),
      data: (products) => ProductGridView(products: products),
    );
  }
}

// Platform-aware service usage
class POSService {
  static POSInterface getInstance() {
    if (Platform.isWindows) return WindowsPOSService();
    if (Platform.isAndroid) return AndroidPOSService();
    throw UnsupportedError('Platform not supported');
  }
}
```



## 📸 Application Preview

Shimana Kiosk (FoodExpo) offers a seamless restaurant ordering experience — from onboarding to checkout and POS printing.  
This section demonstrates the complete user flow through annotated screenshots.

---

### 🏁 Splash & Onboarding Flow

| Splash Screen | Onboarding Step 1 | Onboarding Step 2 | Onboarding Step 3 |
|---------------|------------------|------------------|------------------|
| <img width="250" src="https://github.com/user-attachments/assets/cc141b92-b3ba-4ddc-bebf-1eba6007c0c3" /> | <img width="250" src="https://github.com/user-attachments/assets/6f168a6b-ce38-4ad6-b094-4f3a9d4f9341" /> | <img width="250" src="https://github.com/user-attachments/assets/3deeb0f4-69d1-4eb8-acf6-cce0ea12914e" /> | <img width="250" src="https://github.com/user-attachments/assets/20a96c2c-323a-4128-a787-21fb482d2277" /> |

✨ Smooth onboarding introduces users to the kiosk features and ordering process.

---

### 🔐 Authentication & Settings Access

| Login Screen 1 | Login Screen 2 | Hidden Settings |
|----------------|----------------|----------------|
| <img width="250" src="https://github.com/user-attachments/assets/bf7b4b56-89f7-459e-8885-2fe5d949487a" /> | <img width="250" src="https://github.com/user-attachments/assets/bf22fd55-0889-46d5-b007-b85c02fca814" /> | <img width="250" src="https://github.com/user-attachments/assets/0790efe0-3a93-4b2b-894d-1d1797f69621" /> |

🔑 Secure login flow with hidden settings access for administrators.

---

### 🏠 Home & Category Browsing

| Home Page | Category 1 | Category 2 | Category 3 |
|------------|-------------|-------------|-------------|
| <img width="250" src="https://github.com/user-attachments/assets/61307de5-584b-4ab3-9939-fa8bc769743b" /> | <img width="250" src="https://github.com/user-attachments/assets/645bf1e0-ccc5-4688-81ce-cbb64b2fb213" /> | <img width="250" src="https://github.com/user-attachments/assets/8ed7682d-c3a6-4124-9144-c4300da0f875" /> | <img width="250" src="https://github.com/user-attachments/assets/45992e29-e0de-491e-9146-f7480b4f1ee7" /> |

🍽️ Browse menu items by category with large, interactive UI components optimized for kiosks.

---

### 🍲 Product Details & Search

| Food Details 1 | Food Details 2 | Search View 1 | Search View 2 |
|----------------|----------------|----------------|----------------|
| <img width="250" src="https://github.com/user-attachments/assets/7f1df07c-bbcb-4635-8c0c-db07f97cbf22" /> | <img width="250" src="https://github.com/user-attachments/assets/2f42a06a-ee11-4e9f-a3c1-d01a2d2cac63" /> | <img width="250" src="https://github.com/user-attachments/assets/dc1e48a2-49ef-4432-85ea-69ebc4351c22" /> | <img width="250" src="https://github.com/user-attachments/assets/432751bc-b48a-4d79-8bfd-c0aa4a8ac253" /> |

🔍 Quick search and detailed product pages with add-ons, quantity selection, and customizations.

---

### 🛒 Cart & Order Summary

| Cart View | How to Get Invoice | Invoice Summary |
|------------|------------------|----------------|
| <img width="250" src="https://github.com/user-attachments/assets/94dcb657-3cc5-4387-9908-4b474607ef14" /> | <img width="250" src="https://github.com/user-attachments/assets/7dea0e86-d6e4-48ba-ad53-d59624660f48" /> | <img width="250" src="https://github.com/user-attachments/assets/6005ced1-5446-4893-b143-4df2cb4101c1" /> |

🧾 Cart management supports item edits, quantity changes, and smooth checkout flow with invoice generation.

---

### 🧾 POS Printing & Mobile Integration

| POS Invoice Print | Mobile QR Scan | Invoice PDF |
|------------------|----------------|--------------|
| <img width="250" src="https://github.com/user-attachments/assets/82495d6c-092d-4b7a-874f-6cbe4947367c" /> | <img width="250" src="https://github.com/user-attachments/assets/8d98dcaa-1046-4caf-9e56-68d5b5fa925b" /> | <img width="250" src="https://github.com/user-attachments/assets/84e4dd09-ccc2-4447-8082-121429d7e3fc" /> |

🖨️ Integrated POS printing and mobile-friendly QR scanning bridge kiosk ordering with restaurant operations.

---

## 👨‍💻 Author

**Returaj**  
Flutter Developer specializing in cross-platform applications, kiosk systems, and hardware integration.

---

## ⚠️ Disclaimer

> **Confidentiality Notice**: This project was developed as part of my professional work at **One Direction Companies Limited (ODCL)**.  
> The actual codebase, proprietary business logic, and company-specific implementations remain **private and confidential**.  
> This documentation showcases only the **architectural patterns, technical decisions, and engineering practices** I implemented and can discuss professionally.

---

<div align="center">

*"Building intuitive kiosk experiences with robust hardware integration and cross-platform compatibility"*


---

