# Loan Amortization Calculator

A comprehensive Excel spreadsheet for tracking multiple loans, calculating payments, simulating extra payments, and visualizing your debt payoff journey.

![Excel](https://img.shields.io/badge/Microsoft_Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![License](https://img.shields.io/badge/License-Free_to_Use-green?style=for-the-badge)

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Screenshots](#screenshots)
- [How to Use](#how-to-use)
- [Sheet Structure](#sheet-structure)
- [Formulas Explained](#formulas-explained)
- [Payment Strategies](#payment-strategies)
- [Customization](#customization)
- [FAQ](#faq)
- [Author](#author)
- [License](#license)

---

## Overview

Managing multiple loans can be overwhelming. This calculator helps you:

- **See the true cost** of each loan (principal + interest + fees)
- **Track your progress** as you make payments
- **Prioritize payments** using the Avalanche Method
- **Simulate extra payments** and see potential savings
- **Consolidate all debts** in a single dashboard

### Who is this for?

- Anyone with multiple loans (mortgage, car, personal, student)
- People who want to pay off debt faster
- Those who want to understand how much they're really paying in interest
- Financial planners helping clients organize their debts

---

## Features

### Core Features

| Feature | Description |
|---------|-------------|
| Multi-loan tracking | Track up to 3 loans (easily expandable) |
| Automatic calculations | Monthly payment, interest, principal split |
| Amortization schedule | Full month-by-month breakdown |
| Extra payment simulation | See how extra payments reduce interest |
| Fees & insurance | Include fixed monthly charges |
| Payment tracking | Mark payments as completed |
| Progress visualization | Track completion percentage |

### Dashboard Features

| Feature | Description |
|---------|-------------|
| Loan summary | All loans at a glance |
| Consolidated metrics | Total debt, monthly cost, interest |
| Payment priority | Auto-sorted by interest rate (Avalanche) |
| Progress tracking | Payments made across all loans |
| Visual charts | Bar charts for comparison |

### Smart Calculations

- **Effective Annual Rate (EA) to Monthly Rate** conversion
- **PMT function** for accurate payment calculation
- **Dynamic ranking** for payment prioritization
- **Conditional formulas** that stop when loan is paid off

---

## How to Use

### Step 1: Enter Your Loan Details

Go to each Credit sheet (Credit_1, Credit_2, Credit_3) and fill in the **yellow cells**:

| Field | Description | Example |
|-------|-------------|---------|
| Loan Name | Descriptive name | "Car Loan" |
| Principal Amount | Total borrowed | $25,000 |
| Annual Interest Rate (EA) | Effective annual rate | 8.00% |
| Loan Term (months) | Total months | 60 |
| First Payment Date | When payments start | 01/15/2025 |
| Monthly Fees/Insurance | Fixed monthly charges | $25 |

### Step 2: View Your Dashboard

The Dashboard sheet automatically shows:
- All loans consolidated
- Total monthly cash outflow
- Which loan to prioritize
- Your payment progress

### Step 3: Track Your Payments

In each Credit sheet:
1. Find the current month row
2. Change "Paid" column from "No" to "Yes"
3. Watch your progress update automatically

### Step 4: Simulate Extra Payments

To see how extra payments help:

**Option A: One-time extra payment**
- Enter amount in the "Extra Payment" column (yellow) for specific month

**Option B: Recurring extra payment**
- Enter amount in "Extra Monthly Payment" field (H11)
- Applies to all future months

### Step 5: Analyze Savings

Check the "Interest Savings" metric to see how much you save with extra payments.

---

## Sheet Structure

```
Loan_Amortization_Calculator.xlsx
│
├── Instructions
│   └── User guide, color legend, tips, author info
│
├── Dashboard
│   ├── 1. Loan Summary (all loans)
│   ├── 2. Consolidated Metrics
│   ├── 3. Payment Priority (Avalanche)
│   └── 4. Payment Progress
│
├── Credit_1
│   ├── Loan Details (editable)
│   ├── Progress Tracking (automatic)
│   ├── Projections (automatic)
│   ├── Savings Calculator (automatic)
│   └── Amortization Table (200 rows)
│
├── Credit_2
│   └── (same structure as Credit_1)
│
└── Credit_3
    └── (same structure as Credit_1)
```

---

## Formulas Explained

### Monthly Rate Conversion

```excel
=POWER(1+Annual_Rate, 1/12) - 1
```
Converts Effective Annual Rate to true monthly rate (not simple division by 12).

### Monthly Payment (PMT)

```excel
=IF(Rate>0, PMT(Monthly_Rate, Term, -Principal), Principal/Term)
```
Calculates fixed monthly payment. Handles 0% interest edge case.

### Interest Portion

```excel
=ROUND(Previous_Balance * Monthly_Rate, 2)
```
Interest calculated on remaining balance.

### Principal Portion

```excel
=Payment - Interest
```
Whatever isn't interest goes to principal.

### New Balance

```excel
=MAX(Previous_Balance - Principal_Paid, 0)
```
Prevents negative balance.

### Payment Priority Ranking

```excel
=RANK(Rate, All_Rates, 0)
```
Ranks loans from highest to lowest rate (Avalanche Method).

### Progress Percentage

```excel
=COUNTIF(Paid_Column, "Yes") / COUNTIF(Payment_Column, ">0")
```
Completed payments divided by total payments.

---

## Payment Strategies

### Avalanche Method (Implemented)

Pay minimum on all loans, put extra money toward **highest interest rate** loan.

| Pros | Cons |
|------|------|
| Minimizes total interest paid | May take longer to pay off first loan |
| Mathematically optimal | Less psychological satisfaction early on |

### Snowball Method (Alternative)

Pay minimum on all loans, put extra money toward **smallest balance** loan.

| Pros | Cons |
|------|------|
| Quick wins build motivation | Pay more interest overall |
| Psychological satisfaction | Not mathematically optimal |

This calculator uses **Avalanche Method** by default (priority sorted by rate).

---

## Customization

### Adding More Loans

1. Right-click on Credit_3 tab
2. Select "Move or Copy"
3. Check "Create a copy"
4. Rename to Credit_4
5. Update Dashboard formulas to include new sheet

### Changing Currency

All cells use number format `#,##0.00`. To change currency symbol:
1. Select cells
2. Format Cells > Number > Currency
3. Choose your currency

### Changing Date Format

Default is MM/DD/YYYY. To change:
1. Select date cells
2. Format Cells > Date
3. Choose preferred format

### Adding Snowball Method

To sort by balance instead of rate:
1. Go to Dashboard
2. Change hidden column N formula from `=RANK(Rate...)` to `=RANK(Balance...)`

---

## FAQ

### Q: Why does my payment differ from the bank's statement?

**A:** Banks may use different day-count conventions, or include fees in the payment. Adjust the "Monthly Fees/Insurance" field to match.

### Q: Can I use this for variable rate loans?

**A:** This calculator assumes fixed rates. For variable rates, you'd need to manually update the rate periodically.

### Q: Why is the first month's interest different than expected?

**A:** First payment often covers a partial month. This calculator assumes full months starting from the first payment date.

### Q: How accurate is the interest calculation?

**A:** Very accurate for fixed-rate loans with monthly payments. Uses standard amortization formulas.

### Q: Can I protect the formulas from accidental edits?

**A:** Yes. Select all non-yellow cells, right-click > Format Cells > Protection > Locked. Then Review > Protect Sheet.

### Q: Why are some cells yellow?

**A:** Yellow = editable (your inputs). White = calculated (don't edit). This color coding is explained in the Instructions sheet.

---

## Technical Details

| Specification | Value |
|---------------|-------|
| Total Formulas | 4,356 |
| Max Loan Term | 200 months |
| Number of Loans | 3 (expandable) |
| File Size | ~500 KB |
| Compatibility | Excel 2016+, Google Sheets, LibreOffice |

### Functions Used

- `PMT` - Payment calculation
- `POWER` - Rate conversion
- `ROUND` - Decimal precision
- `MAX` - Prevent negatives
- `MIN` - Cap payments at balance
- `IF` - Conditional logic
- `COUNTIF` - Count payments
- `SUMIF` - Sum conditional
- `INDEX/MATCH` - Dynamic lookups
- `RANK` - Priority sorting
- `EDATE` - Date calculations

---

## Author

**Juan Perea Possos**

- LinkedIn: [linkedin.com/in/juanpereapossos](https://linkedin.com/in/juanpereapossos)
- GitHub: [github.com/IngRetrius](https://github.com/IngRetrius)
- Email: retrius2001@gmail.com

Final-year Computer Information Systems Engineering student. Co-founder of digital studio specializing in front-end web development.

---

## License

**Free to use and share.**

This project is provided as-is for personal and educational use. Feel free to:
- Use it for your personal finances
- Share it with friends and family
- Modify it for your needs
- Use it as a learning resource

Attribution appreciated but not required.

---

## Changelog

### v1.0.0 (2025)

- Initial release
- 3 loan tracking sheets
- Dashboard with consolidated metrics
- Payment priority (Avalanche Method)
- Extra payment simulation
- Monthly fees/insurance support
- Payment tracking with progress metrics
- Bar charts for visualization

---

## Contributing

Found a bug or have a suggestion? 

1. Open an issue on GitHub
2. Or reach out on LinkedIn

Pull requests welcome!

---

## Acknowledgments

- Formulas validated against standard amortization calculations
- Inspired by the need to organize multiple personal loans

---

**If this helped you, consider sharing it with someone who needs it.**