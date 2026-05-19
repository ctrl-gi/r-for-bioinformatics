---
title: "Exercise 5 — Differential Expression Analysis Basics"
---

# Exercise 5 — Differential Expression Analysis Basics

In RNA-seq analysis, one of the most common goals is to identify genes that behave differently between conditions.

Examples:
- healthy vs disease
- treated vs untreated
- responder vs non-responder

This process is called:

# Differential Expression (DE) Analysis

In this exercise, we will:
- combine expression matrices with metadata
- compare Control vs Treatment samples
- calculate fold changes
- identify candidate DE genes

This exercise introduces the core logic behind tools such as:
- DESeq2
- edgeR
- limma

---

# 🧬 Biological Context

Suppose we performed RNA-seq on:
- 4 Control samples
- 4 Treatment samples

We want to identify genes that increase or decrease after treatment.

---

# Part 1 — Create Expression Matrix

## Task 1.1

Create the following gene vector:

```r
genes <- c(
  "TP53","EGFR","MYC","BRCA1",
  "ACTB","GAPDH","VEGFA","CDKN1A",
  "STAT3","BCL2"
)
```

---

## Task 1.2

Create the following count matrix:

```r
counts <- matrix(c(

  120,130,125,128,220,230,240,235,
  300,310,295,305,500,520,510,530,
  90,85,88,92,70,72,68,65,
  450,470,460,455,700,720,710,730,
  1000,980,1020,1010,1050,1070,1080,1060,
  900,920,910,905,930,950,940,945,
  140,150,145,148,320,340,330,335,
  200,210,205,198,410,430,420,425,
  180,190,185,188,350,360,355,370,
  500,490,510,505,300,290,310,305

), nrow = 10, byrow = TRUE)
```

---

## Task 1.3

Assign:
- row names = genes
- column names:

```r
Control_1
Control_2
Control_3
Control_4
Treatment_1
Treatment_2
Treatment_3
Treatment_4
```

---

# Part 2 — Create Metadata

## Task 2.1

Create a metadata data frame containing:

| Sample | Condition |
|---|---|
| Control_1 | Control |
| Control_2 | Control |
| Control_3 | Control |
| Control_4 | Control |
| Treatment_1 | Treatment |
| Treatment_2 | Treatment |
| Treatment_3 | Treatment |
| Treatment_4 | Treatment |

Store as:

```r
metadata
```

---

## Task 2.2

Inspect:
- dimensions
- row names
- column names

---

# Part 3 — Explore Expression Matrix

## Task 3.1

Check:
- dimensions of counts matrix
- number of genes
- number of samples

---

## Task 3.2

Retrieve:
- TP53 expression values
- VEGFA expression values
- STAT3 expression in Treatment_4

---

# Part 4 — Calculate Mean Expression

## Task 4.1

Calculate:
- mean Control expression per gene
- mean Treatment expression per gene

Store as:

```r
control_mean
treatment_mean
```

---

## Task 4.2

Combine results into a data frame:

```r
de_results
```

containing:
- Gene
- ControlMean
- TreatmentMean

---

# Part 5 — Fold Change

## Task 5.1

Calculate fold change:

```r
TreatmentMean / ControlMean
```

Add as a new column:
```r
FoldChange
```

---

## Task 5.2

Interpret:
- FoldChange > 1
- FoldChange < 1

---

## Task 5.3

Find genes with:
- FoldChange > 1.5

These may represent:
- upregulated genes

---

## Task 5.4

Find genes with:
- FoldChange < 0.8

These may represent:
- downregulated genes

---

# Part 6 — Ranking Genes

## Task 6.1

Sort genes:
- highest FoldChange → lowest

---

## Task 6.2

Identify:
- top 3 upregulated genes
- top 3 downregulated genes

---

# Part 7 — Expression Filtering

Genes with very low expression are often removed before DE analysis.

---

## Task 7.1

Calculate:
- mean expression across ALL samples

---

## Task 7.2

Filter out genes where:
- mean expression < 100

Store as:
```r
filtered_de_results
```

---

## Task 7.3

How many genes were removed?

---

# Part 8 — Log2 Fold Change

RNA-seq analysis commonly uses:

# log2 Fold Change

instead of regular fold change.

---

## Task 8.1

Calculate:

```r
log2FC = log2(FoldChange)
```

Add as a new column.

---

## Task 8.2

Interpret:
- positive log2FC
- negative log2FC
- log2FC = 0

---

## Task 8.3

Find genes with:
- log2FC > 0.5

---

# Part 9 — Biological Interpretation

Answer in comments:

```r
# 1. Which genes appear strongly upregulated?
# 2. Which genes appear downregulated?
# 3. Why is fold change useful?
# 4. Why do we use log2 fold change?
# 5. Why is metadata important in RNA-seq analysis?
```

---

# Bonus Challenge

## B1

Create a column:

```r
Regulation
```

Rules:
- "Upregulated" if log2FC > 0.5
- "Downregulated" if log2FC < -0.5
- "Stable" otherwise

---

## B2

Count:
- number of upregulated genes
- number of downregulated genes
- number of stable genes

---

## B3

Find genes that are:
- Upregulated
AND
- mean expression > 300

---

# 🧠 Key Concepts Learned

- metadata-driven analysis
- condition comparison
- fold change
- log2 fold change
- gene ranking
- candidate differential expression

These are the conceptual foundations behind:
- DESeq2
- edgeR
- limma differential expression workflows

---

⬅️ [Previous Exercise](../basics/04_expression_matrix_basics) | 🏠 [Home](../index) | ➡️ [Next Exercise](../basics/06_rnaseq_visualization_basics)
