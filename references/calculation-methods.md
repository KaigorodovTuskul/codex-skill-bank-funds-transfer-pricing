# FTP calculation methods

Use this file for deterministic calculation logic. First identify the bank's approved FTP architecture. Do not force a spread-decomposition model onto a bank that uses full replication/DCF, but always separate economic components conceptually.

## 1. Rate conventions

Before any calculation align:

- currency;
- curve date;
- day-count basis;
- compounding;
- zero/par/forward representation;
- tenor definition;
- interpolation/extrapolation;
- secured/unsecured and seniority class;
- legal entity.

Never subtract or compare rates with inconsistent conventions without transformation.

## 2. Spread-decomposition architecture

Where the bank separates a market/reference curve from bank funding liquidity, for tenor `t`:

```text
LP(t) = MFC(t) - REF(t)
```

where:

- `LP(t)` = term funding-liquidity premium;
- `MFC(t)` = marginal funding cost for the relevant entity/currency/funding class;
- `REF(t)` = comparable bank-approved market/reference curve.

The full internal transfer rate can then be expressed as:

```text
FTP = market_or_repricing_component
    + term_funding_liquidity_component
    + contingent_liquidity_component
    + separately_approved_overlays
```

Treat this as an explanatory bridge, not a universal accounting identity.

## 3. Fixed-rate bullet asset

For a simple bullet asset with horizon `T`:

```text
market_component = REF(T)
liquidity_component = LP(T)
core_funding_FTP = MFC(T)
```

The business receives customer yield and is charged the internal funding transfer price according to policy.

If `T` falls between nodes, use approved interpolation and disclose surrounding nodes.

## 4. Bullet liability

A liability provides funding benefit. Under a matched-maturity approach, the internal credit should reflect the funding value of the balance and its relevant behavioural/contractual horizon, less any components retained centrally under policy.

Do not apply asset sign conventions blindly. State whether the reported number is:

- a positive internal credit to the liability business;
- a negative FTP charge;
- or a Treasury-side cost.

## 5. Floating-rate instruments

Separate rate-reset exposure from funding commitment.

Illustrative decomposition:

```text
market_component = reference/forward rate consistent with reset structure
liquidity_component = LP(contractual_or_behavioural_funding_horizon)
```

A three-year loan resetting quarterly can therefore have a quarterly market reset but a multi-year liquidity component.

For full replication, model each reset/cash-flow period explicitly rather than replacing the structure with one spot tenor.

## 6. Amortising instruments — cash-flow tranching

Map principal cash flows to liquidity tenors.

A useful weighted approximation is:

```text
blended_LP = sum(P_i * t_i * LP(t_i)) / sum(P_i * t_i)
```

where:

- `P_i` = principal repayment amount;
- `t_i` = time to repayment;
- `LP(t_i)` = liquidity premium at that tenor.

This approximation reflects both amount and funding duration. For irregular or rate-sensitive cash flows, prefer DCF/IRR replication.

### BIS/FSI validation example

For a five-year linearly amortising exposure with liquidity premiums 5, 10, 18, 28 and 40 bps at years 1–5:

```text
(1*5 + 2*10 + 3*18 + 4*28 + 5*40) / (1+2+3+4+5)
= 26.1 bps
```

Use only as a unit test of implementation logic, not as a market assumption.

## 7. DCF / IRR replication

Use when:

- cash flows are irregular;
- the yield curve is strongly non-linear;
- reset timing matters;
- the bank's policy uses present-value replication;
- simple weighted averages are not sufficiently accurate.

Possible implementation:

1. value expected contractual/behavioural cash flows on the market/reference curve;
2. value/solve them on the bank marginal funding curve;
3. solve for the constant transfer spread or equivalent internal rate that reconciles the two present values;
4. preserve solver settings, convergence tolerance and curve versions.

## 8. Behavioural maturity and WAL

For expected principal cash flows:

```text
WAL = sum((P_i / P_total) * t_i)
```

WAL is descriptive. When the curve is non-linear or cash flows are dispersed, full cash-flow mapping is preferable.

## 9. Prepayable mortgages / loans

1. segment by relevant cohort/vintage/product characteristics;
2. estimate survival/prepayment behaviour;
3. produce expected principal cash flows;
4. map cash flows to FTP curves;
5. quantify sensitivity to faster/slower prepayment;
6. backtest and version the model.

Do not use contractual final maturity alone when prepayment materially changes funding duration.

## 10. Non-maturity deposits

A practical framework separates:

```text
total balance
= volatile / short-lived component
+ stable / behavioural component
```

Then:

1. estimate decay/survival and rate sensitivity;
2. derive behavioural cash-flow buckets or a replicating portfolio;
3. credit the funding benefit by tenor;
4. apply optionality/behavioural adjustments if policy requires;
5. keep BAU FTP behaviour distinct from stress run-off assumptions.

Do not treat contractual overnight maturity or an LCR runoff factor as the sole economic maturity assumption.

## 11. Contingent-liquidity charge

For a committed line:

```text
undrawn = limit - drawn
expected_usage = undrawn * draw_factor
contingent_charge_amount = expected_usage * standby_liquidity_cost
```

Rate on total limit:

```text
charge_rate_on_limit = (undrawn / limit) * draw_factor * standby_liquidity_cost
```

### BIS/FSI validation example

```text
limit = 10,000,000
drawn = 4,000,000
draw_factor = 60%
standby_liquidity_cost = 18 bps

undrawn = 6,000,000
expected_usage = 3,600,000
charge = 3,600,000 * 0.0018 = 6,480
rate_on_limit = 6.48 bps
```

Use as a calculation check only.

## 12. Liquidity-cushion economics

A simplified annual carry measure:

```text
cushion_carry_cost = funding_cost_of_buffer - yield_on_buffer_assets
```

Refine for:

- haircut-adjusted usable liquidity;
- monetisation horizon;
- encumbrance;
- collateral eligibility;
- secured/unsecured funding assumptions;
- legal-entity/currency transfer restrictions;
- operational availability;
- stress duration;
- concentration and market depth.

Allocate cushion cost to the activities that create the standby-liquidity requirement. Do not mechanically divide it by total assets.

## 13. Trading / secured funding / derivatives

Where material, distinguish:

- secured vs unsecured funding spreads;
- asset-specific haircuts;
- repo/reverse-repo tenor;
- margin requirements;
- derivative collateral calls;
- downgrade/additional-termination triggers;
- wrong-way or concentration effects;
- roll-over assumptions.

Do not force a loan-style WAL method onto a trading exposure if transaction-level secured funding is the more relevant driver.

## 14. Policy overlays

Strategic pricing subsidy, product incentive, floor/cap or management overlay must be shown separately:

```text
economic_FTP
+/- policy_overlay
= applied_FTP
```

Record owner, reason, approval, start/end date and expected P&L transfer.

## 15. Reconciliation

At minimum reconcile:

```text
customer income/expense
- market/repricing FTP component
- funding-liquidity component
- contingent-liquidity component
- other approved internal components
= business contribution
```

Then reconcile business totals to Treasury/central funding result and explain centrally retained amounts.

## 16. Sensitivity set

Consider:

- parallel/non-parallel market curve shifts;
- marginal funding spread widening/tightening;
- curve steepening/flattening;
- alternative proxy funding curves;
- shorter/longer behavioural life;
- higher/lower prepayment;
- deposit decay and rate-beta changes;
- contingent draw/run-off factors;
- stress duration;
- buffer haircuts/yield;
- legal-entity/currency transferability constraints.
