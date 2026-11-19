# FX Hedging

This capability analyzes foreign exchange risk for a U.S. surgical robotics manufacturer expecting to receive €9,400,000 in 365 days.

The project compares forward contracts, money-market hedges, and currency put options to evaluate their effectiveness in managing exchange-rate risk.

## Stage 2 — Model Specification

The technical specification outlines the model's inputs, assumptions, calculations, outputs, and sensitivity analysis. It provides the foundation for building the Excel hedging model in Stage 3.

- [Technical Specification](spec.md) — Documents the model structure, formulas, and validation checks.
- [AI Prompt Log](prompt-log.md) — Documents how ChatGPT was used to help organize, review, and revise the specification and build the workbook.

## Stage 3 — AI-Assisted Build and Audit

The Excel hedging model was generated using ChatGPT based on the Stage 2 technical specification. The workbook contains eight worksheets, named ranges, formula-driven hedge calculations, a sensitivity table and chart, and validation checks.

The workbook was reviewed in Microsoft Excel by checking the named ranges, manually reviewing calculations, and testing whether changes to the spot exchange rate updated the results.

The audit identified an interest rate parity deviation of approximately 4.94%, which remains flagged for investigation. This difference may reflect the use of unmatched interest-rate benchmarks and the assigned forward quote.

- [Excel Hedging Model](model.xlsx) — Contains the hedge calculations, sensitivity analysis, and validation checks.
- [Stage 3 Audit Report](../../analysis/2026-11-18-surgical-robotics-build-audit-analysis.md) — Documents the workbook audit findings, results, and outstanding issues.

## Next Steps

Stage 4 will verify the market data, review the interest-rate assumptions, and investigate the parity deviation.

Stage 5 will validate the model's results and provide a final hedging recommendation for the CFO.
