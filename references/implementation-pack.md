# FTP implementation pack

Use this after methodology decisions are approved or explicitly parameterised. Do not automate unresolved policy questions as hidden defaults.

## 1. Logical architecture

1. **Source-data layer** — contracts, balances, cash flows, commitments, collateral, behavioural history, funding transactions, market data, stress data.
2. **Market-curve service** — reference/discount/forward curves, versions and approvals.
3. **Funding-curve service** — marginal funding curves by entity/currency/funding class, source lineage, proxy hierarchy and approvals.
4. **Behavioural-model service** — prepayment, decay, drawdown, rate beta, stable/volatile segmentation and model versions.
5. **FTP engine** — product routing, matched maturity, DCF/tranching, liquidity premium, contingent liquidity, overlays and signs.
6. **Control layer** — data quality, curve freshness, approval state, override control, reconciliation, exception handling.
7. **Reporting layer** — deal/cohort FTP, profitability bridge, business summaries, Treasury residual, ALCO views and historical reruns.

## 2. Core entities

### `methodology_version`

- version_id
- effective_from / effective_to
- approval_status
- approver
- policy_reference

### `curve_version`

- curve_id
- curve_type: market_reference / marginal_funding / derived_liquidity
- legal_entity
- currency
- funding_class
- as_of_timestamp
- methodology_version
- status: draft / approved / retired
- approver

### `curve_node`

- curve_id/version
- tenor
- rate/spread
- convention
- source_type
- source_reference
- observed/proxy/overlay flag

### `product_mapping`

- product_code
- exposure_side
- repricing_method
- funding_horizon_method
- behavioural_model_id
- contingent_method
- curve_selection_rule
- fallback_rule
- effective dates

### `instrument_or_cohort`

- ID
- legal_entity
- jurisdiction
- currency
- business_unit
- product_type
- side: asset/liability/contingent
- balance/notional/limit
- customer rate
- origination
- maturity
- repricing schedule
- cash-flow schedule
- collateral/secured flags
- behavioural model/version

### `ftp_result`

- instrument/cohort ID
- calculation date
- methodology version
- market curve version
- funding curve version
- behavioural model version
- market/repricing component
- funding-liquidity component
- contingent-liquidity component
- optionality/behavioural adjustment if separate
- economic FTP
- policy overlay
- applied FTP
- monetary transfer
- business contribution
- exception flags
- timestamp

## 3. Configuration, not hard-coding

Keep controlled configuration for:

- product-to-method mapping;
- curve-selection hierarchy;
- funding classes;
- interpolation/extrapolation;
- behavioural model selection;
- stale-data thresholds;
- materiality thresholds;
- floors/caps;
- overlay rules;
- sign conventions;
- fallback rules;
- approval state.

## 4. Minimum controls

- reject/flag missing entity or currency;
- block unapproved methodology/curve/model versions in production;
- flag stale curves;
- identify proxy/extrapolated nodes;
- validate tenor ordering and duplicates;
- reconcile `derived liquidity spread = funding - comparable reference` where that architecture applies;
- validate cash-flow totals;
- detect potential contingent-liquidity double count;
- log every override with user/time/reason/approval;
- retain historical versions for reruns;
- reconcile deal/cohort totals to product/business/bank reporting;
- prevent use of draft/foreign supervisory sources as a runtime compliance flag without local mapping.

## 5. UAT set

### Curves

- exact node;
- interpolation;
- extrapolation/fallback;
- stale/proxy flag;
- different legal entity/currency;
- secured vs unsecured funding class;
- unapproved curve rejection.

### Products

- fixed-rate one-year bullet asset;
- term deposit liability;
- multi-year floating-rate loan with short reset horizon;
- five-year equal-amortising exposure using the BIS/FSI 26.1 bps validation case;
- irregular amortising loan using DCF;
- prepayable mortgage cohort;
- stable and volatile NMD segments;
- revolving line using the BIS/FSI 6,480 validation case;
- fully drawn line with zero undrawn contingent exposure;
- zero draw factor;
- secured trading exposure with haircut;
- matured/closed transaction.

### Controls

- historical rerun reproduces prior result;
- manual override requires approval;
- portfolio sum equals detail;
- missing data raises exception;
- curve/model effective dates enforced;
- overlay expiry works;
- Treasury residual reconciles.

## 6. MVP output tables

- `methodology_versions`
- `market_curves`
- `funding_curves`
- `product_mapping`
- `behavioural_models`
- `instrument_results`
- `summary_by_business`
- `treasury_reconciliation`
- `exceptions`
- `change_log`

## 7. ALCO reporting

Useful views:

- current vs prior market and marginal funding curves;
- term liquidity spread changes;
- representative new-business FTP by product;
- business charge/credit redistribution;
- Treasury residual;
- contingent-liquidity cost allocation;
- behavioural-model drift/backtest results;
- top proxies/overrides/exceptions;
- sensitivity to funding-spread widening and behavioural changes.

## 8. Practical implementation sequence

1. approve source hierarchy and FTP component architecture;
2. approve product taxonomy and sign conventions;
3. establish controlled market/funding curve stores;
4. implement fixed-rate bullet products;
5. implement floating-rate separation of reset and funding horizons;
6. implement amortising cash-flow mapping / DCF;
7. add behavioural products and NMDs;
8. add contingent liquidity and cushion linkage;
9. add trading/secured funding treatment if material;
10. automate controls, reconciliation and ALCO reporting;
11. validate/backtest and migrate from spreadsheets;
12. retire obsolete methods only after parallel-run reconciliation.
