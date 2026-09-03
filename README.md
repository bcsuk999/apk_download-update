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
5. Open PowerShell in the project root and copy the files to a temporary clone of the update repository:

```powershell
if (Test-Path .apk_updates_repo) { Remove-Item -Recurse -Force .apk_updates_repo }
git clone https://github.com/bcsuk999/apk_download-update.git .apk_updates_repo
Copy-Item -Force "apk_updates\version.json", "apk_updates\app-release.apk" ".apk_updates_repo\"
```

6. Commit and push both files:

```powershell
Push-Location .apk_updates_repo
git add version.json app-release.apk
git commit -m "Release app update"
git push origin main
Pop-Location
Remove-Item -Recurse -Force .apk_updates_repo
```

The app will check the new `build` number the next time it opens.

The app checks `version.json`, downloads the APK, shows download progress, and opens Android's installation prompt.
