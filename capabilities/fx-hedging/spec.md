
# Surgical Robotics — FX Transaction Hedge Model · Technical Specification

**University of Hawaiʻi at Mānoa · Shidler College of Business**  
**FIN 321: International Finance and Securities**  
**FX Transaction Hedging Project — Technical Specification**

| Field | Value |
|---|---|
| Created by | Brayden Chang-Kanoa |
| Updated by | Brayden Chang-Kanoa |
| Date Created | 2026-11-06 |
| Date Updated | 2026-11-06 |
| Version | 0.0 |
| LLM Used | ChatGPT — Inputting Data into Template, Revisions, and Layout Creation |
| Role | Treasury Analyst / FP&A Analyst |
| Audience | CFO / Director of Treasury |
| Companion Workbook | student build (Stage 3) |

## 1. Problem Statement

A U.S. surgical robotics manufacturer has a €9,400,000 receivable from a German hospital group, expected to be received in 365 days. The company's functional currency is USD, and exchange rates are quoted in USD per EUR, meaning a depreciation of the euro would reduce the receivable's value when converted into U.S. dollars. The objective is to protect the USD value of the receivable while exploring options that would allow us to possibly benefit from favorable exchange rate movements in the market. From a corporate treasury perspective, the company will compare four strategies: no hedge, a forward contract, a money-market hedge, and a currency put option. The results will help management determine which strategy provides the best balance of financial protection, potential upside, and cost.

## 2. Inputs (Known Variables)

### 2.1 Core Inputs

| Standardized Name | Description / Stage-4 Source | Unit | Example |
|---|---|---|---|
| FC_AMT | EUR receivable; source: assigned scenario | EUR | 9,400,000 |
| S0_in | Spot; source: live EUR/USD market quote | USD per EUR | 1.1800 — indicative, replaced with live data at Stage 4 |
| F0_in | 365-day forward; source: dealer/market quote | USD per EUR | 1.1807 |
| R_USD | USD deposit rate; source: Fed H.15 / bank quote | Annual % | 3.06% — indicative, replaced with live data at Stage 4 |
| R_FC | EUR borrowing rate; source: ECB / bank quote | Annual % | 3.00% — indicative, replaced with live data at Stage 4 |
| T_DAYS | Time to settlement; assigned scenario | Days | 365 |
| BASIS | Single ACT/360 day-count basis; convention | Days | 360 |
| K_PUT | EUR put strike; scenario specifies at spot | USD per EUR | = S0_in |
| K_CALL | EUR call strike; scenario specifies at spot | USD per EUR | = S0_in |
| PREM_PUT | EUR put premium; assigned scenario | USD per EUR | 0.0245 |
| PREM_CALL | EUR call premium; assigned scenario | USD per EUR | 0.0448 |

### 2.2 Derived / Intermediate Values

| Name | Description | Source / named-range formula |
|---|---|---|
| DF_USD / DF_FC | USD / EUR accumulation factors | 1 + R_USD × T_DAYS/BASIS; 1 + R_FC × T_DAYS/BASIS |
| FV_PREM_PUT | Put premium future cost (negative) | −PREM_PUT × FC_AMT × DF_USD |
| FV_PREM_CALL | Call premium future cost (negative) | −PREM_CALL × FC_AMT × DF_USD |
| S_T_grid | 11 settlement-spot scenarios | S0_in × (0.95, 0.96, …, 1.05) |
| USD_NO_HEDGE | Unhedged proceeds by scenario | S_T × FC_AMT |

## 3. Assumptions & Constraints

Receivable, full notional, single settlement at 365 days; USD per EUR throughout. Simple interest on both legs with ACT/360 (BASIS = 360). No bid–ask spreads, taxes, counterparty risk, fees, partial hedges, or probability weights. Option premiums are paid in USD at inception and carried to settlement at R_USD as an opportunity cost. The put protects the receivable; call inputs are retained for the template’s payable extension, not treated as an additional receivable hedge. Covered interest parity is a benchmark, not a guarantee for independently quoted market inputs.

Workbook tabs and purpose: Cover (scope, date, executive outputs); Legend/Key (yellow editable inputs, blue assumptions, black formulas, green cross-tab links, gray outputs); Inputs (single source of all named ranges); Forward (locked proceeds); Money Market (visible borrowing, conversion, investment steps); Options (put payoff and premium); Sensitivity (11-row comparison, hedge profits, winners, chart); Notes & Assumptions (source URLs, retrieval dates, basis, exclusions, audit findings). No hard-coded outputs.

## 4. Calculation Flow

**Step 1 — Accumulation factors and option premium costs**

- DF_USD = 1 + R_USD × T_DAYS/BASIS
- DF_FC = 1 + R_FC × T_DAYS/BASIS
- FV_PREM_PUT = −PREM_PUT × FC_AMT × DF_USD
- FV_PREM_CALL = −PREM_CALL × FC_AMT × DF_USD

**Step 2 — Forward hedge**

USD_FWD = FC_AMT × F0_in

Fixed across settlement rates.

Check figure: **$11,098,580**.

