# 🖥️ Enterprise System Inventory Dashboard

A high-performance, professional system monitoring dashboard designed for **GitHub Pages**. This tool visualizes infrastructure data gathered via automation (PowerShell/Python), providing a "single pane of glass" view into system health, disk space, and environment status.
---

## 🚀 Key Features

* **Live Health Tracking:** Visual badges for system checks ($X/5$) with smart color-coding (Red < 50%, Orange < 80%, Yellow < 100%, Green = 100%).
* **Disk Usage Visualizer:** Dynamic progress bars for `FreeDiskSpace` that trigger a red alert when space drops below 10GB.
* **Smart Summary Cards:** Instant metrics for Total Systems, Critical Health, and Low Disk space. Clicking a card automatically filters the table.
* **Infrastructure Grouping:** Cluster systems by **Environment**, **Business Unit (BU)**, or **Tenant** for organized oversight.
* **Enterprise Tooling:** * **One-Click Copy:** Quickly copy Hostnames or Usernames to your clipboard.
    * **Maintenance Mode:** Manually flag systems as "In-Maintenance" (saved to browser `localStorage`).
    * **Universal Search:** Instant, case-insensitive search across all data fields.
* **Dark Mode Support:** Full high-contrast dark theme for 24/7 NOC operations.

---

## 🔄 Automation Workflow

This dashboard is designed to be fully hands-off. The recommended lifecycle is:



1.  **Collection:** A scheduled PowerShell script runs on your internal network to gather server stats.
2.  **Payload:** The script generates a `data.json` file including a `LastUpdated` timestamp.
3.  **Commit:** A GitHub Action (or API call) pushes the new `data.json` to the repository.
4.  **Deployment:** GitHub Pages automatically refreshes the live dashboard.

---

## 📂 Data Schema (`data.json`)

The dashboard dynamically renders headers based on your JSON keys. Your PowerShell script should output this structure:

```json
{
  "LastUpdated": "2026-01-14T10:30:00",
  "Systems": [
    {
      "Name": "Prod-Web-01",
      "Environment": "Production",
      "BU": "FinTech",
      "FreeDiskSpace": "45GB",
      "ChecksPassed": "5/5",
      "Username": "svc_admin",
      "Uptime": "120 Days"
    }
  ]
}
```

## 🛠️ Deployment Instructions

 * Upload Files: Push index.html and data.json to your GitHub Repository.
 * Enable Pages: * Navigate to Settings > Pages.
   * Select Deploy from a branch.
   * Select main (or your default branch) and / (root).
   * Click Save.
 * Configure LastUpdated: (Optional) Update the GITHUB_USER and GITHUB_REPO variables in the index.html script to enable the commit-history timestamp.
🚦 Monitoring Alerts
 * Stale Data: If the LastUpdated time in the JSON is more than 24 hours old, the timestamp in the header will pulse RED to warn that the automation may be failing.
 * Critical Health: Systems with less than 50% checks passed are automatically highlighted for immediate attention.
🖥️ URL Filtering
Share specific views with team members using URL parameters:
 * ?name=Server01 - Show specific server.
 * ?environment=Production - Show only production systems.
 * ?bu=Engineering - Show only engineering systems.
   
Built with ❤️ for DevOps & System Administrators.
