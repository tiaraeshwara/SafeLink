# SafeLink

SafeLink is a Flutter-based emergency alert application that helps users stay informed about nearby risks, view alert zones on a map, and trigger SOS requests in critical situations. The app uses Firebase for authentication, realtime data storage, push messaging, and backend-connected app services.

## Overview

This project is designed as a multi-platform Flutter application with support for mobile, web, desktop, and Firebase-backed services. It combines:

- user authentication
- role-based profiles
- realtime emergency alerts
- map-based alert visualization
- push notification setup
- an SOS flow for emergency response scenarios

The current codebase already contains a solid app structure, provider-based state management, Firebase integration, and the main user-facing screens.

## Features

### Authentication
- Email/password registration and login
- Google Sign-In support
- Firebase Authentication integration
- Password reset support in the auth layer
- Firestore-backed user profile creation and syncing

### Alerts
- Realtime alert streaming from Firestore
- Alert severity levels: `green`, `yellow`, and `red`
- Government verification support for alerts
- Proximity filtering based on alert radius
- Client-side distance checks using the Haversine formula

### Map View
- Google Maps integration
- Colored markers for alert severity
- Alert radius circles displayed on the map
- Location permission handling

### SOS Flow
- Dedicated SOS screen with press-and-hold interaction
- Animated emergency trigger UI
- Placeholder workflow for future Firestore + FCM emergency dispatch

### User Profile
- Profile page showing account information
- Role badges for `user`, `regular`, `admin`, and `government`
- Sign-out flow

### Notifications
- Firebase Cloud Messaging setup
- Foreground and background message handling
- Topic subscribe/unsubscribe helpers

## Tech Stack

- **Framework:** Flutter
- **Language:** Dart
- **Backend:** Firebase
  - Firebase Authentication
  - Cloud Firestore
  - Firebase Cloud Messaging
  - Firebase Storage
- **State Management:** Provider
- **Maps:** Google Maps Flutter
- **Connectivity:** connectivity_plus
- **Permissions:** permission_handler
- **UI:** Material Design, Google Fonts, Flutter SVG

## Project Structure

```text
lib/
├── app/                # App bootstrap, configuration, routing, and root widget
├── models/             # Data models such as alerts and users
├── providers/          # Provider-based app state management
├── screens/
│   ├── auth/           # Login and registration screens
│   ├── home/           # Home dashboard
│   ├── map/            # Alert map screen
│   ├── profile/        # User profile screen
│   └── sos/            # Emergency SOS screen
├── services/           # Firebase and domain service layer
├── theme/              # App theming
├── utils/              # Constants and helpers
├── widgets/            # Shared UI widgets such as auth gate
├── firebase_options.dart
└── main.dart
```

## Architecture Notes

The app follows a layered structure:

- **Services** handle direct interaction with Firebase APIs.
- **Providers** expose application state and async actions to the widget tree.
- **Models** define alert and user domain objects.
- **Screens** provide the UI for major user workflows.

### Important implementation details
- Firebase is initialized at startup in `lib/main.dart`.
- Firestore offline persistence is enabled with unlimited cache.
- `AuthProvider` listens to Firebase auth state changes and keeps user profile data synced.
- `AlertProvider` manages live alert subscriptions and filtering.
- `AlertService` supports both global and location-based realtime alert streams.
- `AlertModel` includes geo radius calculations for proximity checks.

## Key Screens

- **Splash Screen** – branded app launch experience
- **Login Screen** – email/password and Google sign-in
- **Register Screen** – account creation flow
- **Home Screen** – user dashboard and quick SOS access
- **SOS Screen** – long-press emergency trigger interface
- **Map Screen** – visual display of nearby alert zones
- **Profile Screen** – account details and sign out
- **Main Shell** – persistent bottom navigation across main sections

## Firebase Setup

This project requires Firebase configuration before it can run properly.

### Expected Firebase services
- Authentication
- Cloud Firestore
- Cloud Messaging
- Storage

### Repository files related to Firebase
- `firebase.json`
- `firebase_config.template.json`
- `firestore.rules`
- `lib/firebase_options.dart`

### Setup steps
1. Create a Firebase project.
2. Add the required Android, iOS, web, or desktop apps in Firebase.
3. Generate FlutterFire configuration.
4. Replace template or local Firebase config values as needed.
5. Ensure Google Maps and Firebase credentials are configured for your target platforms.

## Getting Started

### Prerequisites
- Flutter SDK
- Dart SDK
- Firebase project
- Android Studio, VS Code, or another Flutter-compatible IDE
- Platform-specific SDKs for Android/iOS/web/desktop targets

### Install dependencies
```bash
flutter pub get
```

### Run the app
```bash
flutter run
```

## Development Notes

Based on the current implementation, a few areas appear to still be in progress:

- The SOS action currently uses a simulated delay and is marked for future real dispatch integration.
- Some home screen content is still static placeholder UI.
- The map currently starts from a default camera position and does not yet use live device location.
- Some repository folders such as `models` and `screens` include scaffold-style placeholders alongside implemented files.

## Suggested Next Improvements

- Connect the SOS flow to Firestore and push notifications
- Add live GPS location support
- Surface realtime nearby alerts on the home dashboard
- Add admin/government workflows for creating and verifying alerts
- Improve test coverage for providers and services
- Document Firebase environment setup in more detail

## Repository Language Composition

- Dart — 70.1%
- HTML — 22.0%
- C++ — 4.1%
- CMake — 3.0%
- Swift — 0.6%
- C — 0.2%

## Status

SafeLink is already structured as a serious emergency-alert application prototype with production-oriented foundations such as Firebase auth, realtime Firestore streams, offline persistence, role-aware profiles, and map-based alert visualization. It appears to be in an active development stage, with core architecture in place and some workflows still being completed.
