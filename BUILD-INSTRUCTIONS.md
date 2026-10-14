# Building the APK

## Option A: Android Studio (recommended)
1. Install Android Studio (Koala or newer; it bundles JDK 17+) and let it install the Android SDK 34.
2. **File → Open** the `BF-Brothers-Attendance` folder. Wait for Gradle sync (needs internet once, to download dependencies).
3. **Build → Generate Signed App Bundle / APK → APK**, create a key store (see "Signing"), choose **release**, finish.
4. The APK appears in `app/release/`. For a quick unsigned-key test: **Build → Build APK(s)** gives a debug APK in `app/build/outputs/apk/debug/`.

## Option B: Command line
```
gradle wrapper --gradle-version 8.9     # once, creates gradlew
./gradlew assembleRelease               # Windows: gradlew.bat assembleRelease
```
Output: `app/build/outputs/apk/release/app-release.apk`

## Signing and updates
- Create a key: `keytool -genkeypair -v -keystore bf-release.jks -alias bf-release -keyalg RSA -keysize 2048 -validity 10000`
- Copy `keystore.properties.example` to `keystore.properties`, fill it in. `assembleRelease` then signs with your key.
- Without `keystore.properties`, the release build falls back to Android's **debug key** so it still installs. That is fine for
  personal testing, but debug keys are not stable across computers.
- **Keep `bf-release.jks` and its passwords safe and backed up.** Android only installs an update over an existing install if it is
  signed with the *same* key. If you lose the key, you must uninstall (which deletes the data) to install a new version, so export a backup first.
- Never share the key store or `keystore.properties` (both are in `.gitignore`; don't put them in a distributed ZIP).

## Updating the app without losing data
Increase `versionCode` and `versionName` in `app/build.gradle.kts`, sign with the same key, and install over the old app.
If you change the database structure, bump `version` in `AppDatabase` **and add a Room `Migration`**. Destructive migration is intentionally not enabled.

## Versions used
AGP 8.5.2, Kotlin 2.0.20, KSP 2.0.20-1.0.25, Gradle 8.9, Compose BOM 2024.09.00, Room 2.6.1, Navigation 2.8.0. minSdk 26, target/compile 34.
These were chosen to be mutually compatible but have not been compiled here; if Studio suggests upgrades, accept them.
