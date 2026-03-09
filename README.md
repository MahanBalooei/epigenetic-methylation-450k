# 🧬 Epigenetic Analysis: DNA Methylation Patterns (Illumina 450K)

> Identifying differentially methylated CpG sites between healthy and diseased individuals using Illumina HumanMethylation450k array data.

**Course:** DNA/RNA Dynamics  
**Platform:** Illumina HumanMethylation450k Array  
**Language:** R (Bioconductor)  

---

## 📋 Project Overview

This project performs a full differential DNA methylation analysis pipeline, from raw IDAT files through quality control, normalization, statistical testing, and visualization. The goal is to detect CpG sites with significant methylation differences between healthy and diseased sample groups.

### Analysis Pipeline

```
Raw IDAT Files
     ↓
Sample & Probe Quality Control
     ↓
Detection p-value Filtering (threshold: 0.05)
     ↓
Quantile Normalization (preprocessQuantile)
     ↓
Statistical Testing (t-tests per CpG)
     ↓
Correction for Multiple Testing
     ↓
Visualization & Reporting
```

---

## 📁 Repository Structure

```
epigenetic-methylation-450k/
├── analysis.R        # Complete methylation analysis pipeline
├── .gitignore        # Files to ignore (data, outputs)
└── README.md         # This file
```

> **Note:** Raw IDAT files and sample sheets are not included due to file size. Place them in the working directory before running the script.

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/MahanBalooei/epigenetic-methylation-450k.git
cd epigenetic-methylation-450k
```

### 2. Install R dependencies

```r
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install(c(
  "minfi",
  "IlluminaHumanMethylation450kmanifest",
  "IlluminaHumanMethylation450kanno.ilmn12.hg19"
))

install.packages(c("gplots", "qqman"))
```

### 3. Prepare your data

Place your raw IDAT files (or methylation beta matrix) and sample sheet into the working directory. Update file paths and sample group labels in `analysis.R` as needed.

### 4. Run the analysis

Open `analysis.R` in RStudio and run the script, or from the terminal:

```bash
Rscript analysis.R
```

---

## 📦 Tools & Packages

| Package | Purpose |
|---|---|
| `minfi` | Reading IDAT files, QC, normalization |
| `IlluminaHumanMethylation450kmanifest` | Array annotation |
| `gplots` | Heatmap visualization |
| `qqman` | Manhattan and QQ plots |

---

## 📊 Visualizations Generated

The pipeline produces the following plots:

- **Density plots** — Beta and M value distributions (raw vs. normalized)
- **6-panel QC plot** — Overall sample quality assessment
- **PCA plots** — Colored by group, sex, and Sentrix ID
- **Boxplots** — p-value distributions (raw, uncorrected, corrected)
- **Volcano plot** — Significant CpG sites by effect size and significance
- **Manhattan plot** — Genome-wide view of differential methylation
- **Heatmap** — Hierarchical clustering of top differentially methylated probes

---

## 🔬 Key Analysis Steps

**Quality Control**
- Per-sample and per-probe QC using `minfi`
- Detection p-value filtering at threshold 0.05 to remove unreliable probes

**Normalization**
- Quantile normalization via `preprocessQuantile` to reduce technical variation between arrays

**Statistical Testing**
- Pairwise t-tests for each CpG site between healthy and diseased groups
- Multiple testing correction applied to control false discovery rate

---

## 👥 Contributors

| Name | GitHub |
|---|---|
| [Elif Güler](https://github.com/elif-guler) | @elif-guler |
| [Eyip Sinay Dalmaz](https://github.com/Dalmaz-ES) | @Dalmaz-ES |
| [Simay Erol](https://github.com/Simay9) | @Simay9 |
| [Barkin Kemec](https://github.com/mbkemec) | @mbkemec |
| [Negin Nilforoosh](https://github.com/neginnilforosh) | @neginnilforosh |
| [Kimia Kanouni](https://github.com/kanounik) | @kanounik |
| [Mahan Balooei](https://github.com/MahanBalooei) | @MahanBalooei |

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
