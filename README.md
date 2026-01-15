---

# 🖥️ AutomationExpert's Enterprise System Inventory Dashboard

A high-performance, professional system monitoring dashboard designed for **GitHub Pages**. This tool visualizes infrastructure data gathered via automation (PowerShell/Python), providing a "single pane of glass" view into system health, uptime, and environment status.

---

## 🚀 Key Features

* **PWA Ready (Installable):** Install the dashboard as a native desktop or mobile application. Includes offline-ready support via Service Workers.
* **Intelligent Data Mapping:** Use `mapping.json` to rename technical JSON keys (e.g., `Restart Authorization`) to professional headers (e.g., `Restart Auth`) and control column order.
* **Live Health Tracking:** Visual badges for system checks () with smart color-coding (Red < 50%, Orange < 80%, Yellow < 100%, Green = 100%).
* **Numeric Logic Filtering:** Advanced search allowing `>`, `>=`, `<`, and `<=` operations. The engine automatically strips units like "GB" or "Days" for mathematical accuracy.
* **Disk Usage Visualizer:** Dynamic progress bars for `FreeDiskSpace` that trigger a red alert when space drops below 10GB.
* **Uptime Monitoring:** Critical threshold alerts (Red for  days, Orange for  days) to identify systems needing a reboot.
* **Universal Keyword Engine:** Automatic color-coding for status keywords (*Authorized, Pending, Production, None, Denied*) across all columns.
* **Enterprise Tooling:**
* **CSV Export:** Generate reports of your currently filtered view.
* **Dark Mode:** Full high-contrast dark theme for 24/7 NOC operations.
* **Stateless API:** Access raw machine data via URL parameters (`?format=json`).



---

## 🔄 Automation Workflow

This dashboard is designed to be fully hands-off:

1. **Collection:** A scheduled PowerShell script runs on your internal network to gather server stats.
2. **Payload:** The script generates a `data.json` file.
3. **Commit:** A GitHub Action (or API call) pushes the `data.json` to your repository.
4. **Deployment:** GitHub Pages automatically refreshes the live dashboard.

---


## 🚀 Key Features

* **Direct Numeric Logic:** Explicitly define which columns support mathematical filters ($>$, $<$, etc.) via `mapping.json`.
* **System Theme Support:** Automatically respects your OS Light/Dark mode settings using CSS media queries.
* **Smart Unit Handling:** Built-in sanitization strips "Days" or "GB" from values during math operations while keeping them visible in the UI.
* **PWA Enabled:** Fully installable as a standalone app on desktop and mobile.
* **Keyword Intelligence:** Automatic color-coded badges for keywords like *Pending, Production, Authorized,* and *Denied*.
* **Stateless Architecture:** Fully client-side; no database required. Powered by `data.json`.

---

## ⚙️ Configuration Guide

### `mapping.json` (Required)

Defines which fields to show and their display names.

```json
{
  "Name": "System Name",
  "Uptime": "Uptime",
  "FreeDiskSpace": "Disk Free",
  "ChecksPassed": "Health Status",
  "Restart Authorization": "Auth Status"
}

```

### `config.json` (Required)

Controls branding and footer resources.

```json
{
  "dashboardTitle": "AutomationExpert Inventory",
  "footer": {
    "orgName": "AutomationExpert Team",
    "description": "Internal monitoring for core services.",
    "resources": [
      { "label": "Wiki", "url": "https://internal.wiki" }
    ]
  }
}

```

---

## 🤖 API & URL Filtering

Retrieve specific data or filter views via URL:

* **JSON API:** `?name=System-1&format=json` (Returns pure JSON for scripts).
* **UI Filter:** `?environment=Production` (Filters the table view automatically).

---

## 🛠️ Deployment Instructions

1. **Upload Files:** Push `index.html`, `manifest.json`, `sw.js`, `mapping.json`, and `data.json` to your repo.
2. **Enable Pages:**
* Navigate to **Settings > Pages**.
* Select **Deploy from a branch** (Main).
* Click **Save**.


3. **PWA Install:** Open the site in Chrome/Edge and click the **"Install App"** button in the header.

---

### 📈 Version Changelog

#### **v16.7 (Current)**
* **Feature:** Enhanced **Pagination** with options for 25, 50, 100, 500, and "Show All" (999k rows).
* **Fix:** Re-ordered `init()` lifecycle to ensure **URL Filters** and `?format=json` are processed correctly after configuration and data loads.
* **API:** Validated `format=json` for PowerShell `Invoke-RestMethod` compatibility; it now returns a raw string without HTML overhead.

#### **v16.5 (Current)**

* **Feature:** Switched to **Direct Numeric Logic**. Math operators (, , etc.) now only appear for fields explicitly listed in the `numericFields` array within `mapping.json`.
* **Fix:** Robust **System Theme Detection**. Updated CSS variables and media queries to correctly sync with OS dark/light mode settings on all devices.
* **Improvement:** Enhanced **Sanitize Logic** to automatically strip units like "Days" or "GB" during mathematical filtering and sorting while maintaining visibility in the table.

#### **v16.1 - v16.4**

* **Maintenance:** Resolved a bug where the theme selector would not save the user's preference correctly.
* **Feature:** Introduced the `__meta_config__` block in `mapping.json` to allow externalized configuration of app logic without touching the HTML source.
* **UI:** Added a "Systems Found" results counter and a modernized corporate footer with dynamic link support.

#### **v15.0**

* **Feature:** Added **PWA (Installable)** support, allowing the dashboard to be installed as a native desktop/mobile application.
* **Logic:** Integrated numeric operator filtering (, , , , ) for numeric data columns.
* **Visuals:** Re-implemented the 100/80/50 health badge color-coding system for `ChecksPassed`.

#### **v14.0**

* **Feature:** Dynamic Column Mapping introduced. Columns now follow the order and naming conventions defined in `mapping.json`.
* **Visuals:** Added Disk Usage progress bars with automatic red-alert thresholds for low space.

#### **v1.0 - v13.0**

* **Core:** Initial development of the dashboard core, global search engine, dark mode toggle, CSV export, and API-style URL parameter support.

---

<p align="center">Built with ❤️ for DevOps & System Administrators.</p>
