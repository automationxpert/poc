---

# 🖥️ AutomationExpert's Enterprise System Inventory Dashboard

A high-performance, professional system monitoring dashboard designed for **GitHub Pages**. This tool visualizes infrastructure data gathered via automation (PowerShell/Python), providing a "single pane of glass" view into system health, uptime, and environment status.

---

### 🚀 Key Features

* **Hybrid API Engine:** Professional HTML UI for humans and a direct `data.json` endpoint for automation scripts (PowerShell/Python).
* **Direct Numeric Logic:** Define math-capable columns in `mapping.json` to enable advanced filtering (, , etc.) for metrics like Uptime or Disk Space.
* **Deep Linking & UI State:** Share specific filtered views using URL parameters (e.g., `?Environment=Production`) that automatically configure the UI on load.
* **Smart Sanitization:** Built-in logic strips units like "Days" or "GB" during math operations and sorting while keeping them visible for the user.
* **Adaptive UX:** * **Theme Support:** Automatically respects OS Light/Dark mode settings.
* **PWA Ready:** Fully installable as a standalone application on Desktop and Mobile.
* **Stateless & Secure:** 100% client-side architecture with no database required; easily hosted on GitHub Pages or any static web server.

---

## 🔄 Automation Workflow

This dashboard is designed to be fully hands-off:

1. **Collection:** A scheduled PowerShell script runs on your internal network to gather server stats.
2. **Payload:** The script generates a `data.json` file.
3. **Commit:** A GitHub Action (or API call) pushes the `data.json` to your repository.
4. **Deployment:** GitHub Pages automatically refreshes the live dashboard.

---


## 🛠️ Automation & API Usage

Since this dashboard is hosted on a static environment (GitHub Pages), we use a **Hybrid API** strategy.

### 1. Manual User View (HTML)
To view the interactive dashboard, simply navigate to the root URL.
* **Filter via URL:** `index.html?Name=Server01`
* **JSON Redirect:** `index.html?format=json` (Redirects browser to raw data)

### 2. Scripting / PowerShell View (JSON)
For automation, point your scripts directly to the `data.json` file. This ensures you receive the correct `application/json` Content-Type header.

**PowerShell Example:**
```powershell
# Fetch the inventory as a native object
$uri = "[https://automationxpert.github.io/poc/data.json](https://automationxpert.github.io/poc/data.json)"
$inventory = Invoke-RestMethod -Uri $uri

# Example: Filter for systems with low disk space from the script
$inventory.Systems | Where-Object { [float]($_.FreeDiskSpace -replace 'GB','') -lt 10 } | Format-Table

```

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

#### **v16.10 (Current)**
* **Feature:** Enhanced **CSV Export** with dynamic filenames. Exported files now follow the naming convention `Inventory_Export_dd-MM-yyyy_hh-mm.csv` for better version tracking.

#### **v16.9**

* **API:** Formalized the **Hybrid API Strategy**. Redirects `?format=json` in browsers and provides direct `data.json` access for scripts.
* **UI:** Added **"Last Updated"** timestamp to the header, pulling dynamically from `data.json`.
* **Pagination:** Expanded options to include **25, 50, 100, 500, and "Show All"**.
* **Logic:** Enhanced URL parameter listener to support **Exact Match** mode automatically when a link is shared.

#### **v16.8**

* Implemented **Direct Numeric Logic** for mathematical filtering.
* Added **System Theme Detection** (Dark/Light mode) via CSS media queries.
* Re-implemented health badge color-coding (100/80/50 logic).

#### **v16.7**
* **Feature:** Enhanced **Pagination** with options for 25, 50, 100, 500, and "Show All" (999k rows).
* **Fix:** Re-ordered `init()` lifecycle to ensure **URL Filters** and `?format=json` are processed correctly after configuration and data loads.
* **API:** Validated `format=json` for PowerShell `Invoke-RestMethod` compatibility; it now returns a raw string without HTML overhead.

#### **v16.5**

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
