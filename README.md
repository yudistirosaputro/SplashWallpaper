# Splash Wallpaper

Splash Wallpaper is a modular Android wallpaper gallery app built with Kotlin and Jetpack Compose. The app displays a staggered grid of wallpaper images, supports bottom navigation, and includes separate Home, Collection, and About feature modules.

## Features

- Home screen with a 3-column staggered wallpaper grid.
- Wallpaper cards loaded with Coil from remote image URLs.
- Detail screen route with full-image, author, location, like count, and bio UI.
- Collection screen with an empty-state message.
- About screen with profile image, name, and email.
- Bottom navigation for Home, Collection, and About.
- Hilt dependency injection across the app, data, and feature layers.
- Fake in-memory wallpaper data for local development.

## Tech Stack

- Kotlin 1.9.0
- Jetpack Compose with Material 3
- Navigation Compose
- Hilt
- Kotlin Coroutines and Flow
- Coil for image loading
- Gradle Kotlin DSL
- Gradle version catalog
- Custom Gradle convention plugins in `build-logic`

## Project Structure

```text
.
+-- app                 # Android app shell, Hilt application, Activity, NavHost, bottom bar
+-- build-logic         # Shared Gradle convention plugins
+-- core                # Core Android library module
+-- data                # Repository implementation and fake wallpaper response data
+-- designsystem        # Compose theme, colors, and typography
+-- domain              # Domain models, repository contract, and use cases
+-- feature
|   +-- about           # About screen and navigation route
|   +-- collection      # Collection screen and navigation route
|   +-- home            # Home grid, detail screen, ViewModels, and routes
+-- gradle              # Wrapper and version catalog
+-- ui                  # Shared Compose UI components and UiState helper
```

## Architecture

The project follows a simple modular clean architecture style:

- `domain` defines `ImageData`, `ProfileUser`, `WallpaperRepository`, and wallpaper use cases.
- `data` implements `WallpaperRepository` with `WallpaperRepositoryImpl` and maps DTOs from `FakeImageResponse` into domain models.
- `feature:*` modules own screen UI, ViewModels, and navigation route extensions.
- `ui` contains reusable Compose components such as `ImageComponent`, `ItemComponent`, and `UiState`.
- `designsystem` provides `WallpaperTheme` and shared Material color/typography setup.
- `app` wires everything together through `MainActivity`, `WallpaperApplication`, `AppHost`, and the bottom navigation destinations.

## Requirements

- Android Studio with Gradle support.
- JDK compatible with the project Gradle setup.
- Android SDK:
  - Min SDK: 26
  - Compile SDK: 33
  - Target SDK: 33

## Getting Started

1. Clone the repository.
2. Open the project in Android Studio.
3. Let Android Studio sync Gradle.
4. Run the `app` configuration on an emulator or Android device.

The app requests internet permission because wallpaper and profile images are loaded from remote URLs.

## Useful Commands

On Windows:

```powershell
.\gradlew.bat assembleDebug
.\gradlew.bat test
.\gradlew.bat connectedAndroidTest
```

On macOS or Linux:

```bash
./gradlew assembleDebug
./gradlew test
./gradlew connectedAndroidTest
```

## Current Notes

- Wallpaper data currently comes from `FakeImageResponse`; Retrofit and OkHttp dependencies are available but no live API service is wired yet.
- `GetWallpaperDetailUseCase` exists in the domain layer, but the call in `DetailViewModel` is currently commented out.
- Unit and instrumented test files are still the default generated examples.

## Author

Yudistiro Septian Dwi Saputro
