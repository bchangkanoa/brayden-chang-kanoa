# Surgical Robotics — FX Transaction Hedge Model · Technical Specification

**University of Hawaiʻi at Mānoa · Shidler College of Business**  
**FIN 321: International Finance and Securities**  
**FX Transaction Hedging Project — Technical Specification**

| Field | Value |
|---|---|
| Created by | Brayden Chang-Kanoa |
| Updated by | Brayden Chang-Kanoa |
| Date Created | 2026-11-06 |
| Date Updated | 2026-11-18 |
| Version | 0.4 |
| LLM Used | ChatGPT — Inputting Data into Template, Revisions, Calculations, and Layout Creation |
| Role | Treasury Analyst / FP&A Analyst |
| Audience | CFO / Director of Treasury |
| Companion Workbook | Student build (Stage 3) |
| Market Data Reference Date | 2026-11-06 |

## 1. Problem Statement

A U.S. surgical robotics manufacturer has a €9,400,000 receivable from a German hospital group, expected to be received in 365 days. The company's functional currency is USD, and exchange rates are quoted in USD per EUR, meaning a depreciation of the euro would reduce the receivable's value when converted into U.S. dollars. The objective is to protect the USD value of the receivable while exploring options that would allow us to possibly benefit from favorable exchange rate movements in the market.

From a corporate treasury perspective, the company will compare four strategies: no hedge, a forward contract, a money-market hedge, and a currency put option. The results will help management determine which strategy provides the best balance of financial protection, potential upside, and cost.

## 2. Inputs (Known Variables)

### 2.1 Core Inputs

All market observations use November 6, 2026 as the reference date. USD and EUR interest rates are benchmark proxies rather than executable bank financing quotes. Sources and rate limitations are documented below.

| Standardized Name | Description / Source | Unit | Value |
|---|---|---|---|
| FC_AMT | EUR receivable; assigned scenario | EUR | 9,400,000 |
| S0_in | EUR/USD spot; FRED DEXUSEU; 2026-11-06; https://fred.stlouisfed.org/series/DEXUSEU | USD per EUR | 1.1154 |
| F0_in | 365-day forward; assigned bank quote | USD per EUR | 1.1807 |
| R_USD | USD interest-rate proxy; FRED SOFR; 2026-11-06; https://fred.stlouisfed.org/series/SOFR | Annual % | 3.89% |
| R_FC | EUR interest-rate proxy; 12-month Euribor; 2026-11-06; https://www.cbcg.me/slike_i_fajlovi/eng/fajlovi/fajlovi_publikacije/imf/2026/imf_0211_061126.pdf | Annual % | 3.248% |
| T_DAYS | Time to settlement; assigned scenario | Days | 365 |
| BASIS | Single ACT/360 day-count basis; modeling convention | Days | 360 |
| K_PUT | EUR put strike; assigned at spot | USD per EUR | = S0_in |
| K_CALL | EUR call strike; assigned at spot | USD per EUR | = S0_in |
| PREM_PUT | EUR put premium; assigned scenario | USD per EUR | 0.0245 |
| PREM_CALL | EUR call premium; assigned scenario | USD per EUR | 0.0448 |

The put and call strikes are formula-linked to S0_in, so both equal 1.1154 USD per EUR under the current inputs.

The USD SOFR observation is an overnight secured funding benchmark used as a proxy for the USD deposit rate. The EUR 12-month Euribor observation is used as a proxy for the EUR borrowing rate. These benchmarks differ in tenor and market characteristics, and therefore do not represent matched executable financing quotes.

The forward rate of 1.1807 remains the assigned bank quote and is not replaced by an implied forward rate.

### 2.2 Derived / Intermediate Values

| Name | Description | Source / named-range formula |
|---|---|---|
| DF_USD / DF_FC | USD / EUR accumulation factors | 1 + R_USD × T_DAYS/BASIS; 1 + R_FC × T_DAYS/BASIS |
| FV_PREM_PUT | Put premium future cost (negative) | −PREM_PUT × FC_AMT × DF_USD |
| FV_PREM_CALL | Call premium future cost (negative) | −PREM_CALL × FC_AMT × DF_USD |
| F_IMPLIED | Implied forward rate | S0_in × DF_USD/DF_FC |
| FC_BORROW | EUR amount borrowed at inception | FC_AMT/DF_FC |
| USD_NOW | USD proceeds from converting borrowed EUR | FC_BORROW × S0_in |
| S_T_grid | 11 settlement-spot scenarios | S0_in × (0.95, 0.96, …, 1.05) |
| USD_NO_HEDGE | Unhedged proceeds by scenario | S_T × FC_AMT |

## 3. Assumptions & Constraints

Receivable, full notional, single settlement at 365 days; USD per EUR throughout. Simple interest on both legs with ACT/360 (BASIS = 360).

No bid–ask spreads, taxes, counterparty risk, fees, partial hedges, or probability weights.

Option premiums are paid in USD at inception and carried to settlement at R_USD as an opportunity cost.

The put protects the receivable; call inputs are retained for the template's payable extension, not treated as an additional receivable hedge.

Covered interest parity is a benchmark, not a guarantee for independently quoted market inputs. Because the USD and EUR benchmark proxies have different maturities, deviations between the implied forward and assigned bank forward are investigated rather than automatically classified as calculation errors.

Workbook tabs and purpose:

- **Cover:** Project title, scope, report date, author (Brayden Chang-Kanoa), university, course, executive outputs, and a data-source block listing the EUR/USD spot rate, USD and EUR interest rates, forward quote, option premiums, sources, and quote dates.
- **Legend/Key:** Yellow editable inputs, blue assumptions, black formulas, green cross-tab links, and gray outputs.
- **Inputs:** Single source of all named ranges, including values, units, and source information.
- **Forward:** Locked proceeds from the forward contract.
- **Money Market:** Visible EUR borrowing, USD conversion, and USD investment steps.
- **Options:** Put payoff and premium opportunity cost; call inputs reserved for a hypothetical payable extension.
- **Sensitivity:** Eleven-row comparison, hedge profits, winner labels, and line chart.
- **Notes & Assumptions:** Source URLs, retrieval dates, interest
