# FX Hedging Project — AI Prompt Log

## Project
Scenario 3: Surgical Robotics — FX Transaction Hedging

## AI Tool Used
ChatGPT (OpenAI)

# Stage 2 — Technical Specification

## Interaction 1 — Organizing My Initial Draft

**My request:**
I developed my initial analysis based on the surgical robotics scenario and my Stage 1 executive brief. I asked ChatGPT to help organize my work into the technical specification format required by my professor.

**AI assistance:**
ChatGPT helped structure the document using the professor's template, organizing the problem statement, inputs, assumptions, calculations, outputs, and sensitivity analysis. It also suggested technical details for the model.

**My review:**
I reviewed the organized draft to make sure it reflected my original hedging scenario, financial objectives, and the four strategies I wanted to compare.

## Interaction 2 — Reviewing the Professor's Requirements

**My request:**
Review my specification against the professor's template and identify anything that needs to be corrected.

**AI assistance:**
ChatGPT helped identify missing requirements, including the required four-column input table, workbook structure, and validation checks.

**My review and revisions:**

After reviewing the identified gaps, I requested revisions to ensure the specification followed the professor's original template. The following changes were made:

**1. Input Table**
- Before: The initial draft did not fully organize the required inputs into the professor's four-column format or clearly distinguish input variables from calculated values.
- After: Section 2.1 was revised to include standardized names, descriptions and sources, units, and example values. Section 2.2 separately identifies derived values and their formulas. The specification also identifies the market inputs that require verified sources and dates.

**2. Workbook Structure**
- Before: The initial draft did not clearly identify all workbook tabs or explain their individual purposes.
- After: Section 3 was revised to identify all eight workbook tabs and their functions: Cover, Legend/Key, Inputs, Forward, Money Market, Options, Sensitivity, and Notes & Assumptions. The Cover tab specification was also updated to include the author and a data-source block.

**3. Validation Checks**
- Before: The initial draft did not include a complete checklist for verifying the calculations and workbook structure.
- After: Section 6.3 was expanded to include eleven validation checks. These cover named ranges, spreadsheet errors, formula-based outputs, forward proceeds, money-market calculations, interest rate parity, option payoffs, sensitivity scenarios, and formatting.

These revisions improved the specification's clarity and made the model easier to reproduce and audit during Stage 3.

## Interaction 3 — Revising Inputs and Assumptions

**My request:**
Help review the financial assumptions, placeholder values, and calculations to ensure they are appropriate for my scenario.

**AI assistance:**
ChatGPT explained the ACT/360 interest convention, money-market hedge calculations, currency option premiums, and interest rate parity. It also helped identify which market inputs needed verified market data.

**My review:**
I examined the assumptions and checked that the model continued to focus on protecting the company's euro receivable. I also reviewed the distinction between the EUR put used for the receivable and the EUR call retained for a hypothetical payable.

## Interaction 4 — Improving Document Formatting

**My request:**
Help make the document match the professor's template, including the heading, input tables, and font formatting.

**AI assistance:**
ChatGPT adjusted the document layout, standardized the fonts, and organized the tables.

**My review:**
I reviewed multiple versions and requested additional formatting changes before approving the final Word document.

## Interaction 5 — Preparing the GitHub Submission

**My request:**
Convert my completed technical specification into Markdown so I can upload it to GitHub.

**AI assistance:**
ChatGPT converted the document into Markdown while preserving the headings, tables, calculations, and change log.

**My review:**
I reviewed the Markdown formatting to prepare the final specification for submission.

## Interaction 6 — Addressing Stage 2 Feedback

**My request:**
Help me review my professor's Stage 2 feedback and identify the specific corrections needed in my GitHub files.

**AI assistance:**
ChatGPT helped explain the feedback and identify the necessary changes to the market input documentation, Cover tab description, version information, and AI prompt log.

**My review:**
I reviewed the suggested changes and updated the specification to include additional Cover tab documentation. I also expanded this prompt log to document the specific before-and-after changes made to the input table, workbook structure, and validation checks.

The market input section was also revised:
- Before: The specification used indicative values for the EUR/USD spot rate and USD and EUR interest rates without specific observation dates.
- After: The specification included dated market observations and documented interest-rate proxies. The assigned forward quote of 1.1807 remained unchanged, and the baseline calculations were updated.