**Step 3 — Money-market hedge**

Separate calculated outputs:

1. FC_BORROW = FC_AMT/DF_FC
2. USD_NOW = FC_BORROW × S0_in
3. USD_MM = USD_NOW × DF_USD

The EUR receivable repays the EUR loan at maturity.

**Step 4 — Currency options and no hedge**

EUR put:

USD_PUT(S_T) = FC_AMT × MAX(S_T, K_PUT) + FV_PREM_PUT

No hedge:

USD_NO_HEDGE(S_T) = FC_AMT × S_T

For a hypothetical EUR payable only:

USD_CALL_OUTLAY(S_T) = FC_AMT × MIN(S_T, K_CALL) − FV_PREM_CALL

Do not include this payable series in the receivable comparison.

**Step 5 — Strategy comparisons**

For each S_T, calculate:

- USD_NO_HEDGE
- USD_FWD
- USD_MM
- USD_PUT
- Hedge profit for each active strategy (= strategy proceeds − USD_NO_HEDGE)
- Overall winner (maximum of all four)
- Best active hedge (maximum of forward, money market, put)

Ties must be labeled "Tie."

**Step 6 — Summary**

USD_BASE_k evaluates each strategy at S_T = S0_in.

USD_FLOOR_PUT = MIN(USD_PUT over S_T_grid).

Display USD_FWD, USD_MM, USD_BASE_k, USD_FLOOR_PUT, and put premium future cost.

## 5. Outputs

| Output | Description / format | Purpose |
|---|---|---|
| Input panel | 11 core input rows; source and quote date on Notes | Single source of truth |
| Strategy summary | USD_FWD; USD_MM; USD_BASE_k; USD_FLOOR_PUT; gray formula cells | Executive comparison |
| Sensitivity / hedge-profit table | 11 rows; 4 strategies; 3 profit columns; winner labels | Numerical comparison |
| Sensitivity chart | Line chart: settlement USD/EUR vs USD proceeds | Certainty vs upside and downside |

Baseline at S_T = S0_in (illustrative, rounded):

- No hedge: $11,092,000
- Forward: $11,098,580
- Money market: ≈ $11,098,548
- Put: ≈ $10,854,555

Recompute all figures from formulas in Stage 3; no hard-coded outputs.

## 6. Model Review — What Worked & What to Improve

### 6.1 What Worked

The draft specifies the three money-market stages and the put premium opportunity cost, enabling a formula-by-formula audit.

### 6.2 What to Improve

Initial draft lacked an explicit tab map and differentiated parity deviations from calculation failures. Revision adds eight tab purposes, an implied-forward comparison, and a documented parity tolerance; source dates and live quotes remain Stage 4 tasks.

### 6.3 Auditability Checklist

- (a) All 10 required names plus BASIS resolve.
- (b) No #REF!, #DIV/0!, #VALUE!, #NAME?, or other error cells.
- (c) Every calculated output is a formula, not a typed number.
- (d) Forward = FC_AMT × F0_in = $11,098,580.
- (e) EUR loan maturity value = FC_AMT.
- (f) F_IMPLIED = S0_in × DF_USD/DF_FC and USD_MM = FC_AMT × F_IMPLIED.
- (g) Parity difference = ABS(F_IMPLIED − F0_in)/F0_in, flag if > 0.05% (investigate quote mismatch, not automatically a formula defect).
- (h) Put at S_T = K_PUT equals K_PUT × FC_AMT + FV_PREM_PUT.
- (i) Grid has 11 increasing points, centered on S0_in.
- (j) Fixed hedge lines do not vary with S_T.
- (k) Colors match Legend/Key.

## 7. Sensitivity Plan

S_T_grid = S0_in × (0.95, 0.96, 0.97, 0.98, 0.99, 1.00, 1.01, 1.02, 1.03, 1.04, 1.05): 11 rows at 1% increments.

Plot USD_NO_HEDGE, USD_FWD, USD_MM, and USD_PUT against S_T on one line chart. No hedge rises linearly; forward and money market are horizontal; the put is flat below K_PUT (net of financed premium) and rises above it.

CFO should see the trade-off between locked certainty, put protection with upside, and unhedged exposure. Include hedge-profit columns and per-row winner / best-active-hedge labels.

## 8. Limitations & Next Steps

Excludes dynamic/partial hedging, option valuation from volatility, transaction spreads, counterparty/settlement risk, and ASC 815 / IFRS 9 hedge accounting.

Stage 3: AI builds model.xlsx from this spec and audits every check.

Stage 4: replace indicative market inputs with timestamped quotes and review parity.

Stage 5: validate scenarios and recommend a hedge in the CFO memo.

Save as capabilities/fx-hedging/spec.md, update the folder README.md, and commit both alongside prompt-log.md.

## Appendix A — Change Log

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-11-06 | Student / AI-assisted | Initial Stage 2 specification draft using Scenario 3. |
| 0.2 | 2026-11-06 | Student / AI-assisted | Added workbook tab purposes and validation checks; clarified at-spot put/call strikes and exact placeholder disclosure. |
