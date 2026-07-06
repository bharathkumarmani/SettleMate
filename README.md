# SettleMate

**Group Shared Expense Calculator** — an Excel workbook with VBA macros that tracks shared expenses among friends and automatically calculates optimal settlements (who owes who, and the minimum transfers needed to settle everything).

## Overview

| Sheet | Purpose |
|-------|---------|
| **HOME** | Dashboard with buttons to add expenses, generate settlements, export PDF. Friend list goes here. |
| **EXPENSES** | Log every expense one row at a time — date, description, amount, who paid, how to split. |
| **REPORT** | Auto-calculated OWS (One-Who-Spent) matrix showing exactly who owes who. Protected with password `bharath`. |
| **Settlement** | Generated output — optimal From→To→Amount transfers that settle all debts. |
| **Config** | Currency symbol (₹), password, and category list. |

### How the math works

1. Every expense is split across all friends (equally or by custom amount/percentage)
2. The REPORT sheet builds an OWS matrix — each cell = how much row-person owes column-person
3. From the matrix, each person's **net balance** is computed: what others owe them minus what they owe others
4. A greedy algorithm matches the highest debtor to the highest creditor, producing the **minimum number of transfers** needed
5. Every balance ends at exactly zero — mathematically verified

---

## How to Use

### First-time setup

1. Open **SettleMate** in Excel (desktop version, not web)
2. Click **Enable Macros** when prompted


### Step-by-step

**1. Add friends** — Go to HOME sheet. Enter up to 12 names in the friend list (column D, starting at D10).

**2. Log expenses** — Go to EXPENSES sheet. Click the **➕ Add Expense** button or type directly. Each row:
| Column | What to enter |
|--------|---------------|
| Date | When the expense happened |
| Transaction | What it was for (e.g. "Dinner", "Petrol") |
| Amount | Total amount paid |
| Category | Optional — pick from Config sheet list |
| Paid By | Who paid — dropdown matches your friend list |
| Split Type | Pick `Split Equal`, `Split Unequal - %`, or `Split Unequal - Amt` |
| Friend 1–12 | For unequal splits, enter each friend's share (amount or decimal %) |

The **Validation** column automatically flags errors like unrecognized names or split percentages that don't add up to 100%.

**3. Check the report** — Go to REPORT sheet. It auto-calculates the OWS matrix. Protected so formulas aren't accidentally changed (password: `bharath`).

**4. Generate settlement** — Click **💰 Generate Settlement** on HOME. This reads the OWS matrix, computes net balances, and writes the optimal set of transfers to the Settlement sheet.

**5. Export to PDF** — Click **📄 Export PDF** to save both the Settlement and REPORT sheets as a single PDF file.

**6. Clear and start over** — Click **🧹 Clear Settlement** to reset.

---

## Buttons

| Button | What it does |
|--------|-------------|
| ➕ Add Expense | Inserts a new blank row in the EXPENSES table with today's date |
| 💰 Generate Settlement | Runs the full settlement algorithm and writes optimal transfers |
| 📊 Reports | Switches to the REPORT sheet |
| 📄 Export PDF | Saves Settlement + REPORT as a timestamped PDF |
| 🧹 Clear Settlement | Empties the Settlement sheet |