The specification's version information and change log were updated to reflect these revisions.

# Stage 3 — AI-Assisted Workbook Build and Audit

## Interaction 7 — Generating the Excel Workbook

**My request:**
I provided ChatGPT with my professor's Stage 3 requirements and asked it to generate the Excel workbook using my completed Stage 2 specification.

**AI assistance:**
ChatGPT generated `model.xlsx` based on the specification, including eight worksheets, named ranges, hedge calculations, a sensitivity table and chart, and validation checks.

**My review:**
I downloaded the workbook and opened it in Microsoft Excel. I reviewed the worksheet structure and compared the model's inputs and outputs against my Stage 2 specification before beginning the detailed audit.

## Interaction 8 — Checking Named Ranges

**My request:**
I asked ChatGPT to help verify whether the workbook contained the required named ranges.

**AI assistance:**
ChatGPT explained how to access Excel's Name Manager and which named ranges were required by the specification.

**My review:**
I opened Name Manager and manually checked the names, displayed values, and cell references. After reviewing them myself, I sent screenshots to ChatGPT for additional verification.

**Result:**
All 11 required named ranges were present, including the ten core inputs and `BASIS`. Five additional calculated ranges were also included.

## Interaction 9 — Testing the Sensitivity Analysis

**My request:**
I asked ChatGPT to help me test whether the sensitivity analysis responded correctly to changes in the spot exchange rate.

**AI assistance:**
ChatGPT instructed me to temporarily change `S0_in` from 1.1154 to 1.2000 and compare the resulting calculations.

**My review:**
I manually changed the spot rate in Excel and checked whether the sensitivity table, hedge proceeds, and chart updated. I compared the original and revised numbers and then sent screenshots of both versions to ChatGPT for additional verification.

I confirmed that the forward proceeds remained fixed at $11,098,580 while the other applicable calculations responded to the change in the spot rate. After completing the test, I restored the original spot rate of 1.1154.

**Result:**
The sensitivity analysis recalculated correctly when the input changed.

## Interaction 10 — Reviewing the Money-Market Hedge

**My request:**
I asked ChatGPT to help verify the three money-market hedge calculations required by my specification.

**AI assistance:**
ChatGPT reviewed the borrowing, currency conversion, and USD investment calculations and compared them against the specified formulas.

**My review:**
I manually checked the amounts displayed in Excel, including the EUR borrowing amount, USD conversion, investment proceeds, and EUR loan repayment. After checking the numbers, I sent a screenshot of the Money Market worksheet to ChatGPT for additional verification.

**Result:**
The workbook calculated approximately €9,100,316.47 borrowed, $10,150,492.99 converted into USD, and $10,550,831.25 at maturity. The EUR loan repayment equaled the €9,400,000 receivable.

## Interaction 11 — Reviewing the Currency Options

**My request:**
I asked ChatGPT to help review the currency put and call calculations.

**AI assistance:**
ChatGPT reviewed the strike prices, option premiums, future premium costs, and put proceeds. It also checked that the call was separated from the receivable hedge comparison.

**My review:**
I manually examined the option calculations and compared the displayed numbers with the assumptions and formulas in my specification. I then sent a screenshot of the Options worksheet to ChatGPT for additional verification.

I also identified a minor formatting improvement: the exchange rates would be easier to review if displayed to four decimal places rather than two.

**Result:**
The put and call calculations were consistent with the specification, and the call remained separated as a hypothetical payable extension.

## Interaction 12 — Reviewing Validation Checks and Interest Rate Parity

**My request:**
I asked ChatGPT to help review the validation checks and explain why the interest rate parity deviation was flagged for investigation.

**AI assistance:**
ChatGPT explained the difference between the assigned forward quote and the implied forward rate calculated from the spot rate and interest-rate inputs.

**My review:**
I manually reviewed the validation results in Excel and checked the implied forward rate against the assigned forward quote. I then sent a screenshot of the validation section to ChatGPT for additional verification.

The implied forward rate was approximately 1.122429, compared with the assigned forward rate of 1.1807. The deviation was approximately 4.93530%, exceeding the 0.05% tolerance.

