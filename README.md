# glioma_transcript_project

Transcriptomic biomarker research for IDH-mutant glioma — Oldham Lab, UCSF Department of Neurological Surgery.

This repo contains a standalone prognostic risk-score calculator built from a 4-gene signature
(**DEPDC1, GREM1, PLD1, TMEM165**), discovered in the CGGA RNA-seq cohort and cross-platform
validated in a pooled Gravendeel + Kamoun + Weller Affymetrix cohort.

## Contents

- **[`glioma_risk_score.html`](./glioma_risk_score.html)** — the risk-score calculator. Single
  self-contained HTML file (Chart.js embedded inline, no build step, no server, works fully
  offline). Open it directly in any browser.
  - Single-sample mode: enter CPM/TPM values for the 4 genes, get a linear predictor score,
    a Low/Intermediate/High risk category, a 95% confidence interval, and a per-gene
    contribution breakdown.
  - Batch mode: upload a CSV of samples and score them all at once, with a CSV export of results.
  - Shows the discovery cohort's own score distribution and the pooled validation cohort's
    Kaplan–Meier survival curves inline, so the tool's evidence is inspectable, not just a number.
  - **Research tool only — not validated for clinical decision-making.**

- **[`SESSION_SUMMARY.md`](./SESSION_SUMMARY.md)** — full methodology writeup: the Cox
  proportional-hazards pipeline (outlier removal, quantile normalization, ComBat batch
  correction, gene-level FDR correction), per-cohort data-quality issues found and resolved,
  the discovery-cohort statistics behind each of the 4 genes, and the cross-platform
  validation result (log-rank p = 0.00058).

## Key result

| Gene | HR (per SD, CGGA discovery) | q-value | Grade-independent? |
|---|---|---|---|
| DEPDC1 | 1.478 | 4.47×10⁻¹⁰ | Yes |
| TMEM165 | 1.644 | 1.32×10⁻⁵ | Yes |
| GREM1 | 1.229 | 1.60×10⁻² | No |
| PLD1 | 1.244 | 2.57×10⁻² | Yes |

Pooled validation cohort (n=272, independent microarray platform), tertile risk split:
median survival 6.3 / 6.7 / 4.9 years (Low/Intermediate/High), log-rank p = 0.00058.

## Status

The R pipeline scripts used to generate these results are being developed alongside this repo
and aren't included here yet. This repo currently holds the finished, user-facing tool and its
methodology documentation.
