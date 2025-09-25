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

## 🚀 Getting Started (Development Perspective)

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

*(Kiosk interface screenshots would be placed here)*

| Welcome Screen | Menu Browsing | Cart Management |
|----------------|---------------|-----------------|
| *Clean kiosk landing interface* | *Category-based product display* | *Interactive cart with customization* |

| Order Confirmation | POS Printing | Booking Interface |
|-------------------|--------------|-------------------|
| *Order summary and confirmation* | *Receipt generation workflow* | *Table reservation system* |

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

</div>

## 🔗 Project Links

- **📋 FoodExpo Project Documentation**: [View Detailed Architecture](https://github.com/ReturajProshad/professional-summary/blob/main/FOODEXPO.md)
- **🏢 ODCL Portfolio**: [All Professional Projects](https://github.com/ReturajProshad/professional-summary)

---

*Last Updated: ${new Date().toLocaleDateString()}*
