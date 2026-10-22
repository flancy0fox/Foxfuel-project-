# 匯率口袋 — Android APK 自動編譯專案

此專案保留原先的匯率口袋 v49 介面和功能，並新增 GitHub Actions 自動編譯設定。**此 ZIP 不是 APK**；它會在 GitHub 的 Android 編譯環境產出可安裝的 `app-debug.apk`。此環境無法下載 Android SDK，因此無法在此直接編譯或驗證 APK。

## 不需在電腦安裝 Android Studio 的方法

1. 登入 GitHub，建立一個私人（Private）空白 repository。
2. 將 ZIP **解壓後的所有檔案和資料夾**上傳到 repository 根目錄，包含隱藏資料夾 `.github/workflows`。
3. 打開 GitHub repository 的 **Actions** 頁籤，選擇 **Build Android APK**，點選 **Run workflow**。第一次上傳到 `main` 分支時也可能自動啟動。
4. 等待綠色成功標記後，打開該次執行紀錄，在 **Artifacts** 下載 `currency-pocket-android-apk`，解壓取得 `app-debug.apk`。
5. 將 APK 傳到 Android 手機或平板，允許該來源安裝應用程式後安裝。

這是供個人測試/安裝的 **debug 簽署 APK**，不是正式商店發佈版。要在 Google Play 發佈，需要建立正式簽署金鑰並編譯 release AAB。首次建置需網路下載 npm、Gradle、Android SDK 依賴，GitHub Actions 可能因服務或版本變動而失敗；失敗時請查看 Actions 日誌。

## 本機編譯（已有 Android SDK 時）

```bash
npm install
npx cap add android
npx cap sync android
cd android
./gradlew assembleDebug
```

輸出位置：`android/app/build/outputs/apk/debug/app-debug.apk`。

**iPhone/iPad 不可安裝 APK**；iOS 仍需在 macOS/Xcode 環境編譯與簽署。
