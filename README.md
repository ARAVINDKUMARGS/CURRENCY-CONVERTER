# Global Currency Converter
### Institutional-Grade Real-Time Foreign Exchange Engine & Analytics Dashboard

> **SpireX Foundation Internship • Task 7 Submission**  
> **Date:** 12 November 2026  
> **Submission Deadline:** 13 November 2026, 7:00 PM  
> **Status:** Production-Ready / Fully Compliant  

---

## 📌 Executive Summary

**Global Currency Converter** is an institutional-grade, multi-functional financial technology (Fintech) web application developed exclusively using **HTML5, CSS3, and Vanilla JavaScript (ES6+)**. Built from the ground up without third-party UI frameworks (no React, Angular, Vue, Bootstrap, or Tailwind), the platform provides real-time mid-market foreign exchange conversion across **160+ world currencies**, interactive historical trend analytics, multi-currency portfolio conversion, a multi-item travel and invoice calculator, automatic browser locale detection, and full offline resilience via `localStorage`.

---

## 🚀 Key Features

### 1. Core Conversion Engine
- **160+ Supported Currencies:** Complete ISO 4217 database containing official currency codes, names, symbols, and high-definition country flag mappings (via FlagCDN with resilient text fallbacks).
- **Real-Time Spot Rates:** Instant conversion calculated against live reference market rates.
- **Accurate Decimal Precision:** Formatted using `Intl.NumberFormat` with adaptive decimal scaling (up to 6 decimal places for high-denomination and micro-value pairs).
- **Direct & Inverse Rates:** Real-time dual display (e.g., `1 USD = 0.9215 EUR` and `1 EUR = 1.0852 USD`).
- **Interactive Quick Amount Selection:** 1-click pills for `100`, `500`, `1,000`, `5,000`, and `10,000`.
- **Instant Currency Swap:** Animated 180° rotation button and one-click reverse conversion button.
- **Input Validation & Sanitization:** Real-time number checks, protection against negative numbers, NaN values, and input clearing.

### 2. Searchable Currency Modal
- Instant multi-field filtering by **currency code** (e.g., `USD`, `INR`), **country name** (e.g., `Japan`, `Canada`), or **currency title** (e.g., `Rupee`, `Pound`).
- Tabbed organization: **All Currencies (160+)**, **Popular Majors (15)**, and **⭐ Bookmarked Favorites**.
- Keyboard navigation: Accessible modal focus, `Esc` to close, and `/` shortcut to open.

### 3. Historical Trends & Interactive Charting
- **Timeframe Selector:** Switch seamlessly between `7 Days`, `1 Month`, `6 Months`, and `1 Year`.
- **Chart.js Powered Visualization:** Smooth cubic spline interpolation, responsive tooltips, and directional color gradients (Emerald Green for upward trends, Rose Red for depreciations).
- **Key Trend Metrics:** Period Net Change percentage (`+0.48%`), Period High, Period Low, and Period Mean Average.
- **Dual Data Source:** European Central Bank (ECB) official feeds via Frankfurter API, backed by an indicative historical calculation model for non-ECB currencies.

### 4. Advanced Portfolio & Tooling
- **Multi-Currency Simultaneous Converter:** Convert a single base amount into 8+ world currencies concurrently in a responsive card grid with dynamic currency add/remove capability.
- **Multi-Amount Currency Calculator:** Add multiple invoice or travel expense items (e.g., Hotel, Transport, Meals) in diverse foreign currencies and sum them into a single consolidated currency.
- **Market Watchlist & Live Ticker:** Animated marquee ticker tape and live major currency pairs table with real-time inverse rates, 24-hour shift indicators, and 1-click "Convert" loading.

### 5. Resiliency, Persistence & Accessibility
- **Automatic Browser Locale Detection:** Automatically detects visitor country and locale (e.g., `en-IN` → `INR`) with a non-intrusive confirmation banner.
- **Conversion History:** Persistent audit log saved in `localStorage` with relative timestamps, 1-click reload into converter, individual deletion, and batch clear.
- **Pinned Favorites:** Bookmark any currency pair with `localStorage` persistence and quick-switch chips.
- **Offline Mode & Error Recovery:** Automatic local storage snapshot caching. If network connectivity drops, the app seamlessly switches to cached rates and displays an informative banner with a retry trigger.
- **Dark & Light Mode:** Custom CSS variables with persistent preference storage and system color-scheme sync.
- **Clipboard & Native Sharing:** Instant copy of converted results and Web Share API integration.
- **Keyboard Shortcuts:**
  - <kbd>S</kbd> : Swap source & destination currencies
  - <kbd>R</kbd> : Refresh exchange rates
  - <kbd>/</kbd> : Open currency search modal
  - <kbd>Esc</kbd> : Close open modal

