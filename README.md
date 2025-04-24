# README.md - GitHub Actions APK Build Setup for HabitTune

This repository contains the necessary configuration files to build an Android APK for the HabitTune application using GitHub Actions.

## Setup Instructions

1. **Repository Structure**
   Ensure your repository has the following structure:
   ```
   your-repo/
   ├── .github/
   │   └── workflows/
   │       └── flutter-build.yml
   ├── android/
   │   ├── app/
   │   │   ├── build.gradle
   │   │   ├── proguard-rules.pro
   │   │   └── src/
   │   │       └── main/
   │   │           ├── AndroidManifest.xml
   │   │           ├── kotlin/
   │   │           │   └── com/
   │   │           │       └── example/
   │   │           │           └── habittune/
   │   │           │               └── MainActivity.kt
   │   │           └── res/
   │   │               ├── drawable/
   │   │               │   └── launch_background.xml
   │   │               ├── mipmap-*/
   │   │               └── values/
   │   │                   └── styles.xml
   │   ├── build.gradle
   │   ├── gradle.properties
   │   └── settings.gradle
   ├── lib/
   │   └── [your Dart files]
   ├── assets/
   │   ├── images/
   │   └── fonts/
   └── pubspec.yaml
   ```

2. **GitHub Secrets Setup**
   Add the following secrets to your GitHub repository:
   - `KEYSTORE_BASE64`: Your keystore file encoded as base64
   - `KEYSTORE_PASSWORD`: Password for your keystore
   - `KEY_ALIAS`: Alias of the key in your keystore
   - `KEY_PASSWORD`: Password for the key

3. **Generate a Keystore**
   If you don't have a keystore, generate one using:
   ```
   keytool -genkey -v -keystore android/app/keystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload
   ```

4. **Convert Keystore to Base64**
   ```
   base64 -i android/app/keystore.jks
   ```
   Copy the output and add it as the `KEYSTORE_BASE64` secret in GitHub.

## Workflow Details

The GitHub Actions workflow will:
1. Set up Java and Flutter environments
2. Install dependencies
3. Run tests
4. Build a release APK
5. Sign the APK using your keystore
6. Upload the APK as an artifact
7. Create a GitHub release with the APK (on push to main branch)

## Customization

- Update the app package name in `AndroidManifest.xml` and `build.gradle`
- Modify the Flutter version in the workflow file if needed
- Add custom icons to the `mipmap-*` directories
- Update the app version in `pubspec.yaml`
