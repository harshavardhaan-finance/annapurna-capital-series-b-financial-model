# Annapurna Capital Technologies — Cost of Capital & Comparable Company Analysis
### Supporting Note to Task 3 (Valuation) — Series B Package
**Prepared as part of the Corporate Finance & Valuation Portfolio Project**
**Date of analysis:** August 2026

---

## 1. Purpose

This note documents the sourced, defensible build of (a) Annapurna's discount rate (WACC) and (b) a comparable-company valuation cross-check, per Task 3's requirement to value the business using both a DCF and a market-based method. Every market input below is traced to a specific file, sheet, and cell — no discount rate or multiple in this note is assumed without a citation.

---

## 2. Sector Classification

Annapurna does not map cleanly to a single industry classification because its revenue is a blend of three economic engines:

| Revenue line (FY26 mix) | % of Total Revenue | Nearest public-market analogue |
|---|---:|---|
| Financing Facilitation Commission + Marketplace Transaction Fee | 75.4% | Non-bank financial services / lending marketplace |
| Warehouse SaaS/IoT Subscription Fee | 10.3% | Software (Internet) |
| Storage Fee Revenue (owned mini-warehouses) | 14.3% | Farming/Agriculture (physical storage & agri-infrastructure) |

For the beta build (Section 4), we collapse this into a two-way split for simplicity: **~65% "financial services/marketplace" character, ~35% "physical agri-infrastructure" character**, reflecting that the SaaS fee line is small and shares more economic behavior with the warehousing side (both are infrastructure-attached, recurring, low-marginal-cost revenue) than with a standalone software business.

---

## 3. Comparable Company Analysis

**Source:** Web search of public funding disclosures (Tracxn, Entrepreneur/Inc42/YourStory press coverage, CBInsights, PitchBook public listings), current as of August 2026. Annapurna is unlisted, so no public equity comps exist — this is a precedent-transaction / private-market comp set, consistent with Task 3(b)'s requirement.

| Company | Business Model Overlap | Last Disclosed Valuation | Revenue (nearest FY) | Implied EV/Revenue |
|---|---|---:|---:|---:|
| **Arya.ag** | Closest direct comp: eNWR-based storage + credit + marketplace, 12,000 warehouses, 60% of India's districts | $325M (₹2,700 Cr), Series C-II, July 2024 | ₹451 Cr (FY25), profitable | ~6.0x–7.5x |
| **DeHaat** | Full-stack agritech; finance is one vertical among several (inputs, advisory, output market linkage) | $700–800M, Series E, Dec 2022 (stale — not re-marked publicly since) | ₹3,000+ Cr GMV (FY25), ₹369 Cr net profit | ~2.0x–2.3x (likely understated given valuation staleness) |
| **Samunnati** | Pure agri-NBFC / FPO financing — no owned warehousing infrastructure | ~$298M (May 2025 estimate) | Not disclosed post-2020 | Not computable |
| **Sohan Lal Commodity Management (SLCM)** | Agri-logistics + collateral management, 21,000+ warehouses — closest comp for the *owned mini-warehouse* segment specifically | Not disclosed ($58.1M total funding raised) | Not disclosed | Not computable |

**Interpretation for Task 3(b):**
- **Arya.ag is the ceiling** of the range — it is already profitable and runs an asset-light model (leases warehouses rather than owning them), so it structurally deserves a premium multiple to Annapurna, which is still loss-making and carries owned-warehouse capex on its balance sheet.
- **DeHaat's ~2–2.3x is a soft floor**, but it should be treated as understated rather than a true market-clearing multiple, since it reflects a valuation that has not been publicly re-marked in over three years despite substantial revenue growth.
- **Recommended EV/Revenue range for Annapurna: 3.5x–5.5x FY31E revenue**, positioned below Arya.ag (profitability gap) but above DeHaat's stale mark, reflecting Annapurna's stronger reported unit economics (11.1x LTV:CAC — see Case Study Section 7.2) as a partial offset to its current unprofitability and heavier balance sheet.
- Discount this forward EV back to present value using the WACC derived in Section 5, consistent with how the DCF's terminal value is discounted, so both methods in Task 3 are built on the same cost-of-capital foundation.

---

## 4. Beta — Sourced from Damodaran India Industry Betas (`betaIndia.xls`)

**File details:** Sheet `Industry Averages`, dated **05-Jan-2026** (cell B1). Tax convention used in the file: marginal tax rate 30% (cell F8/F9 area — "Do you want to use marginal or effective tax rates in unlevering betas?" → Marginal, 30%).

| Industry (row in file) | Levered Beta | D/E Ratio | Unlevered Beta |
|---|---:|---:|---:|
| **Financial Svcs. (Non-bank & Insurance)** — Excel row 44, columns C/D/F | 0.6035 | 1.465 | **0.298** |
| **Farming/Agriculture** — Excel row 43, columns C/D/F | 0.6647 | 0.101 | **0.621** |

**Blended unlevered beta** (weighted per the revenue split in Section 2):
```
Unlevered Beta = (0.65 × 0.298) + (0.35 × 0.621) = 0.194 + 0.217 = 0.411
```

**Relevered to Annapurna's own target capital structure** (post-Series B, working-capital-loan-only debt against a much larger equity base — target D/E ≈ 10%):
```
Levered Beta = Unlevered Beta × [1 + (1 − Tax Rate) × (D/E)]
             = 0.411 × [1 + (1 − 0.25) × 0.10]
             = 0.411 × 1.075
             = 0.442
```
*(Note: Annapurna's own 25% tax rate per Case Study Section 8 is used here for relevering, not the file's 30% default, since we are applying the beta to Annapurna's specific structure, not staying inside the file's own unlevering convention.)*

---

