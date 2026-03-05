# Invoice Android App

This repository contains an Android app that embeds your existing `index.html` invoice UI in a `WebView`, lets users fill the form, and generates a PDF using Android's print dialog.

## Project structure

- `index.html` - original standalone HTML invoice.
- `app/src/main/assets/index.html` - same invoice HTML used inside Android app (with Android PDF bridge).
- `app/src/main/java/com/example/invoiceapp/MainActivity.kt` - hosts the WebView and triggers Android print-to-PDF.

---

## Build app **without Android Studio**

You can build this app from terminal only.

### Option 1: Build on your machine (CLI only)

### 1) Install prerequisites

- Java 17 (JDK)
- Gradle 8+
- Android command line tools (`sdkmanager`)

### 2) Set Android SDK path

Set one of these:

- Environment variable `ANDROID_SDK_ROOT`
- OR create `local.properties` in project root:

```properties
sdk.dir=/absolute/path/to/Android/Sdk
```

### 3) Install required Android SDK packages

```bash
sdkmanager "platform-tools" "platforms;android-35" "build-tools;35.0.0"
```

### 4) Build debug APK

```bash
gradle assembleDebug
```

APK output:

```text
app/build/outputs/apk/debug/app-debug.apk
```

---

### Option 2: Build in GitHub (no local Android setup)

A GitHub Actions workflow is included at:

- `.github/workflows/android-build.yml`

How to use:

1. Push this repo to GitHub.
2. Open **Actions** tab.
3. Run **Build Android APK** workflow.
4. Download artifact `app-debug-apk`.

This gives you `app-debug.apk` without installing Android Studio locally.

---

## How PDF generation works

- The HTML button calls `generatePdf()`.
- In Android app, `generatePdf()` forwards to `AndroidBridge.generatePdf()`.
- Native code opens Android Print framework so the user can choose **Save as PDF**.
