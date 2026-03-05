# Invoice Android App

This repository now contains an Android app that embeds your existing `index.html` invoice UI in a `WebView`, lets users fill the form, and generates a PDF through Android's print dialog.

## Project structure

- `index.html` - original standalone HTML invoice.
- `app/src/main/assets/index.html` - same invoice HTML used inside Android app (with Android PDF bridge).
- `app/src/main/java/com/example/invoiceapp/MainActivity.kt` - hosts the WebView and triggers Android print-to-PDF.

## Build APK

Prerequisites:

- Android SDK installed
- `ANDROID_SDK_ROOT` set (or `local.properties` with `sdk.dir=...`)

Build debug APK:

```bash
gradle assembleDebug
```

If successful, APK path:

`app/build/outputs/apk/debug/app-debug.apk`

## How PDF generation works

- The HTML button calls `generatePdf()`.
- In Android app, `generatePdf()` forwards to `AndroidBridge.generatePdf()`.
- Native code opens Android Print framework so the user can choose **Save as PDF**.
