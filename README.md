# 🌿 **DNA Methylation Analysis of GSE42861 (Illumina 450K Array)**

*A personal methylation analysis project using R & Bioconductor.*

[![R](https://img.shields.io/badge/R-4.3.3-blue.svg)]()
[![Bioconductor](https://img.shields.io/badge/Bioconductor-3.17-green.svg)]()
[![Illumina](https://img.shields.io/badge/Platform-Illumina%20450K-orange.svg)]()
[![License](https://img.shields.io/badge/License-MIT-lightgrey.svg)]()
[![Status](https://img.shields.io/badge/Status-Completed-brightgreen.svg)]()
[![GEO](https://img.shields.io/badge/Data-GSE42861-blue.svg)]()

---

## ✨ **Introduction**

This repository documents my first complete exploration of Illumina 450K DNA methylation array data.
I carried out this analysis as a way to understand how raw IDAT files are processed, how quality control and normalization work, and how differential methylation is identified and interpreted.

To keep the analysis manageable on a personal computer, I selected a small subset of **six samples** from the GEO dataset **GSE42861** (three RA cases and three controls).
These data are Downloaded Through http link provided the database, which will result in **GSE42861_RAW.tar** Folder containing the zipped IDAT files once we extract it. 


<img width="778" height="491" alt="image" src="https://github.com/user-attachments/assets/88e8d133-6109-413a-91f4-e3439989afff" />


Please keep these files inside the **raw_idats** folder and start the analysis.

This project helped me understand each processing step—from how methylation data are structured to how CpGs are linked to biological pathways through functional enrichment.

Rather than being a tutorial, this repository is a **well-documented record of my personal learning project**, written in a way that I hope will remain clear and useful for anyone who explores similar data.

---

# 📂 **Repository Structure**

```
DNA Methylation Analysis of GSE42861 Illumina 450K Array/
│
├── raw_idats/
│   └── SampleSheet.csv
│
├── results/
│   ├── DMP_all.csv
│   ├── DMP_significant.csv
│   ├── DMP_annotated.csv
│   └── GREAT_results.rds
│
└── docs/
|   ├── DNA_Methylation.Rmd
|   ├── DNA_Meth_Analysis_Arr_Data.pdf
|   ├── Methylation_Concepts.md
|   ├── Pipeline_Flowchart.md
|   └── RA_Biological_Background.md
│
├── Interpretation_Of_Key_Results.md

```

### **📂 raw_idats/**

Contains only the **SampleSheet.csv**, which maps each sample to its IDAT filenames.
The IDAT files themselves were used during the analysis but were removed before uploading to keep the repository lightweight.
The actual folder structure will look something like this after unzipping the files through the code mentioned in the .Rmd file as well as the explainatory pdf.


<img width="820" height="536" alt="image" src="https://github.com/user-attachments/assets/0d7768d8-0ce4-4d5c-b709-d76cb8ee3cac" />



### **📂 results/**

This folder stores all final outputs from the analysis:

* **DMP_all.csv** — Complete differential methylation results
* **DMP_significant.csv** — CpGs passing both FDR and Δβ cutoffs
* **DMP_annotated.csv** — Gene-annotated CpGs
* **GREAT_results.rds** — Functional enrichment output

These files represent the key deliverables of the entire workflow.


### **📂 docs/**

Contains the full analysis and documentation:

* **DNA_Methylation.Rmd** — The complete R workflow
* **DNA_Meth_Analysis_Arr_Data.pdf** — A detailed report summarizing the results and figures


### 📝 **Interpretation_Of_Key_Results.md**

This file provides a clear interpretation of all plots and results from the RA vs. control methylation analysis. 
It explains QC checks, normalization, PCA, volcano plots, and enrichment outputs in simple terms, helping readers understand 
what each visualization means and its biological relevance.

---

# 🧬 **Project Summary**

The analysis begins with loading the raw IDAT files using `minfi`, followed by standard quality control using detection p-values.
All six samples passed QC without issues.

Normalization was performed using **NOOB**, which handles background correction and dye bias. Once normalized, probes were filtered based on common criteria such as SNP overlaps, cross-reactivity, and sex-chromosome locations.

A PCA was used to explore inherent structure in the data, showing mild but noticeable clustering of RA vs. control samples.

Differential methylation analysis was carried out using the **limma** framework, applying both statistical (FDR) and biological (Δβ) thresholds. The significant CpGs were annotated and submitted to **GREAT** for functional enrichment, revealing developmental and morphogenesis-related pathways.

All steps and figures are included in the Rmd and PDF documentation.

---

# 📊 **Visual Output**

One of the main summaries from the enrichment analysis was a set of GO terms associated with the significant CpGs. The enhanced barplot and other visualizations (PCA plot, volcano plot, beta distributions, etc.) are available in the PDF report.



## 🔗 **Quick Navigation**

* 👉 **[Interpretation Of Key Results](./Interpretation_Of_Key_Results.md)**
* 👉 **[raw_idats/](./raw_idats/)**
* 👉 **[results/](./results/)**
* 👉 **[docs/](./docs/)**

  * 📄 [DNA_Methylation.Rmd](./docs/DNA_Methylation.Rmd)
  * 📘 [DNA_Meth_Analysis_Arr_Data.pdf](./docs/DNA_Meth_Analysis_Arr_Data.pdf)
  * 📑 [Methylation_Concepts.md](./docs/Methylation_Concepts.md)
  * 🧩 [Pipeline_Flowchart.md](./docs/Pipeline_Flowchart.md)
  * 🧬 [RA_Biological_Background.md](./docs/RA_Biological_Background.md)


---

# 🛠️ **Troubleshooting Notes**

A few small hiccups came up while working through the project:

* **File mapping:**
  The `Basename` field in SampleSheet must match the shared IDAT prefix exactly. Adding `_Red.idat` or `_Grn.idat` will cause errors.

* **Annotation installation:**
  Occasionally the annotation package installation took multiple attempts, but worked after retrying.

* **GREAT server timeouts:**
  GREAT occasionally timed out; retrying usually resolved it.

These are normal small challenges when working through a 450K pipeline for the first time.

---

# 📎 **Version Information**

The pipeline was run using the following software environment:

### **R & Bioconductor**

* R version: **4.3.3**
* Bioconductor version: **3.17**

### **Key Packages**

* **minfi**: 1.50.x
* **limma**: 3.58.x
* **IlluminaHumanMethylation450kanno.ilmn12.hg19**
* **IlluminaHumanMethylation450kmanifest**
* **rGREAT**
* **tidyverse**

### **Hardware**

* Windows 11
* 16 GB RAM
* Analysis performed locally

I am including this information because it helps ensure the analysis can be reproduced and clarifies the environment I worked in.

---

# 👩‍🔬 **Author**

**Gayatri Samant** :
(Bioinformatics learner exploring genomic and epigenomic data analysis.)

- This repository reflects my attempt to document a complete Illumina 450K methylation analysis in a clean, reproducible, and understandable way.
- Feel free to explore the repository, read through the documentation, or reach out if you’d like to discuss methylation workflows or improvements.



## **"The goal was not perfection but growth—understanding the data, learning the workflow, and presenting it clearly."**



