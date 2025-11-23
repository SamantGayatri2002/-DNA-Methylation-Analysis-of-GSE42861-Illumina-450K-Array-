# DNA Methylation Analysis — Detailed Summary

## Overview
This project analyzes Illumina 450K methylation array data (GSE42861) comparing Rheumatoid Arthritis (RA) patients vs. controls. Six samples (3 RA, 3 controls) were processed using R (Bioconductor).

---
## 1. Quality Control (QC)
### Detection P-values
- **What it shows:** Confidence that probes are detected above background.
- **Result:** Median p-value = 0; <0.2% failed probes per sample.
- **Interpretation:** All samples passed QC (no sample >5% failed probes). Data is reliable.

### plotQC
- **What it shows:** Median intensities per sample.
- **Interpretation:** No outliers → good technical quality.

---
## 2. Normalization (NOOB)
- **Purpose:** Correct background and dye bias.
- **Density Plot:** Overlapping beta-value curves across samples.
- **Interpretation:** Normalization successful; no major technical artifacts.

---
## 3. Probe Filtering
- Removed SNP-affected probes and sex chromosome probes.
- **Why:** Avoid false positives and sex-related confounding.

---
## 4. PCA Plot
- **What it shows:** Principal Component Analysis of top 5,000 variable CpGs.
- **Result:** Modest RA vs. control separation; two mild outliers.
- **Interpretation:** Biological variability likely; no batch effect detected.

---
## 5. Differential Methylation Analysis
- **Method:** limma on M-values; Δβ computed from beta-values.
- **Threshold:** FDR < 0.05 and |Δβ| ≥ 0.10.
- **Result:** ~6,489 significant CpGs.

### Example Top Hits:
| CpG ID | chr | Δβ | FDR | Gene |
|--------|-----|----|-----|------|
| cg00007426 | chr2 | +0.1003 | 6.3e-08 | — |
| cg00017059 | chr2 | +0.1296 | 9.1e-09 | SRBD1 |
| cg00017203 | chr8 | +0.1611 | 5.3e-07 | PLEC1 |

**Interpretation:** Positive Δβ = hypermethylation in RA; negative Δβ = hypomethylation.

---
## 6. Volcano Plot
- **Axes:** Δβ vs. −log10(FDR).
- **Interpretation:** Red points = significant CpGs; right = hypermethylated; left = hypomethylated.

---
## 7. GREAT GO Enrichment
- **Plots:** Top 10 GO terms for Biological Process, Molecular Function, Cellular Component.
- **Interpretation:** Immune-related processes enriched (e.g., cytokine signaling).

---
## Biological Meaning
- RA vs. control shows widespread methylation differences in blood, reflecting immune involvement and cell composition effects.
- Findings are exploratory due to small sample size.

---
## Next Steps
1. Increase sample size for robust results.
2. Adjust for cell composition (Houseman method).
3. Perform region-level analysis (DMRcate).
4. Validate top CpGs in independent datasets.

---
## Session Info
- R 4.3.3, Bioconductor 3.17, Windows 11.

---
*Prepared for: Gayatri Samant*
