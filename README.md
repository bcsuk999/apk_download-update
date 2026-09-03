# SunPay APK Updates

This folder contains the files published in the separate public GitHub repository:

https://github.com/bcsuk999/apk_download-update

## Files

- `version.json` contains the latest app version and APK download URL.
- `app-release.apk` is the arm64-v8a release APK.

## Release a new update

1. Increase the version and build number in the root `pubspec.yaml`.
2. Build only arm64-v8a:

```powershell
flutter build apk --release --target-platform android-arm64
```

3. Copy the new APK into this folder as `app-release.apk`.
4. Increase `build` in `version.json`.
5. Copy `version.json` and `app-release.apk` to the `apk_download-update` GitHub repository.
6. Commit and push both files.

The app checks `version.json`, downloads the APK, shows download progress, and opens Android's installation prompt.