---

## 📂 Project Structure

```
Currency-Converter/
│
├── index.html          # Semantic HTML5 structure & accessibility attributes
├── style.css           # Premium fintech styling, CSS variables, dark/light themes
├── script.js           # Vanilla ES6+ application logic, API client, Chart.js engine
├── README.md           # Comprehensive project documentation & test cases
└── assets/
    └── favicon.svg     # Brand vector favicon
```

---

## 🌐 API Architecture & Methodology

The application connects to **100% free, public exchange rate APIs** requiring zero private credentials or paid subscriptions:

### 1. Primary Exchange Provider: Open ExchangeRate-API
- **Endpoint:** `https://open.er-api.com/v6/latest/{BASE_CURRENCY}`
- **Coverage:** 160+ fiat currencies worldwide.
- **Format:** JSON response containing ISO 4217 rate mappings, UTC last update timestamp, and next scheduled sync timestamp.
- **Rate Classification:** Mid-market reference rates (zero retail spread).

### 2. Secondary Historical Provider: Frankfurter API (ECB Engine)
- **Endpoint:** `https://api.frankfurter.dev/v1/{START_DATE}..{END_DATE}?base={FROM}&symbols={TO}`
- **Coverage:** Official European Central Bank (ECB) reference rate time series.
- **Format:** Chronologically ordered date-indexed rate objects utilized directly by the Chart.js visualizer.

### 3. Multi-Tier Fallback & Offline Architecture
```
[User Action / Base Currency Change]
              │
              ▼
   [Check Memory / Local Cache]  ── (Fresh < 20m) ──> [Render UI]
              │ (Stale / Force)
              ▼
 [Primary: Open ExchangeRate-API] ── (Success) ──────> [Cache & Render]
              │ (Failed / Timeout)
              ▼
 [Secondary: Frankfurter API]    ── (Success) ──────> [Cache & Render]
              │ (Failed / Offline)
              ▼
 [Local Storage Cache Snapshot]  ── (Available) ────> [Render with Offline Banner]
              │ (Empty Storage)
              ▼
 [Built-in Baseline Dataset]     ── (Always Valid) ─> [Safe Normalization & Render]
```

---

## 💻 How to Run the Project in VS Code

