# 📦 Inventory Automation Workflow

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
```

---

## 🔧 Technologies Used

| Tool          | Purpose                      |
|---------------|------------------------------|
| n8n           | Workflow automation          |
| Google Sheets | Inventory data and logging   |
| Telegram      | Real-time alerting           |
| Slack         | Vendor communication         |
| Gmail         | Invoice delivery             |

---

## 📊 Google Sheets Structure

- **Inventory Data** – Source of truth for product stock.  
- **Inventory Snapshot** – Daily archive of inventory state.  
- **Alert Log** – Tracks alerts sent.  
- **Workflow Logs** – End-to-end workflow activity.  

---

## 📬 Alert Format (Telegram)

```text
🚨 Inventory Alert: Low Stock Detected  
📦 Product: {{ Product Name }}  
🔢 SKU: {{ SKU }}  
📉 Current Stock: {{ Quantity }} units  
📊 Reorder Point: {{ ReorderPoint }} units  
👤 Supplier: {{ Vendor }}  
🟥 Priority: Critical  

⚠️ Action Required:  
Stock is below the reorder threshold. Please review and restock promptly.
```

---

## 📦 Order Placement (Slack)

```text
📦 New Order Placement  
📦 Product: {{ Product Name }}  
🔢 SKU: {{ SKU }}  
📉 Quantity to Order: {{ ReorderPoint - Quantity }} units  
👤 Supplier: {{ Vendor }}  

⚠️ Action Required:  
Please confirm this order and provide an estimated delivery date.
```

---

## 🧾 Invoice Email (Gmail)

```text
🧾 Payment Invoice  
📅 Date: {{ $now }}  
📦 Product: {{ Product Name }}  
🔢 SKU: {{ SKU }}  
📉 Quantity: {{ ReorderPoint - Quantity }} units  
💰 Amount: {{ Amount }}  
📅 Due Date: {{ DueDate }}  
🏦 Payment Method: {{ PaymentMethod }}
```

---

## 🛠️ Setup Instructions
1. Clone this repository and import the workflow into your n8n instance.
2. Configure credentials for:
    ** Google Sheets
    ** Telegram Bot
    ** Slack App
    ** Gmail OAuth

3. Update sheet IDs, channel IDs, and email addresses as needed.
4. Activate the workflow and monitor logs for performance.

---

## 🧑‍💻 Author
OLUWALOWO John   
📧 oluwalowojohn@gmail.com   
🎨 [LinkedIn](https://[n8n.io](https://linkedin.com/in/oluwalowojohn/))

---

## 📄 License
This project is licensed under the MIT License. Feel free to fork, adapt, and contribute!

---

## 🙌 Contributions
Pull requests are welcome! If you have ideas to improve the workflow or add new integrations, feel free to open an issue or submit a PR.
