# Bank Funds Transfer Pricing

A Codex skill for designing, auditing, calculating and implementing bank funds transfer pricing (FTP), including liquidity transfer pricing (LTP), matched-maturity marginal funding, behavioural products, contingent liquidity, governance and production controls.

This is a modernised successor to a narrower `bank-liquidity-transfer-pricing` concept. It treats FTP as the broader internal-pricing architecture and LTP as a major component rather than the whole framework.

## Core source stack

The skill deliberately combines several layers instead of pretending that one document is a complete modern standard:

1. **BIS/FSI (2011)** — *Liquidity transfer pricing: a guide to better practice*: detailed LTP mechanics and better-practice concepts.
2. **Federal Reserve / FDIC / OCC (2016), SR 16-3** — practical supervisory guidance on funding risk and contingent-liquidity FTP.
3. **Current Basel Framework** — current LCR/NSFR standards and liquidity-risk context.
4. **BCBS Principles for Sound Liquidity Risk Management and Supervision** — current sound-practice foundation for liquidity governance and allocation of liquidity costs/benefits/risks.
5. **ECB ILAAP Guide** — liquidity costs, benefits and risks in internal pricing, FTP, performance measurement and new-product approval.
6. **EBA SREP material** — current supervisory context for liquidity and funding-risk assessment. The 2026 revised SREP Guidelines are final but were still not yet applicable when this skill was assembled; the skill therefore requires status verification for live use.

See `references/source-framework.md` for status and applicability rules.

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

No license has been assigned yet. Until one is added, repository reuse is not automatically granted.
