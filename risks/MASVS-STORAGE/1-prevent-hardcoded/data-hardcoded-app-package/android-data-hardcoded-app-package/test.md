---
title: Sensitive Data Hardcoded in the App Package
alias: data-hardcoded-app-package
platform: [android, ios]
profiles: [L1, L2]
mappings:
  - masvs-v2: [MASVS-STORAGE-1]
  - mstg-v2: [STORAGE-1]

---

## Purpose

Ensure that sensitive data, including cryptographic keys and authentication material, is not hardcoded in the app package, source code, or compiled binaries.

## Testing Approach

### Static Analysis

1. **Inspect Source Code, Configuration Files, and Binaries:**
   - **Source Code:** Search the source code for sensitive data patterns (e.g., passwords, API keys, cryptographic keys).
     - Keywords to search:
       - `password`
       - `apikey`
       - `secret`
       - `key`
     - Example Commands:
       ```bash
       grep -R "password" src/
       grep -R "apikey" src/
       ```
   - **Configuration Files:** Review platform-specific configuration files for sensitive data.
     - Android: `res/values/strings.xml`, `res/raw/`
     - iOS: `.plist` files, `Info.plist`
   - **Third-party Libraries and SDKs:** Investigate external dependencies for potential hardcoded data.

2. **Decompile and Analyze Binaries:**
   - **Android:**
     - Use Apktool or JADX to decompile the APK file.
     - Inspect the `.smali` or `.java` files for sensitive data patterns.
   - **iOS:**
     - Extract the IPA contents or use tools like Hopper or class-dump to analyze the binary.
     - Inspect the Objective-C classes for hardcoded sensitive data.

### Dynamic Analysis

1. **Monitor API Requests:**
   - Run the app and observe network traffic using tools like Burp Suite or OWASP ZAP.
   - Monitor for sensitive data leakage in API requests.

2. **Monitor Log Outputs:**
   - Review application logs for any sensitive data that may have been accidentally logged.
   - Example command (Android):
   ```bash
   adb logcat -d | grep "password"
