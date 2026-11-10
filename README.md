# fable-test-android-app

Minimal native Android chat app in Kotlin with Jetpack Compose — simple chat screen.

## Requirements

- JDK 17
- Android SDK with compileSdk 34
- Gradle 8.7 (system install)

## Build locally

This repo does not include the Gradle wrapper jar, so `./gradlew` does not work. Use a system Gradle 8.7:

```bash
gradle assembleDebug
```

The APK lands at:

```
app/build/outputs/apk/debug/app-debug.apk
```

## CI

GitHub Actions workflow **Build Debug APK** (`.github/workflows/build.yml`):

- Runs on `push` and `workflow_dispatch`
- Runner: `ubuntu-latest` with JDK 17 and Gradle 8.7
- Builds with `gradle assembleDebug`
- Uploads the debug APK as the `app-debug` workflow artifact

## Known issue

The Compose plugin issue is FIXED in the repo. The unused plugin declaration `org.jetbrains.kotlin.plugin.compose` was removed from `build.gradle` (root) and `app/build.gradle`. Compose is configured via `composeOptions` with `kotlinCompilerExtensionVersion '1.5.14'` alongside Kotlin 1.9.24.
