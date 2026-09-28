---
name: bank-funds-transfer-pricing
description: "Design, audit, calculate and implement bank funds transfer pricing (FTP), including interest-rate/repricing transfer rates, term funding liquidity, contingent liquidity, behavioural maturity, optionality interfaces, governance, profitability attribution and production controls."
---

# Bank Funds Transfer Pricing

Use this skill when the user asks to design, review, calculate, explain or implement a bank funds transfer pricing (FTP) framework, internal transfer curves, liquidity transfer pricing (LTP), matched-maturity pricing, behavioural deposit or loan treatment, contingent-liquidity charges, Treasury/ALCO methodology, product profitability attribution, or an FTP calculation system.

The skill synthesises several generations of supervisory and better-practice material rather than treating any one publication as a complete modern standard. The detailed LTP mechanics are grounded in Joel Grant, *Liquidity transfer pricing: a guide to better practice*, FSI Occasional Paper No 10 (BIS/FSI, 2011). The framework is modernised with the Federal Reserve/FDIC/OCC *Interagency Guidance on Funds Transfer Pricing Related to Funding and Contingent Liquidity Risks* (SR 16-3, 2016), the current Basel liquidity standards and sound-practice framework, ECB ILAAP expectations, and relevant current EBA supervisory material. Read [references/source-framework.md](references/source-framework.md) before treating any supervisory source as binding.

## Source hierarchy

For live work, apply sources in this order:

1. applicable law, regulation and supervisory requirements for the bank's jurisdiction and legal entity;
2. the bank's currently approved ALM/FTP/liquidity policy and model-governance rules;
3. current Basel standards and sound-practice material where applicable;
4. relevant supervisory guidance such as SR 16-3, ECB ILAAP and EBA SREP as comparative/better-practice material unless directly applicable;
5. BIS/FSI 2011 as a detailed LTP methodology benchmark.

Never present foreign supervisory guidance, a consultation draft, or historical better practice as binding local law.

## Core principles

1. **Fix the perimeter first.** Record `as_of_date`, legal entity, branch/group scope, currency, business unit, product population, purpose and methodology version before calculating. Do not silently mix legal entities or currencies.
2. **FTP is an allocation system, not one magic rate.** Separate components that answer different economic questions. At minimum distinguish:
   - market/repricing transfer component;
   - term funding-liquidity premium or benefit;
   - contingent-liquidity cost where relevant;
   - behavioural/optionality effects when policy requires them;
   - explicit policy or strategic overlays.
   Keep credit cost, capital cost, operating cost and commercial margin separate unless the bank's approved architecture deliberately includes them.
3. **Funding horizon and repricing horizon are not the same thing.** A floating-rate asset may reprice in three months while consuming one, three or five years of funding capacity. Model both horizons separately.
4. **Use matched-maturity marginal economics as the benchmark.** For material business, prefer marginal funding costs matched to the contractual or behavioural funding requirement rather than one historical average funding rate.
5. **Centralise risk, decentralise commercial decisions.** FTP should transfer funding and contingent-liquidity risks to a central Treasury/ALM function so business-unit profitability reflects risks created or benefits provided.
6. **Credit stable funding for the benefit actually provided.** Long-lived and behaviourally stable liabilities should generally receive a larger funding benefit than volatile or short-lived balances, subject to model evidence and policy.
7. **Price contingent liquidity.** Undrawn commitments, potential collateral calls, deposit run-off, secured-funding roll-off and other material stress liquidity needs must not be treated as free.
8. **Link contingent-liquidity cost to the liquidity cushion and stress framework.** The size, composition, haircut, monetisation horizon and carry/funding cost of standby liquidity should be consistent with the bank's stress assumptions and legal/currency constraints.
9. **Behavioural products need behavioural treatment.** Prepayable loans, mortgages, revolving products and non-maturity deposits should use approved decay, survival, drawdown, beta or cash-flow models where material.
10. **Do not substitute regulatory factors for economic FTP without a policy decision.** LCR/NSFR or supervisory stress factors may inform FTP but are not automatically the same as behavioural or marginal economic assumptions.
11. **Proportionality is allowed, silent simplification is not.** Simpler approaches are acceptable for immaterial portfolios when the threshold, rationale, impact and approval are documented.
12. **Version everything that can change an answer.** Curves, model parameters, product mappings, behavioural assumptions, stress factors, overlays and methodology rules must have effective dates and versions.
13. **Preserve historical reproducibility.** A historical transaction should be reproducible using the curve/model/policy versions applicable to its pricing or reset date.
14. **Separate observed, modelled and policy-set inputs.** Never make an expert overlay look like a market observation.
15. **Do not invent missing data.** Create a gap register and use sensitivities, bounded scenarios or approved fallbacks when necessary.
16. **Current-use answers require current-source verification.** Market benchmarks, regulation, supervisory status and benchmark conventions can change; check them when the task is for live use.

