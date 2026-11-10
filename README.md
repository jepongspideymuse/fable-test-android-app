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

The committed `build.gradle` and `app/build.gradle` still reference the Gradle plugin `org.jetbrains.kotlin.plugin.compose` at version `1.9.24`, which was never published for Kotlin 1.9.x (the plugin was only published from 2.0.0). A plain local build will therefore fail at plugin resolution.

The CI workflow works around this by removing those plugin lines in the runner's checkout before building. Compose is provided by the Kotlin Android plugin with `kotlinCompilerExtensionVersion 1.5.14`.
