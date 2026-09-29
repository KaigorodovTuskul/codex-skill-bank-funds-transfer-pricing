# Bank Funds Transfer Pricing

A Codex skill for designing, auditing, calculating and implementing bank funds transfer pricing (FTP), including liquidity transfer pricing (LTP), matched-maturity marginal funding, behavioural products, contingent liquidity, governance and production controls.

This is a modernised successor to a narrower `bank-liquidity-transfer-pricing` concept. It treats FTP as the broader internal-pricing architecture and LTP as a major component rather than the whole framework.

## Core source stack

The skill deliberately combines several layers instead of treating any single publication as a complete modern FTP standard. Source status must be re-checked for live work. Links below point to the official publishers.

1. **BIS / FSI (2011)** — [*Liquidity transfer pricing: a guide to better practice*](https://www.bis.org/publications/fsi-paper-10-liquidity-transfer-pricing-guide-better-practice). Detailed LTP mechanics: matched-maturity marginal funding, liquidity premiums, behavioural products, contingent liquidity and governance.
2. **Federal Reserve / FDIC / OCC (2016)** — [*Interagency Guidance on Funds Transfer Pricing Related to Funding and Contingent Liquidity Risks*](https://www.federalreserve.gov/frrs/guidance/interagency-guidance-on-funds-transfer-pricing-related-to-funding-and-contingent-liquidity-risks.htm) (SR 16-3 / OCC Bulletin 2016-7). Practical supervisory guidance on funding-risk and contingent-liquidity FTP, product pricing, business metrics, new-product approval, governance and allocation granularity.
3. **Basel Framework — Liquidity Coverage Ratio (LCR)** — [current LCR standard](https://www.bis.org/committees/bcbs/basel-framework/standard/lcr). Current regulatory framework for short-term liquidity resilience, HQLA and stressed cash outflows/inflows.
4. **Basel Framework — Net Stable Funding Ratio (NSFR)** — [current NSFR standard](https://www.bis.org/committees/bcbs/basel-framework/standard/nsf). Current regulatory framework for structural funding stability.
5. **BCBS (2008, status: current)** — [*Principles for Sound Liquidity Risk Management and Supervision*](https://www.bis.org/publications/200809-guidelines-principles-sound-liquidity-risk-management-and-supervision). Sound-practice foundation for governance, liquidity-risk tolerance, allocation of liquidity costs/benefits/risks, stress testing and liquidity buffers.
6. **ECB (2018)** — [*ECB Guide to the internal liquidity adequacy assessment process (ILAAP)*](https://www.bankingsupervision.europa.eu/ecb/pub/pdf/ssm.ilaap_guide_201811.en.pdf). Supervisory expectations for integrating liquidity costs, benefits and risks into internal pricing, FTP, performance measurement and new-product approval.
7. **EBA SREP** — [SREP and Pillar 2 source page](https://eba.europa.eu/regulation-and-policy/supervisory-review-and-evaluation-process-srep-and-pillar-2) and the [26 June 2026 revised SREP Guidelines announcement](https://www.eba.europa.eu/publications-and-media/press-releases/eba-reaches-another-important-milestone-enhancing-supervisory-efficiency-its-revised-srep-guidelines). The 2026 revision is final but applies from 1 January 2027, so the skill requires version and applicability checks for live use.
8. **FSI (2024)** — [*Liquidity stress tests for banks – range of practices and possible developments*](https://www.bis.org/publications/fsi-insight-59-liquidity-stress-tests-banks-range-practices-and-possible-developments). Modern supplementary source for liquidity-stress assumptions, haircuts, outflow modelling, management actions, contagion and second-round effects; it is not an FTP manual.

The skill also monitors the [Basel Consolidated Guidelines liquidity module](https://www.bis.org/committees/bcbs/basel-consolidated-guidelines/module/lqy/10), but as of the source review date it is a **draft under consultation**, not a replacement for currently effective standards.

See [`references/source-framework.md`](references/source-framework.md) for source hierarchy, applicability classes, status rules and the distinction between regulatory constraints and economic FTP parameters.

## What it does

- designs bank-wide FTP/LTP methodology and governance;
- separates repricing/market transfer rates from term funding-liquidity and contingent-liquidity economics;
- distinguishes coupon reset tenor from funding horizon for floating-rate assets;
- builds/reviews marginal funding curves by entity, currency and funding class;
- maps bullet, amortising, prepayable and behavioural cash flows;
- handles non-maturity deposits and revolving/committed facilities;
- links contingent-liquidity pricing to stress testing and the liquidity cushion;
- audits existing FTP spreadsheets, policies and systems;
- converts approved methodology into data requirements, calculation rules, controls, reports and UAT;
- reconciles product/business profitability to Treasury residual;
- keeps foreign, historical and draft supervisory sources distinct from binding local requirements.

## Structure

```text
.
|- SKILL.md
|- README.md
|- agents/
|  `- openai.yaml
`- references/
   |- audit-checklist.md
   |- calculation-methods.md
   |- data-contract.md
   |- implementation-pack.md
   |- policy-template.md
   `- source-framework.md
```

## Installation

macOS/Linux:

```bash
git clone https://github.com/KaigorodovTuskul/codex-skill-bank-funds-transfer-pricing.git ~/.agents/skills/bank-funds-transfer-pricing
```

Windows PowerShell:

```powershell
git clone https://github.com/KaigorodovTuskul/codex-skill-bank-funds-transfer-pricing.git "$env:USERPROFILE\.agents\skills\bank-funds-transfer-pricing"
```

Explicit invocation:

```text
$bank-funds-transfer-pricing
```

## Example prompts

```text
$bank-funds-transfer-pricing Audit our current FTP methodology and quantify where using one average cost of funds distorts profitability by tenor.
```

```text
$bank-funds-transfer-pricing Build FTP for a floating-rate corporate loan portfolio. Separate rate-reset horizon from funding horizon and show the resulting transfer-rate bridge.
```

```text
$bank-funds-transfer-pricing Design the treatment of non-maturity deposits using behavioural decay and a stable/volatile segmentation. Keep BAU FTP assumptions separate from stress runoff.
```

```text
$bank-funds-transfer-pricing Turn this approved FTP methodology into an MVP system specification with product mappings, curve versioning, controls, reports and UAT cases.
```

```text
$bank-funds-transfer-pricing Prepare an ALCO pack explaining the change in marginal funding curves, impact on new-business pricing and Treasury residual.
```

## Important limitation

The skill is a methodology and implementation framework. It does not turn BIS, US or EU supervisory material into binding requirements for another jurisdiction. For live work it must first determine the applicable legal entity and jurisdiction and verify the current rules and source status.
