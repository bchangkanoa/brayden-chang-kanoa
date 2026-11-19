# Surgical Robotics — Stage 3 Workbook Build Audit

**Author:** Brayden Chang-Kanoa  
**Date:** 2026-11-18  
**Project:** FIN 321 — FX Transaction Hedging  
**Scenario:** Surgical Robotics  
**Workbook:** `capabilities/fx-hedging/model.xlsx`  
**Specification:** `capabilities/fx-hedging/spec.md`  
**AI Tool:** ChatGPT

## 1. Audit Objective

The purpose of this audit was to evaluate the AI-generated FX hedging workbook against the requirements established in my Stage 2 technical specification. I reviewed the named ranges, hedge calculations, sensitivity analysis, and validation checks to determine whether the workbook was functioning as intended.

## 2. Audit Findings

### Finding 1 — Named Ranges

**What I checked:** I opened Excel's Name Manager and reviewed the required named ranges against the Stage 2 specification.

**What I found:** All 11 required named ranges were present, including the ten core inputs and `BASIS`. The displayed values and cell references were consistent with the specification. Additional calculated ranges were also included.

**What I did:** I confirmed the named ranges and retained their existing references because no discrepancies were identified.

**Status:** PASS

### Finding 2 — Sensitivity Analysis

**What I checked:** I temporarily changed the EUR/USD spot rate (`S0_in`) from 1.1154 to 1.2000 and examined the sensitivity table and chart.

**What I found:** The settlement-rate scenarios, unhedged proceeds, money-market proceeds, put proceeds, and chart updated automatically. The forward proceeds remained fixed at $11,098,580, as expected.

**What I did:** I compared the original and revised results, confirmed the calculations responded correctly, and restored the original spot rate of 1.1154.

**Status:** PASS

### Finding 3 — Interest Rate Parity Deviation

**What I checked:** I reviewed the implied forward rate, the assigned forward quote, and the workbook's parity deviation validation.

**What I found:** The implied forward rate was approximately 1.122429, compared with the assigned forward rate of 1.1807. The deviation was approximately 4.93530%, exceeding the specified 0.05% tolerance.

**What I did:** I retained the assigned forward quote and left the validation status as `INVESTIGATE`. The difference may reflect the use of unmatched benchmark interest rates and the assigned forward quote. This issue is documented for further investigation during Stage 4.

**Status:** INVESTIGATE

### Finding 4 — Money-Market Hedge

**What I checked:** I reviewed the three required money-market hedge calculations: EUR borrowing, conversion into USD, and investment of USD proceeds.

**What I found:** The workbook calculated approximately €9,100,316.47 borrowed, $10,150,492.99 converted into USD, and $10,550,831.25 at maturity. The EUR loan repayment equaled the €9,400,000 receivable.

**What I did:** I compared the displayed calculations with the formulas in the Stage 2 specification and confirmed that the amounts were consistent.

**Status:** PASS

### Finding 5 — Currency Options

**What I checked:** I reviewed the put and call strikes, premiums, future premium costs, and net proceeds.

**What I found:** The put and call strikes were linked to the spot rate. The put premium was $230,300 at inception and approximately $239,383.10 at maturity. The call was separately labeled as a hypothetical payable extension and excluded from the receivable comparison.

**What I did:** I confirmed the displayed calculations were consistent with the specification. I also identified a minor formatting improvement: displaying exchange rates to at least four decimal places would make the inputs easier to audit.

**Status:** PASS — formatting improvement identified

### Finding 6 — Workbook Validation Checks

**What I checked:** I examined the validation results in the Notes & Assumptions worksheet.

**What I found:** Eleven validation checks displayed `PASS`, including the forward calculation, EUR loan repayment, money-market parity, put floor, sensitivity bounds, and fixed hedge proceeds. One check displayed `INVESTIGATE` for the parity deviation. No checks displayed `FAIL`.

**What I did:** I retained the investigation flag and documented the exception rather than changing the assumptions or formulas to force the check to pass.

**Status:** 11 PASS / 1 INVESTIGATE / 0 FAIL

## 3. Limitations and Follow-Up

The workbook uses a USD SOFR benchmark and a 12-month EUR Euribor benchmark as interest-rate proxies. These are not matched executable 365-day financing quotes. The underlying market observations should be independently confirmed, and the rate-tenor mismatch should be investigated during Stage 4.

The assigned forward quote of 1.1807 remains unchanged, consistent with the scenario requirements.

## 4. Conclusion

The AI-generated workbook passed the named-range, hedge-calculation, sensitivity, and formula-recalculation checks performed during this audit. The primary outstanding issue is the interest-rate parity deviation, which remains explicitly flagged for investigation.

The model is ready for continued testing and market-data verification in Stage 4, subject to resolving or documenting the outstanding market-input limitations.
