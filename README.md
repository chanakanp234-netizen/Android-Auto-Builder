# Android Auto Builder

A GitHub-hosted Android APK builder. Upload a complete Android Studio project ZIP under `input/`; GitHub Actions builds a debug APK in the cloud and publishes it as an Actions artifact.

## Automatic build

1. Add a complete Android project ZIP to `input/` (for example, `input/my-app.zip`).
2. Commit the ZIP to the `main` branch.
3. The **Build Android APK** workflow starts automatically.
4. Open the repository's **Actions** tab, select the latest run, and download `android-debug-apk` from Artifacts.

You can also run the workflow manually from **Actions → Build Android APK → Run workflow**, and specify the ZIP path.

## Required ZIP contents

The ZIP must contain a complete Gradle Android project, including:
- `gradlew`
- `gradle/wrapper/gradle-wrapper.jar` and `gradle-wrapper.properties`
- `settings.gradle` or `settings.gradle.kts`
- An Android application module with an `assembleDebug` task

The ZIP may contain one top-level enclosing directory; the workflow locates `gradlew`.

## Output

The workflow uploads the debug APK(s) as the artifact **android-debug-apk** for 14 days. Debug APKs are intended for testing and sideloading, not Play Store distribution.

## Public-repository warning

This repository is public. Any ZIP uploaded here is publicly accessible. Never upload private projects, credentials, API keys, signing keys, keystores, passwords, or personal data. For confidential projects, switch the repository to Private before uploading.

## Scope and limitations

- Uses GitHub-hosted runners; no local Android Studio, JDK, Gradle, or Android SDK is required.
- Builds `assembleDebug`; release signing is intentionally not configured.
- Does not guarantee every arbitrary ZIP is an Android Gradle project. Web projects, incomplete source archives, or projects missing Gradle wrapper files will fail validation.
