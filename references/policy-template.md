# Bank FTP policy / methodology template

Tailor this structure to the bank, jurisdiction and operating model. Do not copy mechanically.

## 1. Purpose

Define why FTP exists: centralise funding and contingent-liquidity risk, attribute costs/benefits to activities that create or provide funding/liquidity, support product pricing and performance measurement, align incentives with risk appetite, and support ALM decisions.

## 2. Scope and perimeter

Specify:

- legal entities / branches;
- jurisdictions;
- currencies;
- business units;
- covered assets, liabilities and off-balance-sheet products;
- materiality thresholds;
- exclusions and simplifications.

## 3. Source hierarchy and regulatory status

List:

- binding local regulations;
- group standards;
- current Basel standards/guidelines used;
- supervisory guidance used as comparator;
- historical/better-practice sources;
- bank policies/model-governance standards.

State explicitly that foreign or draft material is not treated as binding unless applicable.

## 4. Definitions and FTP architecture

Define:

- FTP;
- LTP / funding-liquidity component;
- market/repricing transfer component;
- marginal funding cost;
- term liquidity premium/benefit;
- contingent-liquidity charge;
- behavioural maturity;
- optionality adjustment if used;
- liquidity cushion;
- economic FTP vs applied FTP;
- strategic/policy overlay;
- Treasury residual.

Show the transfer-rate bridge and sign conventions.

## 5. Governance / RACI

Define responsibilities for:

- Board/senior management as applicable;
- ALCO;
- Treasury / ALM;
- Risk;
- Finance/Control;
- business units;
- model validation/model risk;
- IT/data owners;
- Internal Audit.

Define approval thresholds for methodology, curves, models, proxies, overrides and exceptions.

## 6. Market / repricing curve methodology

Document:

- curve purpose;
- market instruments/benchmarks;
- product mapping;
- forward/reset treatment;
- tenor nodes;
- day count/compounding;
- interpolation/extrapolation;
- update frequency;
- fallback hierarchy;
- approval and controls.

## 7. Marginal funding curve methodology

Document:

- eligible funding observations;
- entity/currency distinctions;
- seniority and secured/unsecured classes;
- primary issuance vs secondary/indicative data;
- proxy hierarchy;
- sparse-tenor treatment;
- market-access overlays;
- update frequency/stale limits;
- manual overlays and governance.

## 8. Term funding-liquidity methodology

If using spread decomposition:

```text
LP(t) = MFC(t) - REF(t)
```

Document how assets are charged and liabilities credited, including sign conventions and treatment of internal funding pools.

## 9. Product mapping

For each product family specify:

- contractual cash flows;
- repricing horizon;
- funding/liquidity horizon;
- cash-flow/DCF method;
- behavioural model;
- contingent-liquidity treatment;
- optionality treatment;
- curve selection;
- fallback.

At minimum cover bullet loans/deposits, floating products, amortising loans, mortgages/prepayables, NMDs, securities/trading if relevant, revolving lines and guarantees/commitments if material.

## 10. Behavioural models

For each model define:

- segmentation;
- data history;
- methodology;
- calibration;
- versioning;
- validation/backtesting;
- limitations;
- override/fallback;
- BAU vs stress use.

## 11. Contingent liquidity

Define covered exposures, usage assumptions, stress linkage, standby-liquidity cost and allocation method. Prevent double counting of drawn and undrawn portions.

## 12. Liquidity cushion

Define:

- stress scenarios and horizon;
- eligible assets;
- haircuts and monetisation;
- transferability/encumbrance constraints;
- funding cost and asset yield;
- cost attribution method.

## 13. Trading / secured funding / derivatives

Where material define secured/unsecured transfer pricing, haircuts, repo tenor, collateral/margin outflows and relevant stress triggers.

## 14. New business and back book

State when transfer prices are locked, reset or remeasured. Distinguish customer/product economics, management revaluation and accounting P&L.

## 15. Strategic pricing / overlays

Require overlays to be separately visible from economic FTP. Define approver, duration, owner and reporting of the resulting internal subsidy/charge.

## 16. Data, systems and controls

Define source systems, curve/model stores, lineage, versioning, maker-checker, reconciliation, exception reporting, retention and access control.

## 17. Performance measurement and reporting

Define how FTP feeds:

- product/customer pricing;
- business profitability;
- Treasury result;
- budget/plan;
- ALCO reporting;
- new-product approval.

## 18. Review cycle

Define periodic review, model monitoring, curve monitoring, ad-hoc triggers, material-change thresholds and approval requirements.
