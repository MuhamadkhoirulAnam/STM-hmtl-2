# STM COMPANY Android WebView

Android wrapper for `https://devdesk.my.id`. PHP and MySQL remain on the hosting server.

## Build with GitHub Actions
1. Create a GitHub repository (or a separate branch/repository for this app).
2. Upload the complete contents of this ZIP, preserving `.github/workflows/build-apk.yml`.
3. For Firebase, download the Android `google-services.json` for package `com.stmcompany.app` and place it at `app/google-services.json`.
4. Commit to `main`, then open **Actions → Build STM COMPANY APK**.
5. Download artifact `stm-company-debug-apk` from a successful workflow run.

## Firebase setup
- Firebase Android app package must exactly match `com.stmcompany.app`.
- Add `app/google-services.json`; this project conditionally applies the Google Services Gradle plugin only when the file exists.
- FCM receive service and Android 13+ notification permission are included.
- This does not yet send device tokens to the PHP server or implement the admin send interface. Those require backend endpoint and secure FCM HTTP v1 service-account credentials on the server.
- Keep the Firebase service-account private key outside the repository and public web root. Never put it in the APK or GitHub source.

## Notes
- The workflow installs Android SDK packages explicitly; it does not request the obsolete package named `tools`.
- Debug APK is for testing. Configure release signing securely with GitHub Actions secrets before public distribution.
- WebView allows navigation within `devdesk.my.id`; other hosts open in the external browser.
- Test login, uploads, downloads, file chooser, OAuth redirects, and payment flows on real devices. File upload/download and OAuth may need additional native WebChromeClient/deep-link handling.
