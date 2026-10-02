<p align="center">
  <img src="docs/assets/banner.svg" alt="Hexacom Banner" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white" alt="Flutter">
  <img src="https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logo=dart&logoColor=white" alt="Dart">
  <img src="https://img.shields.io/badge/Firebase-FFCA28?style=for-the-badge&logo=firebase&logoColor=black" alt="Firebase">
  <img src="https://img.shields.io/badge/Android-3DDC84?style=for-the-badge&logo=android&logoColor=white" alt="Android">
  <img src="https://img.shields.io/badge/iOS-000000?style=for-the-badge&logo=apple&logoColor=white" alt="iOS">
</p>

# 🍔 Hexacom

**A full-featured food delivery customer app built with Flutter** — browse restaurants, search dishes, manage a cart, check out, pay, chat with the restaurant, and track your order live on a map.

> **Developed by [Arslan Malik](https://github.com/arsalanmaalik461)**
> 📱 WhatsApp: [+92 300 8987448](https://wa.me/923008987448) · 🌐 Website: [arslanmalik.tech](https://arslanmalik.tech)

---

## 🌟 Executive Overview

Hexacom is the customer-facing mobile app of a food-delivery platform, written entirely in Dart/Flutter for Android, iOS, and Web from a single codebase. It talks to a REST backend (`/api/v1/...`) for everything dynamic — restaurant and menu catalogs, coupons, orders, chat messages, and payments — while Firebase powers push notifications, social authentication, and crash reporting.

The app is organized into ~30 feature modules under `lib/features/` (auth, cart, checkout, order, track, chat, payment, coupon, flash sale, wishlist, and more), with a `Provider` + `GetIt` state-management setup and `go_router` for deep-linkable navigation. Maps and live order tracking run on Google Maps + geolocator, and the whole UI is localized and ships with light and dark themes.

The codebase ships ready to rebrand: the Android package is `com.sixamtech.hexacom_user`, the app label is **Hexacom**, and the backend base URL lives in one constant (`AppConstants.baseUrl` in `lib/utill/app_constants.dart`) — point it at your own server and the entire storefront comes alive.

---

## 📑 Table of Contents

- [✨ Key Features & Highlights](#-key-features--highlights)
- [🖥️ Feature Showcase](#️-feature-showcase)
- [🏗️ System Architecture](#️-system-architecture)
- [🚀 Quickstart & Installation Guide](#-quickstart--installation-guide)
- [📂 Project Structure](#-project-structure)
- [🛡️ Security & Notes](#️-security--notes)

---

## ✨ Key Features & Highlights

| Feature | Description |
| :--- | :--- |
| 🔐 Multi-login auth | Phone/OTP (PIN-code fields), email, plus Google, Facebook & Apple sign-in via Firebase Auth |
| 🏪 Restaurant & menu browsing | Categories, banners, carousels, flash-sale deals, discounted products, staggered product grids |
| 🔎 Smart search | Type-ahead search across products with search history (`flutter_typeahead`) |
| 🛒 Cart & checkout | Multi-item cart, saved delivery addresses, coupon apply, order placement |
| 💳 Payments | Dedicated payment module wired to backend gateways (in-app webview supported) |
| 📍 Live order tracking | Real-time delivery tracking on Google Maps with geolocation & geocoding |
| 💬 In-app chat | Two-way chat with the restaurant during an active order |
| 🔔 Push notifications | Firebase Cloud Messaging + local notifications (custom `notification.wav`) |
| ⭐ Ratings & reviews | Rate restaurants/dishes, read reviews |
| ❤️ Wishlist | Save favourite products/restaurants |
| 🎟️ Coupons & flash sales | Coupon list/apply and time-limited flash-sale products |
| 🌍 Multi-language + themes | Full localization support and light/dark theme switching |
| 📦 Maintenance & update modes | Built-in force-update and maintenance-mode screens |
| 🍪 Web-ready | Responsive web build with URL strategy & cookies banner |

---

## 🖥️ Feature Showcase

### 1. 🔐 Authentication & Onboarding

> "Sign in with phone, email, Google, Facebook or Apple — verified with OTP, localized from the first screen."

- Onboarding walkthrough, language selection, and welcome screens on first launch
- OTP verification flows for phone and email (`pin_code_fields`)
- Social sign-in via Firebase Auth, Google Sign-In, Facebook Auth, and Sign in with Apple
- Password reset / forgot-password flow backed by the auth API

### 2. 🛒 Catalog, Cart & Checkout

> "Browse → search → cart → coupon → checkout: the whole food-ordering funnel in one smooth flow."

- Home dashboard with banners, categories, flash sales, and latest/discounted products
- Product detail pages with photo gallery (`photo_view`), variants, and add-ons
- Cart with quantity controls, coupon application, and multiple saved addresses
- Checkout screen computing totals before placing the order via `/api/v1/customer/order/place`

### 3. 📍 Order Tracking & Chat

> "Watch your food move on a live map — and message the restaurant if anything changes."

- Live map tracking screen (Google Maps) with delivery-rider position updates
- Order list with status timeline: placed → confirmed → cooking → on the way → delivered
- In-app chat thread per order (message send/receive via `/api/v1/customer/message/*`)
- Push notifications on every order status change

### 4. 💳 Payments & Notifications

> "Pay how you like, and never miss a status update."

- Payment module with in-app webview support for gateway redirects (`flutter_inappwebview`)
- Transaction history tied to the customer profile
- FCM token registration (`/api/v1/customer/cm-firebase-token`) + local notification rendering
- Firebase Crashlytics for production crash reporting

---

## 🏗️ System Architecture

```mermaid
graph TD
    A["Hexacom Flutter App<br/>(Android / iOS / Web)"] --> B["REST Backend<br/>/api/v1/..."]
    A --> C["Firebase<br/>Auth · FCM · Crashlytics"]
    A --> D["Google Maps Platform<br/>Maps · Places · Geocoding"]
    B --> E["MySQL Database"]
    B --> F["Admin Panel<br/>(restaurants, orders, coupons)"]
    A --> G["Local Device<br/>SharedPreferences · cache · assets"]

    style A fill:#02569B,color:#fff
    style B fill:#FF2D20,color:#fff
    style C fill:#FFCA28,color:#000
```

**Stack:** Flutter 3.4+ / Dart · Provider + GetIt (state) · go_router (navigation) · Dio + http (networking) · Firebase Auth / Messaging / Crashlytics · Google Maps Flutter · SharedPreferences (local storage) · flutter_localizations (i18n).

---

## 🚀 Quickstart & Installation Guide

### Prerequisites

- [Flutter SDK](https://docs.flutter.dev/get-started/install) **3.4.0 or newer** (Dart bundled)
- Android Studio / Xcode for emulator or device builds
- A Firebase project (or reuse the bundled `google-services.json` / iOS plist)
- The backend server URL (API exposing `/api/v1/...`)

### Step-by-Step Installation

```bash
# 1. Clone the repo
git clone https://github.com/arsalanmaalik461/Hexcom.git
cd Hexcom

# 2. Point the app at your backend (REQUIRED — currently a placeholder)
#    Edit lib/utill/app_constants.dart and set:
#      static const String baseUrl = 'https://your-server.com';

# 3. Install dependencies
flutter pub get

# 4. Run on a connected device / emulator
flutter run

# 5. Build release APK
flutter build apk --release
```

> ⚠️ The stock checkout of this repo has `baseUrl = 'YOUR_BASE_URL_HERE'` — the app will not load data until you set it to a real backend URL.

---

## 📂 Project Structure

```
Hexcom/
├── lib/
│   ├── main.dart                 # App entry point, provider tree, routing
│   ├── di_container.dart         # GetIt service registration
│   ├── common/                   # Shared widgets, models, enums
│   ├── data/datasource/remote/   # Dio API clients
│   ├── features/                 # ~30 feature modules
│   │   ├── auth/                 # login, register, OTP, social sign-in
│   │   ├── home/                 # dashboard, banners, categories
│   │   ├── product/              # product list & detail
│   │   ├── cart/ checkout/       # cart + checkout flow
│   │   ├── payment/              # payment screens & gateways
│   │   ├── order/ track/         # orders + live map tracking
│   │   ├── chat/                 # in-app restaurant chat
│   │   ├── coupon/ flash_sale/   # promos & deals
│   │   ├── notification/         # push & in-app notifications
│   │   ├── profile/ address/     # account & addresses
│   │   ├── wishlist/ rate_review/# favourites & reviews
│   │   ├── search/ menu/         # search & category menus
│   │   ├── language/ onboarding/ # locale + first-run screens
│   │   ├── splash/ update/       # startup, force-update
│   │   ├── maintanance/ support/ # maintenance & help
│   │   └── html/ welcome_screen/ # static pages & welcome
│   ├── helper/                   # notification, API, route helpers
│   ├── localization/             # i18n language files
│   ├── provider/                 # theme, language, localization
│   ├── theme/                    # light_theme / dark_theme
│   └── utill/                    # app_constants, images, styles, routes
├── assets/                       # fonts, icons, images, svg, sounds
├── android/                      # com.sixamtech.hexacom_user
├── ios/                          # iOS runner + Firebase plist
├── web/                          # web build entry
├── test/                         # widget tests
└── pubspec.yaml                  # dependencies & assets
```

---

## 🛡️ Security & Notes

- **Base URL is a placeholder** (`YOUR_BASE_URL_HERE`): set a real HTTPS backend URL before release.
- The repo ships with Firebase config files (`google-services.json`, iOS plist) committed — fine for a demo, but rotate/replace keys for production builds and consider moving secrets out of the repo.
- OTP, social sign-in, and password-reset flows delegate to the backend + Firebase — never store user tokens in plain text; the app uses `shared_preferences` only for session tokens and settings.
- Location, camera, notification, and storage permissions are requested at runtime (`permission_handler`) — review them against your store-listing privacy policy.
- `flutter run` / release builds require a valid Firebase project matching the bundled package name `com.sixamtech.hexacom_user` if you keep the default config files.

---

<p align="center">
  <sub>Developed with ❤️ by <a href="https://github.com/arsalanmaalik461">Arslan Malik</a> · 📱 <a href="https://wa.me/923008987448">WhatsApp: +92 300 8987448</a> · 🌐 <a href="https://arslanmalik.tech">arslanmalik.tech</a></sub>
</p>
