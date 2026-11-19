# Stage 4 — Market Data and Population Memo

**Project:** FX Hedging — Surgical Robotics  
**Scenario:** Scenario 3 — Surgical Robotics  
**Author:** Brayden Chang-Kanoa  
**Date Prepared:** November 18, 2026  
**Market Observation Date:** November 17, 2026  
**Status:** Market data collected; workbook population and validation pending

## 1. Purpose

The purpose of this memo is to document the market inputs selected for the Surgical Robotics foreign exchange hedging model. The company expects to receive €9,400,000 from a German hospital group in 365 days and must evaluate strategies to manage its exposure to changes in the EUR/USD exchange rate.

The selected inputs use November 17, 2026 observations to maintain a consistent market reference date. The European Central Bank (ECB) provides the EUR/USD exchange rate and euro-denominated government yield, while the Federal Reserve Bank of St. Louis (FRED) provides the U.S. Treasury yield.

## 2. Market Inputs and Sources

| Input | Value | Source | Observation Date | Notes |
|---|---|---|---|---|
| `S0_in` | 1.0989 USD/EUR | ECB — Euro Foreign Exchange Reference Rates | Nov. 17, 2026 | Official reference rate; not an executable bank quote |
| `R_USD` | 4.60% | FRED — DGS1 | Nov. 17, 2026 | One-year U.S. Treasury yield proxy |
| `R_FC` | 2.977566% | ECB — AAA 1-Year Government Bond Spot Yield | Nov. 17, 2026 | Original continuously compounded yield |
| `R_FC` (model input) | 2.980937% | Calculated from ECB yield | Nov. 17, 2026 | Converted to simple ACT/360 convention |
| `F0_in` | 1.1807 USD/EUR | Assigned scenario | Scenario-provided | Bank forward quote retained |
| `K_PUT` | 1.0989 USD/EUR | Set equal to live spot | Nov. 17, 2026 | At-the-money put strike |
| `K_CALL` | 1.0989 USD/EUR | Set equal to live spot | Nov. 17, 2026 | At-the-money call strike |
| `PREM_PUT` | $0.0245/EUR | Assigned scenario | Scenario-provided | Premium retained; not a live quote |
| `PREM_CALL` | $0.0448/EUR | Assigned scenario | Scenario-provided | Premium retained; not a live quote |
| `FC_AMT` | €9,400,000 | Assigned scenario | Scenario-provided | Contractual receivable |
| `T_DAYS` | 365 | Assigned scenario | Scenario-provided | Exposure horizon |
| `BASIS` | 360 | Model specification | Model assumption | ACT/360 day-count convention |

**Retrieval date:** November 18, 2026. Exact retrieval clock times were not recorded and are not represented as independently verified timestamps.

### Source Links

**European Central Bank — EUR/USD Spot Rate**

https://www.ecb.europa.eu/stats/exchange/eurofxref/shared/pdf/2026/11/20261117.pdf

**Federal Reserve Bank of St. Louis — One-Year Treasury Yield**

https://fred.stlouisfed.org/series/DGS1

**European Central Bank — One-Year AAA Government Bond Yield**

https://data.ecb.europa.eu/data/datasets/YC/YC.B.U2.EUR.4F.G_N_A.SV_C_YM.SR_1Y

ECB series identifier: `YC.B.U2.EUR.4F.G_N_A.SV_C_YM.SR_1Y`

The ECB yield of 2.977566% was read from the ECB Data Portal chart displaying November 17, 2026.

## 3. Interest Rate Selection and Assumptions

The U.S. interest rate is the one-year constant-maturity Treasury yield published by FRED. This rate was selected because its maturity closely matches the company's 365-day exposure.

The euro interest rate is the ECB's one-year AAA euro-area government bond spot yield. This rate was selected because it is denominated in euros and matches the exposure's approximate maturity.

Both interest rates are government-yield proxies rather than executable corporate borrowing or investment rates. The U.S. Treasury yield and ECB AAA spot yield also use different quotation conventions, requiring an adjustment before comparison.

### Conversion of the ECB Yield

The ECB reports its yield using continuous compounding, while the hedging workbook uses simple interest with an ACT/360 convention.

The converted euro rate is calculated as:

`R_FC = [EXP(0.02977566 × 365/365) − 1] / (365/360)`

**Converted EUR rate = 2.980937%**

The converted rate will be entered into the workbook's `R_FC` named-range input cell.

This conversion matches the one-year effective accumulation factor while expressing the rate using the workbook's 365/360 simple-interest convention.

## 4. Covered Interest Parity Calculation

Covered interest parity (CIP) provides a theoretical forward exchange rate based on the spot rate and the two interest rates.

The model uses:

`F_CIP = S0 × (1 + R_USD × T/BASIS) / (1 + R_FC × T/BASIS)`

Using the selected inputs:

- Spot rate: 1.0989 USD/EUR
- USD interest rate: 4.60%
- Converted EUR interest rate: 2.980937%
- Time: 365 days
- Day-count basis: 360

**CIP-implied forward rate: 1.116410 USD/EUR**

**Assigned bank forward rate: 1.180700 USD/EUR**

### Forward Rate Comparison

| Measure | Result |
|---|---:|
| Bank forward quote | 1.180700 |
| CIP-implied forward | 1.116410 |
| Difference (bank minus CIP) | +0.064290 USD/EUR |
| Difference relative to CIP-implied forward | +5.7587% |
| Proceeds using bank quote | $11,098,580 |
| Proceeds using CIP-implied rate | $10,494,252 |
| Difference in USD proceeds | +$604,328 |

The bank's assigned forward quote is substantially higher than the theoretical CIP-implied forward rate.

This discrepancy will remain flagged for investigation. The bank quote will not be changed to force the parity check to pass.

Because the calculation uses government-yield proxies rather than executable borrowing and lending rates, the difference does not independently establish an arbitrage opportunity. A bank requote or matched-tenor executable market rates would be needed for a stronger pricing assessment.

## 5. Option Assumptions

The put and call strikes are set equal to the selected EUR/USD spot rate of 1.0989 USD/EUR.

The original scenario premiums remain unchanged:

- EUR put premium: $0.0245 per EUR
- EUR call premium: $0.0448 per EUR

These premiums are scenario-provided assumptions, not independently retrieved market option prices.

## 6. Workbook Population and Validation Plan

The updated market values will be entered into the existing Excel workbook through the appropriate named-range input cells.

The following checks will be performed after population:

1. Confirm all hedge calculations recalculate correctly.
2. Verify that the sensitivity table and chart update around the new spot rate.
3. Re-run the covered interest parity validation and record the deviation.
4. Confirm the forward, money-market, and option calculations remain formula-driven.
5. Compare workbook outputs against the professor's FX Hedging Lab.
6. Document any discrepancies or structural fixes before submission.

These checks are pending and will be updated after the workbook has been populated and tested.

## 7. Limitations and Next Steps

The selected data represent a common November 17, 2026 observation date rather than the November 18 market close. This choice aligns the inputs using the latest mutually selected completed observation date.

The ECB exchange rate is an informational reference rate, and the interest rates are government-yield proxies. They may differ from rates available to the company for actual transactions.

The next step is to populate the Excel workbook with the selected inputs, perform the validation checks, and cross-check the results against the FX Hedging Lab. Any unresolved discrepancies will be carried forward into Stage 5.