### Method 1: Using VS Code "Live Server" Extension (Recommended)
1. Open **Visual Studio Code**.
2. Click **File > Open Folder...** and select the `currency converter` folder.
3. In the Extensions tab (`Ctrl + Shift + X`), search for and install **Live Server** (by *Ritwick Dey*).
4. Right-click on [index.html](file:///c:/Users/Admin/currency%20converter/index.html) in the file explorer.
5. Select **"Open with Live Server"** (or click **Go Live** in the bottom status bar).
6. The app will open in your default browser at `http://127.0.0.1:5500`.

### Method 2: Using Python's Built-in HTTP Server
If you have Python installed, open the terminal in the project directory and run:
```bash
python -m http.server 8000
```
Then navigate to `http://localhost:8000` in any web browser.

### Method 3: Using Node.js `npx serve`
```bash
npx serve .
```
Navigate to the URL displayed in the terminal output.

### Method 4: Direct Browser Execution
Double-click [index.html](file:///c:/Users/Admin/currency%20converter/index.html) to open it directly in Google Chrome, Microsoft Edge, Brave, or Mozilla Firefox via the `file://` protocol. All core features and offline fallback operate cleanly.

---

## 🧪 Testing Instructions & Test Cases

| Test Case ID | Test Objective | Procedure / Input | Expected Result | Pass/Fail |
| :--- | :--- | :--- | :--- | :--- |
| **TC-01** | Standard Conversion | Enter `1000`, select `USD` → `EUR` | Converted amount displays correctly (e.g. `~920.00 EUR`) with direct & inverse rates | **PASS** |
| **TC-02** | Quick Amount Pills | Click the `5000` pill | Input updates to `5000`, pill highlights, result recalculates instantly | **PASS** |
| **TC-03** | Currency Swap | Click the swap button or press <kbd>S</kbd> | `from` and `to` swap with smooth rotation animation, rates re-fetch | **PASS** |
| **TC-04** | Search Filtering | Open modal, search `"Yen"` or `"JPY"` | Japanese Yen displays as top match with flag and symbol | **PASS** |
| **TC-05** | Input Validation | Enter `-500` or clear input | Red helper text warns invalid amount; result resets gracefully to `0.00` | **PASS** |
| **TC-06** | Historical Chart Range | Click `7D`, `1M`, `6M`, `1Y` buttons | Chart re-renders with corresponding time points, period high/low/average update | **PASS** |
| **TC-07** | Multi-Currency Portfolio | Change base amount to `250` | All 8+ cards update their converted amounts in real time | **PASS** |
| **TC-08** | Currency Calculator | Add an expense row of `150 EUR` and `200 USD` to `INR` | Correct aggregated sum converted to target currency | **PASS** |
| **TC-09** | Clipboard Copy | Click "Copy Amount" button | Converted text copied to clipboard with green toast notification feedback | **PASS** |
| **TC-10** | LocalStorage Persistence | Add favorite currency, convert, reload browser | Bookmarked favorites and conversion history persist across page reloads | **PASS** |
| **TC-11** | Offline Resiliency | Disconnect WiFi or inspect DevTools Offline mode | Amber banner appears: "Offline Fallback: Displaying cached rates"; no crash | **PASS** |
| **TC-12** | Theme Switching | Click Sun/Moon icon in navigation | Instant toggle between Light & Dark themes; Chart canvas updates dynamically | **PASS** |

---

## 📤 GitHub Upload Instructions

To upload this project to your GitHub account:

1. **Initialize Git Repository:**
   ```bash
   git init
   git add .
   git commit -m "feat: SpireX Foundation Task 7 - Global Currency Converter"
   ```

2. **Create Remote Repository on GitHub:**
   - Log into [GitHub](https://github.com).
   - Click the **+** icon in the upper-right corner and select **New repository**.
   - Set repository name: `currency-converter` (or `global-currency-converter`).
   - Leave "Add a README" **unchecked** (we already have a complete one).
   - Click **Create repository**.

3. **Link and Push:**
   ```bash
   git branch -M main
   git remote add origin https://github.com/<YOUR-USERNAME>/<YOUR-REPO-NAME>.git
   git push -u origin main
   ```

---

## 🚀 Deployment Instructions (Free Hosting)

### Option 1: GitHub Pages (Recommended)
1. Go to your repository on GitHub.
2. Click the **Settings** tab.
3. In the left navigation, scroll to the **Code and automation** section and click **Pages**.
4. Under **Build and deployment > Source**, select **Deploy from a branch**.
5. Under **Branch**, select `main` and folder `/ (root)`. Click **Save**.
6. Within 1–2 minutes, your website will be live at:
   `https://<YOUR-USERNAME>.github.io/<YOUR-REPO-NAME>/`

### Option 2: Netlify
1. Go to [Netlify](https://www.netlify.com) and log in.
2. Drag and drop your `currency converter` folder into the Netlify drop zone.
3. Netlify will deploy your application instantly with a free HTTPS URL.

### Option 3: Vercel
1. Install Vercel CLI: `npm install -g vercel` or link your GitHub repository on [Vercel](https://vercel.com).
2. Run `vercel` in your project folder and follow the prompts.

---

## 📋 SpireX Foundation Task 7 Compliance Checklist

- [x] **Strict Tech Stack:** HTML5, CSS3, and Vanilla JavaScript (ES6+) only.
- [x] **Zero Frameworks:** No React, Angular, Vue, Bootstrap, or Tailwind CSS.
- [x] **100% Free Resources:** Free APIs only; no paid subscriptions; no private keys in frontend.
- [x] **160+ World Currencies:** Complete ISO dataset with country flags and symbols.
- [x] **Real-Time Exchange Rates:** Live fetch from Open Exchange Rates and Frankfurter ECB.
- [x] **Validation & Error Handling:** Comprehensive input validation, visual error states, and retry options.
- [x] **Fintech UI/UX:** Glassmorphism, gradients, clean typography, micro-interactions, and responsive layout.
- [x] **Light & Dark Theme:** Full color-token support with persistent preference.
- [x] **Historical Trends:** Interactive Chart.js charts with 7D, 1M, 6M, and 1Y ranges, plus high/low/average analytics.
- [x] **Multi-Currency Converter:** Real-time multi-target grid with dynamic add/remove.
- [x] **Multi-Amount Calculator:** Multi-line expense breakdown tool.
- [x] **Local Storage Support:** Favorites and recent conversion history saved locally.
- [x] **Offline Resilience:** Seamless fallback to cached rates with timestamp indicator.
- [x] **Keyboard Accessibility:** Shortcuts (`S`, `R`, `/`, `Esc`) and full ARIA compliance.

---

**Developed for the SpireX Foundation Internship Program • Task 7**  
*Academic & Demonstration Project — 12 November 2026*
#   C U R R E N C Y - C O N V E R T E R  
 