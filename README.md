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

## 📂 Configuration Files

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
  "dashboardTitle": "Ops-Center Inventory",
  "footer": {
    "orgName": "Global Infrastructure Team",
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

## 📈 Version Changelog

### **v16.0 (Latest)**

* **Unit Sanitization:** Mathematical filtering now works on fields containing text (strips "GB", "Days").
* **Universal Keyword Formatter:** Keywords like *Pending* or *Authorized* now automatically receive color badges.
* **Professional Footer:** Redesigned for a minimalist, high-end corporate aesthetic.

### **v15.0**

* **Numeric Operators:** Added `>`, `>=`, `<`, and `<=` filtering logic.
* **PWA Support:** Integrated Web App Manifest and Service Workers for desktop installation.

### **v14.0**

* **Dynamic Mapping:** Introduced `mapping.json` for field aliasing and ordering.
* **Alert Thresholds:** Added Uptime and Health percentage-based color logic.

### **v1.0 - v13.0**

* Initial dashboard development, Dark Mode, CSV Export, and Global Search implementation.

---

<p align="center">Built with ❤️ for DevOps & System Administrators.</p>
