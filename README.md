# Personal Finance Dashboard

A self-contained, single-file personal finance dashboard. No server needed — just open the HTML file in your browser.

## Quick Start

1. Open `index.html` in any browser — it works with the included demo data
2. To use your own data, follow the "Add Your Own Data" section below

## Features

- **Overview** — Total spend, daily average, income vs spend, monthly trend, category donut
- **Categories** — Heatmap showing spend intensity by month, category breakdown with drill-down
- **Merchants** — Top merchants chart, searchable paginated table, side-by-side detail panel
- **Transactions** — Full filterable/searchable table with CSV export, per-transaction category editing
- **Cash Flow** — Income vs spending chart, net cash flow trend, transfer tracking
- **Insights** — Trip/event analyzer (search "Italy" or "vacation"), subscription tracker, anomaly detection
- **Category Management** — Create, rename, delete categories; bulk reassign merchants/transactions
- **Date Filtering** — Global date range pills (This Month, Last 3 Mo, YTD, All Time, Custom)
- **Dark/Light Mode** — Toggle in the header
- All data and customizations saved to localStorage (persists across sessions)

## Add Your Own Data

The dashboard expects transaction data in this JSON format embedded in the HTML file.

### Data Format

```json
{
  "cats": ["Category1", "Category2", ...],
  "merch": ["Merchant1", "Merchant2", ...],
  "srcs": ["Bank Account", "Credit Card 1", "Credit Card 2"],
  "s": [
    ["2025-01-15", 42.50, 0, 0, 0, "MERCHANT DESCRIPTION"],
    ...
  ],
  "i": [
    ["2025-01-10", 3200.00, "EMPLOYER DIRECT DEPOSIT", "Bank Account"],
    ...
  ],
  "tr": [
    ["2025-01-20", 1500.00, "CREDIT CARD PAYMENT", "Bank Account"],
    ...
  ]
}
```

### Field Definitions

**`cats`** — Array of category names (strings). Index position matters.

**`merch`** — Array of merchant names (strings). Index position matters.

**`srcs`** — Array of account/source names (strings). Index position matters.

**`s`** (spending) — Each transaction is an array:
| Index | Field | Type | Example |
|-------|-------|------|---------|
| 0 | Date | string (YYYY-MM-DD) | "2025-03-15" |
| 1 | Amount | number | 42.50 |
| 2 | Merchant index | number | 0 (index into `merch` array) |
| 3 | Category index | number | 0 (index into `cats` array) |
| 4 | Source index | number | 0 (index into `srcs` array) |
| 5 | Description | string | "WHOLE FOODS PURCHASE" |

**`i`** (income) — Each entry: `[date, amount, description, source_name]`

**`tr`** (transfers) — Each entry: `[date, amount, description, source_name]`

### Steps to Add Your Data

1. Export your bank/credit card statements as CSV or PDF
2. Use a script or AI to parse them into the JSON format above
3. Open `index.html` in a text editor
4. Find the line starting with `const RAW=`
5. Replace everything between `const RAW=` and the `;` with your JSON
6. Save and open in browser

### Tips

- **Exclude transfers**: Credit card payments from your bank account should go in `tr` (transfers), not `s` (spending) — this prevents double-counting
- **Categories**: Start broad, then use the in-app category manager to create custom categories and reassign merchants
- **Merchant normalization**: Multiple merchant strings (e.g., "STARBUCKS #1234", "STARBUCKS #5678") should map to the same merchant index
- **Income**: Only include actual income deposits, not transfers between your own accounts

## Tech Stack

- Single HTML file, no build tools, no dependencies to install
- Chart.js (loaded from CDN) for all visualizations
- Inter font from Google Fonts
- All state stored in browser localStorage

## Privacy

All your financial data stays in the HTML file and your browser's localStorage. Nothing is sent to any server.