## FTP component architecture

Use the bank's approved architecture if one exists. Otherwise analyse the economics through the following bridge:

```text
customer rate / asset yield
  minus market or repricing transfer component
  minus term funding-liquidity charge
  minus contingent-liquidity charge
  minus other separately approved risk/cost components
= business commercial margin / contribution
```

For liabilities, the direction reverses: a liability that provides useful funding receives an internal funding benefit/credit. Always state sign conventions explicitly.

Do not assume that the final internal FTP rate must be a simple arithmetic sum for every product. Complex products may require discounted cash-flow replication, multiple cash-flow buckets, behavioural portfolios or option-adjusted methods.

## Work modes

### 1. Methodology design

Create or revise a bank-wide FTP methodology, policy, ALCO standard or product methodology. Use [references/policy-template.md](references/policy-template.md), [references/source-framework.md](references/source-framework.md) and [references/calculation-methods.md](references/calculation-methods.md).

### 2. Transaction / portfolio calculation

Calculate FTP for one transaction, product cohort or portfolio. Use [references/calculation-methods.md](references/calculation-methods.md) and [references/data-contract.md](references/data-contract.md). Show formulas, curve nodes, interpolation, assumptions, sign conventions and monetary impact.

### 3. Audit / gap analysis

Review an existing policy, model, spreadsheet or production engine. Use [references/audit-checklist.md](references/audit-checklist.md). For every material finding state evidence, economic effect, control/risk consequence, remediation and data required to quantify it.

### 4. System implementation

Translate approved methodology into product mappings, data contracts, curve stores, services, configuration, controls, reports and UAT. Use [references/implementation-pack.md](references/implementation-pack.md). Keep policy decisions out of hard-coded application logic wherever possible.

### 5. ALCO / management decision support

Prepare concise decision material showing curve changes, funding economics, affected products, profitability redistribution, Treasury residual, contingent-liquidity allocation, exceptions, limitations and proposed decisions. Preserve traceability from management totals to product or instrument-level calculations.

## Calculation workflow

1. **Classify the exposure.** Asset, liability or contingent; fixed/floating; bullet/amortising/revolving/non-maturity; secured/unsecured; currency; entity; product family; business unit.
2. **Map contractual cash flows.** Capture payment, repricing, maturity, amortisation, commitment and collateral terms.
3. **Map behavioural cash flows where needed.** Use approved prepayment, decay, drawdown, run-off, beta or behavioural-life models.
4. **Resolve the market/repricing curve.** Identify the bank-approved reference or replication curve appropriate to the product's rate risk and repricing structure.
5. **Resolve the marginal funding curve.** Use current entity/currency/funding-class economics or the approved proxy hierarchy.
6. **Derive the term funding-liquidity spread.** When architecture uses a spread decomposition, calculate the difference between the marginal funding curve and the comparable market/reference curve using consistent conventions.
7. **Apply matched maturity/cash-flow mapping.** Bullet products can use a matched tenor; amortising and behavioural products should normally map expected principal/cash-flow tranches across the curve or use DCF/IRR replication.
8. **Calculate contingent-liquidity cost.** Map expected/stressed usage to the cost of standby liquidity, consistent with the bank's cushion/stress framework.
9. **Apply approved overlays separately.** Strategic subsidies, floors, caps or management adjustments must remain visible and governed.
10. **Reconcile.** Bridge customer economics to business margin and Treasury result; reconcile instrument → product → business → bank totals.
11. **Test.** Run sensitivity to curve shape, funding spreads, behavioural life, prepayment, deposit decay, draw factors, stress horizon, haircuts and proxy choices.

## Product-routing rules

### Fixed-rate bullet assets and liabilities

Use matched-maturity market/repricing and funding economics for the relevant horizon. Do not apply one pooled rate across materially different maturities.

### Floating-rate assets and liabilities

Separate:

```text
repricing component -> next reset / relevant market index horizon
funding-liquidity component -> contractual or behavioural funding horizon
```

Do not price a multi-year floating asset as a three-month liquidity exposure merely because its coupon resets every three months.

### Amortising loans

Map principal repayments by tenor or use a DCF/IRR method. Contractual final maturity alone is usually insufficient when principal amortises materially before final maturity.

### Prepayable mortgages and loans

