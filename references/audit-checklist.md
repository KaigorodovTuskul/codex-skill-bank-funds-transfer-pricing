# FTP audit and gap-analysis checklist

For each finding record:

```text
ID
area
evidence / observed practice
expected methodology or control
source/status basis
pricing or risk-attribution effect
materiality / affected perimeter
recommended remediation
data needed to quantify
owner / target date (if requested)
```

Do not call a difference a regulatory breach unless the applicable rule and perimeter have been verified.

## 1. Purpose, scope and governance

- Is there a formal FTP policy with purpose, scope and component architecture?
- Are all material assets, liabilities, off-balance-sheet and contingent exposures covered?
- Is responsibility for market/repricing FTP, funding-liquidity FTP and contingent liquidity clear?
- Is Treasury/ALM central ownership explicit?
- Is independent Risk and Finance/Control challenge defined?
- Are ALCO approvals and review thresholds clear?
- Does new-product approval require an FTP treatment?
- Are centrally retained FTP costs/benefits documented and analysed for incentive effects?

## 2. Source and regulatory discipline

- Is the bank distinguishing binding local rules from international/foreign best practice?
- Are current source versions and effective dates tracked?
- Are draft/consultation documents labelled as such?
- Are regulatory liquidity factors used as economic FTP assumptions only when explicitly approved?

## 3. Market / repricing curve

- Is the curve purpose defined?
- Is it appropriate for currency and product repricing structure?
- Are reset conventions, forwards, day count and compounding correct?
- Is there a controlled proxy/fallback hierarchy?
- Are curve versions retained?

## 4. Marginal funding curve

- Is the curve based on marginal rather than only average historical funding cost for material business?
- Are legal entity, currency, seniority and secured/unsecured distinctions captured?
- Are source observations timestamped?
- Are tenor gaps, interpolation and extrapolation governed?
- Are stale data and manual overlays controlled?
- Is market access / proxy selection explained?

## 5. Product mapping

- Are repricing and funding horizons separated?
- Are bullet products matched by relevant tenor?
- Are amortising products cash-flow mapped rather than final-maturity-only where material?
- Are floating assets protected from the `next reset = funding horizon` error?
- Are liability credits based on actual funding benefit?
- Are sign conventions consistent?

## 6. Behavioural products

- Are prepayments, decay, withdrawals and drawdowns modelled where material?
- Are NMDs segmented by stability/rate sensitivity where evidence supports it?
- Are BAU and stress assumptions distinct?
- Are models versioned, backtested and governed?
- Are fallbacks explicit?

## 7. Contingent liquidity

- Are undrawn commitments priced?
- Are collateral calls, deposit run-off and secured-funding roll-off considered where material?
- Are draw/run-off assumptions evidence-based or explicitly policy-set?
- Is the cost allocated to the activity creating the need?
- Is double counting between drawn/on-balance and undrawn/contingent parts prevented?

## 8. Liquidity cushion / stress linkage

- Is the cushion linked to stress/scenario analysis?
- Are idiosyncratic, market-wide and combined scenarios covered as relevant?
- Is stress duration explicit?
- Are haircuts and monetisation horizons realistic and versioned?
- Is usable liquidity constrained for entity/currency transferability and encumbrance?
- Is cushion carry/funding cost measured?
- Is cost attributed by driver rather than socialised without rationale?

## 9. Trading / secured funding / derivatives

- Are secured and unsecured economics distinguished?
- Are asset haircuts and repo/reverse-repo tenors relevant to transfer pricing?
- Are stressed collateral/margin outflows captured?
- Are downgrade/additional-termination triggers considered where material?

## 10. Performance attribution

- Does product/business profitability include relevant FTP components?
- Can commercial margin be separated from funding/liquidity effects?
- Does Treasury retain unexplained material residual P&L?
- Are strategic subsidies/overlays visible separately from economic FTP?
- Can management see how curve changes redistribute profitability?

## 11. Data and systems

- Can historical results be reproduced from stored curve/model/methodology versions?
- Is there a controlled curve/model store?
- Is data lineage retained?
- Are calculations deterministic and tested?
- Are stale/proxy/override flags visible?
- Is maker-checker implemented?
- Do instrument/cohort totals reconcile to product/business/bank views?

## 12. High-impact gap tests

Quantify when possible:

- one pooled rate vs matched-maturity FTP;
- average funding cost vs marginal funding curve;
- next-reset tenor vs true funding horizon on floating assets;
- final maturity vs amortising/behavioural cash flows;
- long stable funding credit granted to volatile NMD balances;
- missing contingent-liquidity charges;
- cushion cost left centrally vs allocated by driver;
- stale funding curve;
- proxy curve choice;
- manual override without provenance;
- inconsistent back-book repricing.

Report impact as bps, annual monetary amount, product/business redistribution, change in customer margin and Treasury residual where data permits.
