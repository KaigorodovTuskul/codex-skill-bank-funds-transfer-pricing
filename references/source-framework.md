# Source framework and applicability

Last source-status review for this skill: 2026-09-29. Re-check status before any live regulatory conclusion.

## 1. Binding-source rule

No international or foreign supervisory publication becomes binding merely because it is cited by this skill. Determine:

- legal entity and booking location;
- home/host supervisor;
- applicable national law and prudential rules;
- group vs solo requirements;
- currency-specific or resolution/liquidity-transfer constraints;
- the bank's approved internal policy.

Classify every external source as one of:

```text
BINDING_LOCAL
APPLICABLE_GROUP_STANDARD
SUPERVISORY_EXPECTATION
INTERNATIONAL_STANDARD
BETTER_PRACTICE
HISTORICAL_REFERENCE
DRAFT_OR_CONSULTATION
```

Never collapse these categories.

## 2. BIS / FSI LTP benchmark — 2011

Joel Grant, *Liquidity transfer pricing: a guide to better practice*, FSI Occasional Paper No 10, Bank for International Settlements / Financial Stability Institute, 30 December 2011.

Official publication page:
https://www.bis.org/publications/fsi-paper-10-liquidity-transfer-pricing-guide-better-practice

Use for:

- matched-maturity marginal cost-of-funds logic;
- charging liquidity users and crediting funding providers;
- amortising / blended marginal rates;
- behavioural treatment of non-maturity products;
- contingent-liquidity allocation;
- stress-linked liquidity-cushion sizing and cost attribution;
- governance and central Treasury ownership concepts.

Status in this skill: `BETTER_PRACTICE` / `HISTORICAL_REFERENCE`.

Do not hard-code 2011 benchmark conventions, market instruments or rate examples.

## 3. Federal Reserve / FDIC / OCC SR 16-3 — 2016

*Interagency Guidance on Funds Transfer Pricing Related to Funding and Contingent Liquidity Risks*, 1 March 2016.

Official Federal Reserve page:
https://www.federalreserve.gov/frrs/guidance/interagency-guidance-on-funds-transfer-pricing-related-to-funding-and-contingent-liquidity-risks.htm

Use for:

- FTP as a central allocation of funding and contingent-liquidity costs/benefits;
- product pricing, business metrics and new-product approval;
- granular allocation based on characteristics that create funding/liquidity risk;
- central management of funding risk;
- governance, consistency, transparency and documentation;
- centrally retained FTP costs/benefits and incentive analysis;
- trading, secured funding, haircuts, derivatives and potential stressed outflows.

Status in this skill: `SUPERVISORY_EXPECTATION` for institutions within its scope; otherwise `BETTER_PRACTICE` comparator.

Do not assume its original US scope threshold or applicability automatically maps to another bank or jurisdiction.

## 4. BCBS Principles for Sound Liquidity Risk Management and Supervision

Official BIS page:
https://www.bis.org/publications/200809-guidelines-principles-sound-liquidity-risk-management-and-supervision

The 2008 principles remain marked current by BIS as of the skill's source review.

Use for:

- liquidity-risk tolerance and governance;
- allocating liquidity costs, benefits and risks to significant activities;
- liquidity cushion;
- severe stress testing;
- contingency funding;
- collateral and intraday liquidity context.

Status: `INTERNATIONAL_STANDARD` / sound-practice foundation, subject to national implementation.

## 5. Current Basel Framework — LCR and NSFR

Liquidity Coverage Ratio:
https://www.bis.org/committees/bcbs/basel-framework/standard/lcr

Net Stable Funding Ratio:
https://www.bis.org/committees/bcbs/basel-framework/standard/nsf

Use for:

- current regulatory liquidity context;
- HQLA, outflows/inflows and regulatory liquidity horizon context;
- structural stable-funding requirements;
- legal-entity/currency transfer restrictions where applicable.

Do not automatically use LCR runoff factors or NSFR ASF/RSF factors as economic FTP parameters. They can inform or constrain the methodology, but economic and regulatory objectives differ.

## 6. Basel Consolidated Guidelines liquidity module — 2026 draft

BIS page:
https://www.bis.org/committees/bcbs/basel-consolidated-guidelines/module/lqy/10

At the skill's source review date, BIS labels the Consolidated Guidelines as a draft under consultation.

Status: `DRAFT_OR_CONSULTATION`.

Use only as an orientation/source-routing aid unless its status changes. Verify status before citing it as current guidance.

## 7. ECB ILAAP Guide

*ECB Guide to the internal liquidity adequacy assessment process (ILAAP)*.

Official ECB PDF landing/source:
https://www.bankingsupervision.europa.eu/ecb/pub/pdf/ssm.ilaap_guide_201811.en.pdf

Use for the expectation that a bank integrates liquidity costs, benefits and risks into internal pricing, FTP, performance measurement and new-product approval, and for ILAAP consistency and transferability considerations.

Status: `SUPERVISORY_EXPECTATION` for relevant ECB-supervised institutions; otherwise a useful comparative benchmark.

## 8. EBA SREP Guidelines

Official EBA page:
https://eba.europa.eu/regulation-and-policy/supervisory-review-and-evaluation-process-srep-and-pillar-2

26 June 2026 revised SREP announcement:
https://www.eba.europa.eu/publications-and-media/press-releases/eba-reaches-another-important-milestone-enhancing-supervisory-efficiency-its-revised-srep-guidelines

As of the skill's source review, the 2026 revised SREP Guidelines were final and scheduled to apply from 1 January 2027. Until then, verify which earlier version remains applicable in the relevant jurisdiction and supervisory context.

Use for:

- supervisory assessment of liquidity and funding risk;
- proportionality and risk-focused supervisory context;
- stress-testing context.

Status depends on version and date. Always check the current version/applicability before relying on it.

## 9. FSI liquidity stress-testing update — 2024

FSI Insights No 59, *Liquidity stress tests for banks – range of practices and possible developments*, 11 October 2024.

Official BIS page:
https://www.bis.org/publications/fsi-insight-59-liquidity-stress-tests-banks-range-practices-and-possible-developments

Use as a modern supplementary source for liquidity stress assumptions, second-round effects, outflow assumptions, haircuts and modelling limitations. It is not an FTP manual.

## 10. How to use the source stack

For methodology design, build a source table:

| Topic | Binding/local source | Current international source | Better-practice source | Bank policy | Gap |
|---|---|---|---|---|---|
| FTP governance |  | BCBS principles | SR 16-3 / BIS 2011 |  |  |
| marginal funding curve |  |  | BIS 2011 / SR 16-3 |  |  |
| contingent liquidity |  | LCR/stress framework | SR 16-3 / BIS 2011 |  |  |
| NMD behaviour |  | relevant local IRRBB/liquidity rules | BIS 2011 / SR 16-3 |  |  |
| liquidity cushion |  | LCR / BCBS principles | BIS 2011 |  |  |
| performance attribution |  | BCBS principles | SR 16-3 / ECB ILAAP |  |  |

If the current local source contradicts a better-practice source, the local requirement governs compliance. Record the economic consequence separately if the user is analysing management FTP rather than pure regulatory compliance.