I retained the `INVESTIGATE` status rather than changing the inputs or formulas to force the check to pass.

**Result:**
Eleven validation checks displayed `PASS`, one displayed `INVESTIGATE`, and none displayed `FAIL`. The parity deviation remained documented for further investigation in Stage 4.

## Interaction 13 — Preparing the Audit Report and GitHub Submission

**My request:**
I asked ChatGPT to help organize my workbook audit findings into the Markdown format required for Stage 3 and explain where to submit the files.

**AI assistance:**
ChatGPT helped organize the audit report using the required structure of what I checked, what I found, and what I did. It also provided instructions for uploading the workbook and audit report to GitHub.

**My review:**
I reviewed the audit report against the checks I performed in Excel. I uploaded `model.xlsx` to `capabilities/fx-hedging/` and created the audit report at `analysis/2026-11-18-surgical-robotics-build-audit-analysis.md`.

**Result:**
The workbook and audit report were committed to GitHub.

# Stage 4 — Market Data and Population

## Interaction 14 — Researching and Manually Verifying Market Data Sources

**My request:**
I asked ChatGPT to help me search for reliable sources for the EUR/USD spot exchange rate and the one-year USD and EUR interest rates. I initially wanted to use FRED for all three inputs to maintain consistency, but after reviewing the available series, I asked ChatGPT to help locate appropriate data on the European Central Bank's website.

**AI assistance:**
ChatGPT helped identify potential market data sources, locate the relevant FRED and ECB series, and explain which interest-rate benchmarks would be suitable for my 365-day foreign currency exposure. It also helped compare different rate choices and provided links to the official data sources.

**My review and independent verification:**
After ChatGPT helped identify the sources, I personally visited the websites to verify the information. I reviewed the ECB Data Portal, checked the published one-year euro-area AAA government bond yield, and confirmed the observation date and reported value. I also reviewed the selected ECB exchange-rate and FRED interest-rate information.

I did not rely solely on ChatGPT's reported figures. I used the original data sources to review the observations and selected November 17, 2026 as the common market observation date.

**Result:**
I selected the ECB EUR/USD reference rate of 1.0989, the FRED one-year USD Treasury yield of 4.60%, and the ECB one-year EUR government bond yield of 2.977566%.

## Interaction 15 — Converting Interest Rates and Calculating CIP

**My request:**
I asked ChatGPT to explain how to convert the ECB's continuously compounded one-year EUR yield into the simple ACT/360 convention required by my workbook.

**AI assistance:**
ChatGPT helped explain the conversion and calculate the covered interest parity (CIP) implied forward rate using the selected market observations.

**My review:**
I entered the converted EUR rate of 2.980937% into Excel, together with the ECB spot rate of 1.0989 and the FRED USD rate of 4.60%.

I reviewed the recalculated results in my workbook and confirmed that the assigned bank forward quote of 1.1807 remained unchanged.

**Result:**
The workbook calculated a CIP-implied forward rate of approximately 1.116410. The discrepancy between the bank quote and theoretical forward rate remained flagged for investigation.

## Interaction 16 — Populating the Excel Workbook

**My request:**
I asked ChatGPT to guide me through updating the existing Excel workbook with the selected and reviewed market data.

**AI assistance:**
ChatGPT helped identify the correct input cells and explained how to update the market values without overwriting the workbook's formulas.

**My review:**
I personally downloaded the workbook from GitHub, opened it in Microsoft Excel, and manually entered the market inputs.

I also updated the source documentation in the Inputs and Notes & Assumptions worksheets to reflect the ECB and FRED observations.

The put and call strikes remained linked to the updated spot rate, while the scenario-provided forward quote and option premiums remained unchanged.

**Result:**
The workbook was populated with the November 17, 2026 market observations without requiring structural formula changes.

## Interaction 17 — Reviewing the Updated Workbook

**My request:**
I asked ChatGPT to help review the workbook after entering the new market observations.

**AI assistance:**
ChatGPT reviewed screenshots of the Money Market, Options, Notes & Assumptions, and Sensitivity worksheets. It helped compare the recalculated amounts with the expected financial calculations and identify whether the model continued to function properly.

