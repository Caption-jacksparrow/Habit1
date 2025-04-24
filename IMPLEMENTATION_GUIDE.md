# GitHub Actions APK Build Implementation Guide

This guide provides step-by-step instructions for implementing GitHub Actions to build your HabitTune Android APK automatically.

## Prerequisites

- A GitHub account
- Your HabitTune Flutter project
- Basic knowledge of Git

## Implementation Steps

### 1. Set Up Your GitHub Repository

1. Create a new GitHub repository or use an existing one
2. Push your HabitTune project to the repository
3. Ensure your repository has the proper Flutter project structure

### 2. Add Configuration Files

Add all the configuration files provided in this package to your repository, maintaining the directory structure:

- `.github/workflows/flutter-build.yml` - GitHub Actions workflow configuration
- `android/` directory with all build configuration files
- `pubspec.yaml` with proper dependencies

### 3. Generate Android Keystore

For signing your APK, you'll need a keystore:

```bash
keytool -genkey -v -keystore keystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload
```

When prompted:
- Enter a secure password for the keystore
- Provide information about your organization
- Remember the alias name and passwords used

### 4. Set Up GitHub Secrets

In your GitHub repository:
1. Go to Settings > Secrets and variables > Actions
2. Add the following secrets:

   - `KEYSTORE_BASE64`: Your keystore file encoded as base64
     ```bash
     base64 -i keystore.jks
     ```
     Copy the output as the secret value
     
   - `KEYSTORE_PASSWORD`: The password you used for the keystore
   - `KEY_ALIAS`: The alias you used when creating the keystore (e.g., "upload")
   - `KEY_PASSWORD`: The password for the key alias

### 5. Trigger the Workflow

The workflow will automatically run when:
- You push to the main branch
- You create a pull request to the main branch
- You manually trigger it from the Actions tab

### 6. Access Your Built APK

After the workflow runs successfully:
1. Go to the Actions tab in your repository
2. Click on the completed workflow run
3. Download the APK from the Artifacts section

For releases (pushes to main):
1. Go to the Releases section of your repository
2. Find the latest release
3. Download the APK attached to the release

## Troubleshooting

- **Build Failures**: Check the workflow logs for specific error messages
- **Signing Issues**: Verify your keystore secrets are correctly set up
- **Missing Dependencies**: Ensure your pubspec.yaml includes all required dependencies

## Customization

- Update app package name in `AndroidManifest.xml` and `build.gradle` files
- Modify Flutter version in the workflow file if needed
- Add custom app icons to the mipmap directories
- Update app version in pubspec.yaml

## Maintenance

- Update the Flutter version in the workflow file as new versions are released
- Regularly update dependencies in pubspec.yaml
- Consider implementing automated version increments based on git tags or commit count