## 5. Equity Risk Premium — Sourced from Damodaran Country Risk Premium file (`ctrypremJuly26.xlsx`)

**File details:** Sheet `ERPs by country`, dated **01-Jul-2026** (cell B2).

| Input | Cell reference | Value |
|---|---|---:|
| Mature market ERP | Cell E3 | 4.20% |
| US Equity Risk Premium (implied ERP approach) | Cell E4 | 4.42% |
| **India — Rating-based Default Spread** (Moody's Baa3) | Row 73, Column D | 1.75% |
| **India — Country Risk Premium** | Row 73, Column F | **2.72%** |
| **India — Total Equity Risk Premium** | Row 73, Column E | **6.92%** |

We use the **Total Equity Risk Premium of 6.92%** (mature market ERP + India country risk premium) as the ERP input in CAPM, consistent with Damodaran's standard prescribed approach for emerging-market cost of equity.

---

## 6. Risk-Free Rate — Current Market Data (not in Damodaran file, sourced separately)

The Damodaran files use a **US long-term Treasury rate (3.95%, `waccIndia.xls` cell D9)** as their risk-free base, because their cost-of-capital output is denominated in USD before being converted to local currency. Since our DCF is built entirely in ₹ Lakhs, we instead anchor directly to the **India 10-Year G-Sec yield**, which is the correct INR-denominated risk-free proxy:

**India 10Y G-Sec yield: 6.85%** (as of August 21, 2026)

---

## 7. Cost of Equity (CAPM)

```
Cost of Equity = Risk-Free Rate + (Levered Beta × Total ERP)
               = 6.85% + (0.442 × 6.92%)
               = 6.85% + 3.06%
               = 9.91%
```

**Private-company / illiquidity adjustment:** This 9.91% is a public-market CAPM output. Damodaran explicitly recommends adding a size/illiquidity premium for private companies (his own written guidance suggests a minimum of 3–6%); for an early-stage, still-loss-making Series B company specifically, we take the upper half of that band:

```
Adjusted Cost of Equity = 9.91% + 6.0% = ~15.9%, rounded to 16%
```

---

## 8. Cost of Debt

Taken directly from the case (Section 8, Assumptions row 90) rather than proxied from Damodaran's lookup table, since Annapurna's actual borrowing rate is explicitly given:

```
Pre-tax Cost of Debt = 15.0%
After-tax Cost of Debt = 15.0% × (1 − 25%) = 11.25%
```

*(Cross-check only: Damodaran's `waccIndia.xls` shows a sector cost of debt of 6.71% for both Financial Svcs. and Farming/Agriculture — Excel rows 53 and 52, column G — but this reflects large, rated public borrowers and materially understates a Series-B-stage private company's actual borrowing cost. Annapurna's stated 15% working-capital loan rate is used as the correct input.)*

---

## 9. Capital Structure Weights

Using Annapurna's post-Series B target structure — the ₹140 Cr raise added to the existing equity base, against a working-capital loan that stays in the ₹13–21 Cr range through FY31E (Assumptions row 89):

```
Equity ≈ ₹193.5 Cr (paid-in capital, post-Series B) + retained value
Debt ≈ ₹13–21 Cr (working capital loan)

D/V ≈ 5%
E/V ≈ 95%
```

---

## 10. WACC — Final Build

```
WACC = (E/V × Cost of Equity) + (D/V × After-tax Cost of Debt)
     = (0.95 × 16.0%) + (0.05 × 11.25%)
     = 15.2% + 0.56%
     = 15.76%, rounded to ~16%
```

**Cross-check against Damodaran's pre-built sector WACCs** (`waccIndia.xls`, local-currency column, Excel rows 52–53):

| Industry | Damodaran Cost of Capital (local currency) |
|---|---:|
| Farming/Agriculture (row 52) | 10.94% |
| Financial Svcs. Non-bank & Insurance (row 53) | 8.71% |

Our build (~16%) sits meaningfully above both sector averages. This gap is expected and should be stated explicitly in the assignment write-up: Damodaran's numbers are **large-cap, public-market, liquid-equity averages**; Annapurna is an **unlisted, pre-profitability, Series-B-stage company**, and the ~6% illiquidity/early-stage premium applied in Section 7 is exactly what bridges that gap. Presenting both numbers side by side (rather than only the final ~16%) demonstrates the reasoning rather than hiding the adjustment.

---

## 11. Summary of Recommended Inputs for Task 3

| Input | Value | Source |
|---|---:|---|
| Risk-free rate | 6.85% | India 10Y G-Sec, market data (Aug 2026) |
| Total Equity Risk Premium (India) | 6.92% | `ctrypremJuly26.xlsx`, row 73, col E |
| Unlevered beta (blended) | 0.411 | `betaIndia.xls`, rows 43 & 44, col F |
| Relevered beta | 0.442 | Calculated (Section 4) |
| Illiquidity/private-company premium | 6.0% | Judgment call, per Damodaran's recommended 3–6% floor, upper end for early-stage |
| Cost of Equity | ~16.0% | CAPM + illiquidity premium |
| Cost of Debt (after-tax) | 11.25% | Case Study, Assumptions row 90 |
| **WACC** | **~16%** | Weighted per Section 10 |
| Comparable EV/Revenue range | 3.5x–5.5x FY31E revenue | Arya.ag / DeHaat precedent transactions (Section 3) |

Use the ~16% WACC to discount FCFF and to derive the DCF terminal value (Task 3a); use the 3.5x–5.5x EV/Revenue range applied to FY31E revenue, discounted back at the same WACC, as the comparable-transaction cross-check (Task 3b). Where the two methods diverge, the assignment should state which assumption (growth rate, margin trajectory, or multiple) drives the gap — this is explicitly invited by the case (Section 8's closing note).