**My review:**
I opened each worksheet in Excel, reviewed the updated calculations, and sent screenshots to ChatGPT for additional verification.

I confirmed that the sensitivity analysis recalculated around the new spot rate and that the forward and money-market proceeds remained fixed across the scenarios.

**Result:**
The workbook reported 11 `PASS`, 1 `INVESTIGATE`, and 0 `FAIL` validation checks. The parity deviation remained approximately 5.44509% under the workbook's calculation convention.

## Interaction 18 — Cross-Verifying Results Against the FX Hedging Lab

**My request:**
I asked ChatGPT to help me independently cross-check my Excel workbook against the professor's FX Hedging Lab.

**AI assistance:**
ChatGPT guided me through entering the same market inputs into the FX Hedging Lab and helped compare the lab's calculations against my Excel workbook.

ChatGPT also assisted in identifying and explaining a discrepancy between the put-option results in the two models.

**My review and independent verification:**
I personally opened the professor's FX Hedging Lab, manually entered the selected market inputs, and reviewed the calculated results.

I compared the lab's forward hedge, money-market hedge, and CIP-implied forward calculations against my Excel workbook, with ChatGPT assisting in the comparison.

The forward, money-market, and CIP results matched within the displayed precision.

However, the put-option proceeds differed by $10,740.94. With ChatGPT's assistance, I investigated the discrepancy by reviewing the formula in my Excel workbook.

I determined that my workbook deducted the financed option premium of $241,040.94, while the FX Hedging Lab deducted the original upfront premium of $230,300.

I retained the original workbook formula because financing the premium through maturity was consistent with my Stage 2 specification.

**Result:**
The FX Hedging Lab cross-check confirmed agreement for the forward, money-market, and CIP calculations. The put-option difference was explained and documented as a difference in premium-financing conventions rather than changing the workbook to force the results to match.

## Interaction 19 — Preparing the Stage 4 Market-Data Memo

**My request:**
I asked ChatGPT to help organize the selected market observations, source documentation, CIP calculation, workbook validation, and FX Hedging Lab comparison into the required Stage 4 market-data memo.

**AI assistance:**
ChatGPT helped draft and revise the Markdown memo, including the market-data table, source links, interest-rate conversion, forward-rate comparison, validation results, and FX Lab discrepancy.

**My review:**
I reviewed the memo to ensure that it reflected the market data I had checked, the values I entered into Excel, and the cross-verification performed using the FX Hedging Lab.

I then updated the memo and committed the populated Excel workbook to GitHub.

**Result:**
The Stage 4 market-data memo was saved at `data/2026-11-18-surgical-robotics-market-data-memo.md`, and the updated workbook was committed at `capabilities/fx-hedging/model.xlsx`.

# Summary of AI Use

My work began with the surgical robotics scenario and the hedging analysis developed during Stage 1. I used ChatGPT to help organize my analysis into the required technical specification, review the professor's requirements, explain financial assumptions, improve formatting, and prepare the Markdown files for GitHub.

During Stage 3, ChatGPT generated the Excel workbook based on my specification and assisted with the auditing process. I opened the workbook in Microsoft Excel and manually reviewed the named ranges, hedge calculations, sensitivity analysis, and validation checks before sending screenshots to ChatGPT for additional verification.

**During Stage 4, I primarily used ChatGPT as a research assistant to help locate appropriate market data sources. After receiving its suggestions, I personally visited the ECB and FRED websites to review the published observations and verify the numbers rather than relying solely on AI-generated information.** I selected the market inputs, entered them into Excel, and updated the source documentation.

**I also used ChatGPT to assist with cross-verification against the professor's FX Hedging Lab.** I manually entered the inputs into the lab and compared its results with my Excel workbook. ChatGPT helped interpret the comparisons and investigate the put-option discrepancy. After reviewing the formula, I retained the original premium-financing convention and documented the reason for the difference.

Throughout the project, I remained responsible for selecting and reviewing the sources, checking the calculations, testing the workbook, interpreting the results, and documenting any limitations. The interest rate parity discrepancy was preserved for further investigation rather than adjusting the inputs to force the model to pass.
