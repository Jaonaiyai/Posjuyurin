# LoyPOS – Android Point of Sale

An offline POS app for Android phones and tablets, modeled on the core of Loyverse POS.
Kotlin · Jetpack Compose (Material 3) · Room (SQLite). Minimum Android 8.0.

## Features

| Area | What it does |
|---|---|
| **Sale** | Item tiles with colors, category filter, search by name / SKU / barcode, ticket with +/− quantity, discount presets (5–20%), VAT included or added, charge by Cash (with quick-cash buttons and change), Card, or QR/PromptPay |
| **Receipts** | Full sales history, search by number, receipt view (58 mm printer width), share/print via any app, full refund (stock is returned) |
| **Items** | Add / edit / delete items: price, cost, category, SKU, barcode, color, stock tracking with low-stock warning. Categories with colors |
| **Reports** | Today / 7 days / 30 days: net & gross sales, refunds, receipt count, average sale, VAT, sales-by-hour or by-day chart, payment-type breakdown, top 10 items |
| **Settings** | Store name, address, receipt footer, currency symbol (default ฿), tax rate (default 7%), prices-include-tax switch, export all sales to CSV |

Demo items (drinks, food, snacks) are added on first launch so you can try it immediately — delete or edit them in **Items**.

## Get the APK – option A: Android Studio (on your computer)

1. Install **Android Studio** (free): https://developer.android.com/studio
2. Unzip this project, then **File → Open** and choose the `LoyPOS` folder. Wait for "Gradle sync" to finish (first time downloads ~1 GB).
3. Plug in your Android device with **USB debugging** on, and press ▶ **Run** — the app installs directly.
4. To make an APK file: **Build → Build App Bundle(s) / APK(s) → Build APK(s)**.
   The file appears at `app/build/outputs/apk/debug/app-debug.apk`. Copy it to any phone or tablet and open it to install
   (allow "Install unknown apps" when Android asks).

## Get the APK – option B: build in the cloud with GitHub (no install needed)

1. Create a free GitHub account and a new repository.
2. Upload all files of this folder (including the hidden `.github` folder).
3. Open the **Actions** tab → the "Build APK" job runs automatically (about 5 minutes).
4. Open the finished run → download **LoyPOS-apk** → unzip → install `app-release.apk` on your device.

## Project structure

```
app/src/main/java/com/loypos/app/
├── MainActivity.kt        app entry point
├── PosViewModel.kt        cart, checkout, refunds, reports, CSV export, demo data
├── Format.kt              money / quantity / date formatting, color palette
├── data/
│   ├── Entities.kt        Category, Item, Receipt, ReceiptLine tables
│   ├── PosDao.kt          database queries + checkout/refund transactions
│   ├── PosDatabase.kt     Room database
│   └── SettingsStore.kt   store settings (SharedPreferences)
└── ui/
    ├── PosApp.kt          bottom navigation
    ├── SaleScreen.kt      register, ticket, payment dialog
    ├── ReceiptsScreen.kt  history, receipt view, refund
    ├── ItemsScreen.kt     items & categories editor
    ├── ReportsScreen.kt   dashboard
    ├── SettingsScreen.kt  settings & export
    └── Theme.kt           colors (light/dark)
```

## Notes before using it in a real shop

- The release APK is signed with the debug key so it installs easily. Create your own signing key
  (**Build → Generate Signed Bundle / APK**) before publishing on Google Play.
- Data lives only on the device. Use **Settings → Export CSV** regularly as a backup.
- Good next additions: Bluetooth thermal printer (ESC/POS), camera barcode scanning, customers & loyalty points,
  employees with PIN login, shifts / cash drawer, item variants and modifiers, cloud sync.
