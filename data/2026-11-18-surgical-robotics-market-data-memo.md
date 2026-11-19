## 6. Workbook Population and Validation Results

The existing Excel workbook was populated with the November 17, 2026 market observations through the named-range input cells. The original scenario forward quote, receivable amount, settlement horizon, and option premiums remained unchanged.

### Workbook Validation

The workbook was reviewed in Microsoft Excel after population. The following results were confirmed:

| Validation | Result |
|---|---|
| Forward hedge proceeds | $11,098,580 |
| Money-market hedge proceeds | $10,494,252 |
| Put-option net proceeds | $10,088,619.06 |
| CIP-implied forward | 1.116410 USD/EUR |
| Parity deviation | 5.44509% |
| Validation checks | 11 PASS, 1 INVESTIGATE, 0 FAIL |

The sensitivity table recalculated across 11 scenarios, ranging from a 5% decrease to a 5% increase in the EUR/USD spot rate. The forward and money-market proceeds remained fixed across the scenarios, while the unhedged and put-option proceeds changed with the settlement exchange rate.

The parity deviation remained flagged as INVESTIGATE. No inputs or formulas were changed to force the check to pass.

### FX Hedging Lab Cross-Check

The workbook's results were compared with the professor's FX Hedging Lab using the same market inputs.

| Calculation | Excel Workbook | FX Hedging Lab | Comparison |
|---|---:|---:|---|
| Forward hedge | $11,098,580 | $11,098,580 | Match |
| EUR borrowing | €9,124,235 | €9,124,235 | Match |
| USD conversion | $10,026,622 | $10,026,622 | Match |
| Money-market hedge | $10,494,252 | $10,494,252 | Match |
| CIP-implied forward | 1.116410 | 1.1164 | Match within displayed precision |
| Put-option net proceeds at spot | $10,088,619.06 | $10,099,360.00 | Difference of $10,740.94 |

The forward, money-market, and covered interest parity calculations matched the FX Hedging Lab.

The put-option results differed because of how the option premium was treated. The FX Hedging Lab deducted the original upfront premium of $230,300, while the Excel workbook deducted the premium accumulated to maturity of $241,040.94.

The Excel workbook uses the formula:

`=FC_AMT*MAX(B12,K_PUT)+FV_PREM_PUT`

This formula accounts for the financing cost of the upfront premium, consistent with the Stage 2 specification.

The difference of $10,740.94 was therefore attributed to the premium-financing convention rather than an arithmetic error. The existing formula was retained, and the difference was documented.

### Structural Fixes

No structural formula changes were required during Stage 4 testing.

The input-source notes and assumptions documentation were updated to reflect the ECB and FRED market observations. The model's calculations, sensitivity analysis, and validation checks continued to operate after the new inputs were entered.

The unresolved parity deviation will be addressed in Stage 5.
