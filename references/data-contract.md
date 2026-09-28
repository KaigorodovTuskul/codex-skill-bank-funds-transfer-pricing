# FTP data contract

Ask only for fields that can materially affect the requested result. Never silently default a missing required field.

## A. Perimeter and purpose

| Field | Required | Notes |
|---|---:|---|
| as_of_date | yes | curve/pricing date |
| legal_entity | yes | group/subsidiary/branch |
| jurisdiction | for live work | determines regulatory overlay |
| currency | yes | no silent currency mixing |
| business_unit | usually | attribution/reporting |
| methodology_version | yes for live/backtest | policy version |
| output_purpose | yes | pricing, P&L, audit, ALCO, build |

## B. Instrument / product

Capture where relevant:

- instrument/cohort ID;
- asset / liability / contingent classification;
- product type;
- customer rate/yield or expense;
- notional/balance;
- origination date;
- contractual maturity;
- repricing index, frequency and dates;
- scheduled principal and interest cash flows;
- prepayment/withdrawal terms;
- commitment limit and drawn amount;
- secured/unsecured status;
- collateral and haircut data;
- optionality/embedded caps/floors where relevant;
- booking entity and currency.

## C. Behavioural models

For prepayable/revolving/non-maturity products capture:

- segmentation and cohort definition;
- historical observation window;
- prepayment/decay/survival/run-off curve;
- stable vs volatile balance rule;
- rate beta / pricing sensitivity if used;
- drawdown assumptions;
- model owner and version;
- calibration date;
- backtest statistics;
- expert overlays;
- fallback assumption;
- distinction between BAU and stress assumptions.

## D. Market / reference curves

Retain:

- curve ID/version;
- currency;
- curve purpose;
- as-of timestamp;
- tenor nodes;
- rates;
- source instruments;
- day count and compounding;
- interpolation/extrapolation;
- approval status.

## E. Marginal funding curve

Retain:

- legal entity / issuer;
- currency;
- funding class and seniority;
- secured/unsecured;
- source transaction/quote/instrument;
- tenor nodes and rates/spreads;
- observation timestamp;
- primary vs proxy status;
- proxy hierarchy;
- manual overlays and approvals;
- stale-data tolerance.

## F. Liquidity stress / cushion data

Capture where relevant:

- scenario and version;
- idiosyncratic/systemic/combined stress;
- horizon and assumed market-disruption duration;
- draw/run-off factors;
- collateral-call assumptions;
- secured-funding roll-off;
- buffer asset inventory;
- haircuts;
- monetisation horizons;
- buffer yields;
- funding cost;
- legal/currency transfer restrictions;
- encumbrance.

## G. Applied FTP result

At instrument/cohort level retain:

- market/repricing horizon and rate;
- funding/liquidity horizon;
- marginal funding rate;
- term liquidity premium/benefit;
- contingent-liquidity amount/rate;
- behavioural/optionality adjustment if separately modelled;
- policy overlay;
- economic FTP;
- applied FTP;
- customer margin/contribution measure;
- annualised monetary impact;
- curve versions;
- model versions;
- methodology version;
- exception flags;
- calculation timestamp.

## H. Data-quality flags

Use explicit flags for:

- missing required data;
- stale curve;
- proxy funding curve;
- extrapolated tenor;
- manual override;
- unapproved curve/model;
- missing behavioural model;
- model outside calibration range;
- inconsistent cash flows;
- sign/reconciliation failure;
- duplicate exposure;
- legal-entity mismatch;
- currency mismatch;
- possible contingent-liquidity double count;
- regulatory source status not verified for live work.
