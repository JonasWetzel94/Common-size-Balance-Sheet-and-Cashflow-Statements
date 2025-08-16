# Omega Industries — Common-Size BS, Indirect CFS, and Free Cash Flows (Excel)

---

## Case Description
Omega Industries Ltd. (manufacturing) — build a recruiter-readable financial reporting workbook in Excel:
- Create a **common-size balance sheet** for the current year.
<img width="390" height="744" alt="image" src="https://github.com/user-attachments/assets/cb56c3b3-05e1-40c0-bfd3-ef69e5c931aa" />

---

- Roll forward **PP&E** and **Retained Earnings** from notes/workings.
<img width="496" height="468" alt="image" src="https://github.com/user-attachments/assets/3b2f15c3-49af-41a2-a163-60e68822250a" />


---

- Compute **FCFF** and **FCFE** and explain the drivers.
<img width="515" height="768" alt="image" src="https://github.com/user-attachments/assets/041961f1-7f89-4610-ae50-e6197188c77d" />



---

## Tasks
- Transform the Balance Sheet to **common-size (%)**.
- Calculate **working capital movements** (Inventory, Trade receivables, Trade payables).
- Build an **Indirect CFS** with clear sections (Operating, Investing, Financing).
- Derive **CapEx** from PP&E reconciliation and **net borrowing** from debt movements.
- Calculate **FCFF / FCFE** and validate with control checks.
- Document mapping, formulas, and audit trails.

---

## Accounting/Analytics Steps (exact postings & calcs)
1. **PP&E reconciliation (USD m)**  
   Opening **129,447** + Purchases **8,623** − Depreciation **28,787** ⇒ Closing **109,283**.
2. **Retained earnings roll-forward (USD m)**  
   Begin **64,760** + Net income **4,114** + OCI **14** − Dividends **9,779** ⇒ End **59,109**.
3. **Working capital (changes, USD m)**  
   Inventory **+10,248** (use of cash), Trade receivables **−22,142** (source), Trade payables **−24,731** (use) ⇒ **Net WC change −12,837** (use).
4. **Cash Flow (Indirect)**  
   - Operating profit (EBIT) **5,242**  
   - + Depreciation **28,787**  
   - ± WC change **−12,837** ⇒ **Cash flow from operations (pre-int/tax/div)** **21,192**  
   - − Interest **495**, − Tax **633**, − Dividends **9,779** ⇒ **Net CFO** **10,285**  
   - Investing: − CapEx **17,675** (PP&E **8,623** + Intangibles **9,052**)  
   - Financing: **Net borrowing −5,847** (LT −1,755; ST −4,092)
5. **Cash reconciliation**  
   **Net cash flow −13,237**; Cash **beg 16,813 → end 3,576**, change **−13,237** ✅
6. **Free cash flows (USD m)**  
   - **FCFF = 3,913**  
     `EBIT 5,242 + Dep 28,787 + Interest 495×(1–0.20) – CapEx 17,675 – WC investment 12,837`  
   - **FCFE = −2,330**  
     `CFO (pre-int/tax/div) 21,192 – CapEx 17,675 + Net borrowing (−5,847)`

---

## Trial Balance / Data Summary
| Item | Current Year (USD m) | % of Assets |
|---|---:|---:|
| **Total Assets** | **176,118** | **100%** |
| PP&E (NBV) | 109,283 | 62% |
| Intangibles | 18,118 | 10% |
| Inventory | 31,398 | 18% |
| Trade receivables | 13,743 | 8% |
| Cash & cash equivalents | 3,576 | 2% |
| **Total Equity** | **88,446** | **50%** |
| — Share capital | 29,337 | 17% |
| — Retained earnings (closing) | 59,109 | 34% |
| **Non-current liabilities** | **31,620** | **18%** |
| — LT borrowings | 13,902 | 8% |
| — Pension liabilities | 17,718 | 10% |
| **Current liabilities** | **56,052** | **32%** |
| — ST borrowings | 21,721 | 12% |
| — Trade payables | 34,331 | 19% |

**Checks**
- **Assets (176,118) = Liabilities (87,672) + Equity (88,446)** ✅  
- **RE roll-forward** and **PP&E roll-forward** tie to the Balance Sheet ✅  
- **Cash change** ties to the CFS and Balance Sheet ✅

---

## Financial Statements / Results (key numbers)
- **Common-size BS:** Equity **50%**, Liabilities **50%** (Debt ratio ≈ **50%**).  
- **CFS (Indirect):** CFO **10,285**, CFI **−17,675**, CFF **−5,847**, **Net cash −13,237**.  
- **FCFF:** **3,913** (positive operating generation before financing).  
- **FCFE:** **−2,330** (cash shortfall to equity after CapEx and debt repayments).

---

## Mapping / Logic
- **Common-size**: Each BS line ÷ **Total Assets** (absolute reference).  
  Example: `='Balance Sheet'!C9 / 'Balance Sheet'!$C$33`
- **WC movement** (signs follow CFS logic):  
  - ΔInventory = Curr − Prior ⇒ **outflow if positive**  
  - ΔReceivables = Curr − Prior ⇒ **inflow if negative**  
  - ΔPayables = Curr − Prior ⇒ **outflow if negative**
- **CapEx**: `PP&E Purchases = Closing − Opening + Depreciation`  
  (Add intangible purchases for total investing cash outflow.)
- **Net borrowing**: Sum of **ΔLT debt + ΔST debt** (repayments negative).
- **FCFF**: `EBIT + Dep + Interest×(1–Tax) − CapEx − ΔNWC`  
- **FCFE**: `CFO (pre-int/tax/div) − CapEx + Net borrowing`
- **Cash check**: `CFO + CFI + CFF = ΔCash` and `Beg Cash + ΔCash = End Cash`.

---

## How I Built It
- **Excel structure**: separate tabs for *Income Statement*, *Balance Sheet*, *Common-size*, *Workings*, and *CFS – Indirect*.  
- **Techniques used**
  - Absolute cell anchoring for denominators: `$C$33`
  - Clear sign convention for WC lines (helper section in CFS tab)
  - Roll-forward blocks for PP&E and RE to surface **CapEx** and **Dividends**
  - Cross-sheet references and control cells labeled **“Check!”** (all evaluate to 0)
- **Example formulas**
  - Common-size line: `=BalanceSheet!C9 / BalanceSheet!$C$33`
  - WC subtotal: `=SUM(C17:C19)` (Inventory, AR, AP changes)
  - Net cash flow: `=C36 + C43 + C49`
  - FCFE (alt form): `=CFO_pre - CapEx + NetBorrowing`

---

## What I Learned
- Building a clean **audit trail** (roll-forwards → statements) speeds reviews.  
- **FCFE can be negative** even with positive FCFF when **CapEx and debt repayments** exceed operating cash.  
- Common-size views highlight structure quickly (Omega ≈ **72%** non-current assets; **50/50** equity vs. liabilities).  
- Small control cells (“Check!”) reduce reconciliation mistakes.

---

## Quick Skills Snapshot
- Financial statements modeling in **Excel** (IS/BS → CFS via Indirect Method)
- **Common-size analysis**, working capital mechanics, and reconciliations
- **Roll-forwards** (PP&E, Retained Earnings) driving CapEx/dividends
- **Valuation cash flows**: FCFF & FCFE with consistent sign conventions
- Review-friendly documentation with **built-in checks** and traceability

