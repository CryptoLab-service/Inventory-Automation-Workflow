# 📦 Inventory Automation Workflow with n8n

This repository contains a robust inventory management workflow built using [n8n](https://n8n.io), designed to automate stock monitoring, alerting, vendor communication, and logging. It integrates Google Sheets, Telegram, Slack, and Gmail to streamline operations and ensure timely restocking.

---

## 🧠 Workflow Summary

This workflow runs daily at 8 AM and performs the following:

1. **Fetches inventory data** from Google Sheets.
2. **Archives a snapshot** of the current inventory.
3. **Assigns priority levels** based on category and vendor.
4. **Validates data integrity** (SKU, Quantity, ReorderPoint).
5. **Checks alert timestamps** to avoid duplicate notifications.
6. **Filters low-stock items** and batches them for processing.
7. **Sends alerts** via Telegram for critical items.
8. **Places orders** via Slack and confirms them.
9. **Sends payment invoices** via Gmail.
10. **Logs all actions** to Google Sheets.
11. **Handles errors** gracefully with logging and optional notifications.

---

## 🗂️ Workflow Architecture

```mermaid
graph TD
    A[Schedule Trigger (8AM)] --> B[Get Inventory Log]
    B --> C[Archive Snapshot]
    C --> D[Assign Priority]
    D --> E[Data Validation]
    E --> F[Compare Timestamp]
    F --> G[Throttle Filter]
    G --> H[Filter Low Stock]
    H --> I[Loop Over Items]
    I --> J[Update Timestamp]
    I --> K[Map Priority Index]
    K --> L[Message Alert (Telegram)]
    I --> M[Order Placement (Slack)]
    M --> N[Order Confirmation (Slack)]
    N --> O[Payment Invoice (Gmail)]
    M --> P[Workflow Logs]
    N --> P
    O --> P
    M --> Q[Error Handling]
    N --> Q
    O --> Q