Use expected cash flows or behavioural life based on an approved prepayment/decay model. Keep BAU modelling separate from liquidity stress assumptions unless policy explicitly links them.

### Non-maturity deposits

Segment balances by stability and rate sensitivity where evidence supports it. Use behavioural decay/replicating treatment for funding-benefit attribution. Do not credit the entire balance as long-term stable funding solely because historical balances were sticky, and do not reduce economic FTP to a regulatory runoff percentage without methodology approval.

### Revolving / committed facilities

Price the drawn portion using on-balance-sheet FTP and the undrawn portion using a contingent-liquidity charge based on expected or stress usage and standby-liquidity cost. Prevent double counting.

### Trading, secured funding and derivatives

Where material, recognise secured vs unsecured funding, collateral haircuts, tenor, margin/collateral calls, close-out or downgrade triggers, and stressed funding outflows. Use the bank's trading-book methodology rather than forcing a retail-loan template onto these exposures.

## Governance expectations

- A central Treasury/ALM or funding function should own or operate the FTP framework; responsibilities must be explicit.
- Risk and Finance/Control should provide independent challenge appropriate to the bank's governance model.
- ALCO or equivalent senior management should approve material methodology principles and review material changes/exceptions.
- Business lines should understand how FTP affects pricing and performance; Treasury should understand product funding and contingent-liquidity characteristics.
- Behavioural models should have owners, calibration data, validation/backtesting, limitations, review frequency and fallbacks.
- Curve/model changes and manual overrides should have maker-checker controls, timestamps, rationale and approval.
- Centrally retained FTP costs/benefits should be explicit and analysed for incentive effects; unexplained Treasury residual is a diagnostic signal.
- New-product approval should identify the product's FTP treatment before material origination begins.

## Red flags

Treat these as investigation triggers, not automatic proof of failure:

- no formal FTP/LTP methodology;
- zero or near-zero funding/liquidity charge for material balance-sheet usage;
- one average historical funding rate for all tenors;
- no distinction between repricing tenor and funding horizon;
- final contractual maturity used for heavily amortising/prepayable assets without justification;
- non-maturity deposits credited as long-term stable funding without behavioural evidence;
- undrawn commitments or collateral calls excluded from pricing;
- liquidity-cushion cost left entirely in Treasury or socialised across unrelated products;
- stale curves or ungoverned spreadsheet overrides;
- different legal entities/currencies using one curve without a transferability rationale;
- current business pricing based on an obsolete benchmark convention;
- regulatory LCR/NSFR factors used mechanically as economic FTP assumptions;
- no reconciliation from deal-level FTP to business profitability and Treasury residual;
- no historical curve/model versioning;
- foreign or draft supervisory guidance represented as binding local regulation.

## Output discipline

For calculations, include at least:

- as-of date, entity, currency and methodology version;
- product classification and contractual/behavioural horizons;
- market/repricing curve source;
- marginal funding curve source and funding class;
- relevant curve points and interpolation/extrapolation;
- term funding-liquidity component;
- contingent-liquidity component where relevant;
- policy overlay if any;
- rate result and monetary result where possible;
- observed vs modelled vs policy-set inputs;
- sensitivity/limitations;
- reconciliation to the intended profitability measure.

For audits, group findings by governance, scope, curve construction, product mapping, behavioural models, contingent liquidity, stress/cushion linkage, data/systems, profitability attribution, model risk and controls.

## Deliverables

The output can be a Markdown methodology, ALCO memo, spreadsheet model/specification, implementation backlog, test pack or code model. When the user requests DOCX, PPTX or XLSX, use the corresponding artifact workflow and keep calculation lineage visible.

Read [references/source-framework.md](references/source-framework.md) for source status and applicability; [references/calculation-methods.md](references/calculation-methods.md) for deterministic formulas; [references/data-contract.md](references/data-contract.md) before requesting data; [references/audit-checklist.md](references/audit-checklist.md) for reviews; [references/policy-template.md](references/policy-template.md) for methodology drafting; and [references/implementation-pack.md](references/implementation-pack.md) for production design.

## Completion gate

Before delivery verify that: the legal entity, currency, as-of date and product perimeter are explicit; the current applicable source hierarchy was checked for live work; repricing and funding horizons are separated where needed; the marginal funding curve is economically relevant; cash-flow and behavioural treatment match the product; contingent liquidity is considered; regulatory factors are not silently substituted for economic assumptions; overlays and simplifications are visible; curve/model versions are reproducible; sign conventions are clear; and instrument-level results reconcile to portfolio/business/Treasury reporting.
