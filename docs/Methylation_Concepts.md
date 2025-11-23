# 📌 DNA Methylation and Illumina 450K Array — Concepts Explained

This document provides a clear, beginner-friendly overview of how DNA methylation works and how the Illumina 450K array measures it.

---

## 🧬 What is DNA Methylation?

DNA methylation is an epigenetic modification where a methyl group (–CH₃) is added to the **5th carbon of cytosine**, primarily at **CpG dinucleotides**.

### 🔹 Key biological roles:
- Regulation of gene expression  
- X-chromosome inactivation  
- Genomic stability  
- Embryonic development  
- Immune cell differentiation  
- Environmental response and disease susceptibility  

Methylation does **not** change the DNA sequence — it modifies how genes are read.

---

## 🧬 CpG Islands, Shores, Shelves, and Open Seas

The genome contains different CpG-dense regions:

- **CpG islands:** High CpG density, usually at promoters  
- **CpG shores:** 0–2 kb from islands  
- **CpG shelves:** 2–4 kb from islands  
- **Open sea:** Isolated CpGs far from islands  

Methylation patterns differ across these regions and help regulate gene activity.

---

## 🧬 What Does the Illumina 450K Array Measure?

The Illumina HumanMethylation450 BeadChip measures methylation at **~485,000 CpGs** across the genome using two fluorescent intensities:

- **Methylated signal (M)**
- **Unmethylated signal (U)**

The array outputs a **Beta value** for each CpG:

\[
\text{Beta} = \frac{M}{M + U + 100}
\]

### Interpretation:
- **0.0 → fully unmethylated**
- **1.0 → fully methylated**
- Most CpGs fall between **0.2–0.8**

Beta values are intuitive but not ideal for statistical modeling.

---

## 🧬 M-values (Used for Statistics)

Because Beta values have uneven variance near 0 and 1, differential testing is usually performed on **M-values**, defined as:

\[
M = \log_2 \left( \frac{M + 1}{U + 1} \right)
\]

- M-values approximate a normal distribution  
- Limma and other statistical methods work better with them  
- Interpretation is less intuitive than Beta values, so results are often converted back to Beta for reporting

---

## 🧬 Infinium Probe Types (Type I vs Type II — In depth)

The 450K array uses two probe chemistries, and understanding them is essential for good preprocessing.

---

### 🔹 **Type I Probes**
- Use **two separate probes** per CpG:  
  - one for methylated signal  
  - one for unmethylated signal  
- Use a **single-color channel** (either red or green)
- High signal but more susceptible to dye bias  
- Better dynamic range for extreme methylation levels (0 or 1)

Structure:
- Two probes hybridize depending on methylation state  
- Single-base extension differentiates signals

---

### 🔹 **Type II Probes**
- Use **one probe** per CpG  
- Differentiates methylation using **two-color channels**
- More compact but slightly lower dynamic range  
- More abundant on the array (>60% of probes)

Structure:
- Single probe binds regardless of methylation  
- Color channel determines methylation state

---

### 🧪 Why Type I and Type II Need Normalization

Because the chemistry and dynamic range differ:

- Type I has **higher sensitivity**  
- Type II has **compressed Beta values**

This creates a **two-cluster distribution**, which can distort downstream analysis.

Normalization methods like **NOOB**, **SWAN**, and **Functional Normalization** help align probe types so their Beta values are comparable.

---

## 🧬 Why Filter Probes?

Some probes can produce misleading methylation values.  
Filtering ensures reliability.

### Filtered probe categories include:

#### 1️⃣ **Probes overlapping SNPs**
- SNPs at the CpG or single-base extension site change binding efficiency  
- Causes false methylation readings

#### 2️⃣ **Cross-reactive probes**
- Bind to multiple genomic locations  
- Produce mixed signals  

#### 3️⃣ **Sex chromosome probes**
- X/Y methylation strongly differs between males and females  
- Remove unless sex is part of study design  

#### 4️⃣ **Probes failing detection p-value threshold**
- Low-quality or noisy intensity measurements  
- Must be removed to avoid artifacts

---

## 🧬 How the Array Measures Methylation (Conceptual)

1. DNA is bisulfite converted:  
   - **Unmethylated cytosines → uracil**  
   - **Methylated cytosines → remain cytosine**

2. Probes hybridize depending on the methylation state.

3. Fluorescent intensities (M and U) are read for each CpG.

4. Beta and M values are calculated.

5. Data are normalized to correct:
   - dye bias  
   - probe type bias  
   - background noise  

6. Final values represent actual methylation percentages.

---

## 🧬 Why Methylation Arrays Are Still Widely Used

Despite sequencing-based methods, 450K/EPIC arrays are popular because:

- Cost-effective  
- Good reproducibility  
- Easy statistical frameworks (limma)  
- Well-annotated probes  
- Large existing datasets (GEO)  

---

## 📌 Summary

The Illumina 450K array provides a robust, high-resolution view of DNA methylation across hundreds of thousands of CpG sites. Understanding probe chemistry, normalization, and probe filtering is essential for reliable downstream analysis. This conceptual file prepares the reader for the code and results in the rest of the project.


