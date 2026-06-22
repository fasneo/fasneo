# Fasneo Android App (WebView)

Ye ek Android WebView app hai jo **https://fasneo.com** ko load karta hai.

## Features
- Pull to refresh
- Back button navigation (WebView history ke saath)
- Loading progress bar
- Splash screen with logo
- No-internet screen + Retry button
- File download support (DownloadManager se)
- External links (jaise payment gateway, WhatsApp) device ke browser/app mein khulenge

---

## 🚀 APK Build Karne Ke 3 Tarike

### Option 1: GitHub Actions se (Android Studio install karne ki zaroorat nahi)

1. Ye poora folder GitHub repository mein push karo.
2. GitHub repo mein jao → **Actions** tab → "Build APK" workflow apne aap chalega.
3. Workflow complete hone ke baad, **Artifacts** section mein `fasneo-debug-apk` milega — usme `app-debug.apk` hai.
4. APK download karo aur apni website pe daal do.

> Note: Ye **debug APK** banata hai (testing ke liye sahi hai). Play Store pe daalne ke liye ya production-ready signed APK ke liye Option 2 use karo.

### Option 2: Android Studio se (Recommended for production/signed APK)

1. [Android Studio](https://developer.android.com/studio) install karo.
2. **File → Open** → ye `FasneoApp` folder select karo.
3. Gradle sync hone do (pehli baar thoda time lagega, internet chahiye).
4. Top menu mein **Build → Generate Signed Bundle / APK** select karo.
5. **APK** choose karo → naya keystore banao (ya existing use karo) → **release** build select karo.
6. Build complete hone ke baad APK `app/release/` folder mein milega.

### Option 3: Command line se (agar Android SDK already installed hai)

```bash
cd FasneoApp
./gradlew assembleDebug
```

APK yahan milega: `app/build/outputs/apk/debug/app-debug.apk`

---

## 📝 Important: Apni Site Pe APK Daalne Se Pehle

1. **Signed Release APK banao** (sirf debug APK mat use karo production ke liye) — Option 2 follow karo.
2. App ka icon already `A2.png` logo se generate ho gaya hai (sab densities mein).
3. Agar website ka URL change karna ho, toh edit karo:
   `app/src/main/java/com/fasneo/app/MainActivity.kt` mein `siteUrl` variable.
4. Package name `com.fasneo.app` hai — ye unique identity hai, isse baad mein change mat karna agar Play Store pe daalna ho.

## 🔧 Customization

| Kya change karna hai | Kahan |
|---|---|
| Website URL | `MainActivity.kt` → `siteUrl` |
| App name | `res/values/strings.xml` → `app_name` |
| Colors | `res/values/colors.xml` |
| App icon | `res/mipmap-*/ic_launcher.png` (logo se already generated) |
| Splash delay | `SplashActivity.kt` → `splashDelayMillis` |

## ⚠️ APK Apni Website Pe Direct Download Ke Liye Daalne Se Pehle

- Users ko APK install karne ke liye "Install from unknown sources" allow karna padega (Android security ki wajah se), kyunki ye Play Store se nahi aa rahi.
- Behtar long-term solution: Play Store pe publish karo (Google Play Console account chahiye, one-time $25 fee).
- Apni site pe ek note add karo: "Is APK ko install karne ke liye apni device settings mein 'Unknown Sources' allow karein."
