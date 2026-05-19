---
title: "Exercise 5 — Solutions"
---

# Exercise 5 — Solutions: Differential Expression Analysis Basics

---

# Part 1 — Create Expression Matrix

## Task 1.1

```r
genes <- c(
  "TP53","EGFR","MYC","BRCA1",
  "ACTB","GAPDH","VEGFA","CDKN1A",
  "STAT3","BCL2"
)
```

---

## Task 1.2

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

```r
rownames(counts) <- genes

colnames(counts) <- c(
  "Control_1",
  "Control_2",
  "Control_3",
  "Control_4",
  "Treatment_1",
  "Treatment_2",
  "Treatment_3",
  "Treatment_4"
)
```

---

# Part 2 — Create Metadata

## Task 2.1

```r
metadata <- data.frame(
  Sample = colnames(counts),
  Condition = c(
    "Control","Control","Control","Control",
    "Treatment","Treatment","Treatment","Treatment"
  )
)

metadata
```

---

## Task 2.2

```r
dim(metadata)

rownames(metadata)

colnames(metadata)
```

---

# Part 3 — Explore Expression Matrix

## Task 3.1

```r
dim(counts)

nrow(counts)

ncol(counts)
```

### Answers:
- 10 genes
- 8 samples

---

## Task 3.2

```r
counts["TP53", ]

counts["VEGFA", ]

counts["STAT3", "Treatment_4"]
```

---

# Part 4 — Calculate Mean Expression

## Task 4.1

```r
control_mean <- rowMeans(
  counts[, c(
    "Control_1",
    "Control_2",
    "Control_3",
    "Control_4"
  )]
)

treatment_mean <- rowMeans(
  counts[, c(
    "Treatment_1",
    "Treatment_2",
    "Treatment_3",
    "Treatment_4"
  )]
)
```

---

## Task 4.2

```r
de_results <- data.frame(
  Gene = genes,
  ControlMean = control_mean,
  TreatmentMean = treatment_mean
)

de_results
```

---

# Part 5 — Fold Change

## Task 5.1

```r
de_results$FoldChange <-
  de_results$TreatmentMean /
  de_results$ControlMean

de_results
```

---

## Task 5.2 — Interpretation

```r
# FoldChange > 1:
# Higher expression in Treatment

# FoldChange < 1:
# Lower expression in Treatment
```

---

## Task 5.3 — Upregulated Genes

```r
de_results[de_results$FoldChange > 1.5, ]
```

---

## Task 5.4 — Downregulated Genes

```r
de_results[de_results$FoldChange < 0.8, ]
```

---

# Part 6 — Ranking Genes

## Task 6.1

```r
de_results_sorted <-
  de_results[order(
    de_results$FoldChange,
    decreasing = TRUE
  ), ]

de_results_sorted
```

---

## Task 6.2

### Top 3 Upregulated

```r
head(de_results_sorted, 3)
```

---

### Top 3 Downregulated

```r
tail(de_results_sorted, 3)
```

---

# Part 7 — Expression Filtering

## Task 7.1

```r
de_results$MeanExpression <-
  rowMeans(counts)

de_results
```

---

## Task 7.2

```r
filtered_de_results <-
  de_results[de_results$MeanExpression >= 100, ]

filtered_de_results
```

---

## Task 7.3

```r
nrow(de_results) -
  nrow(filtered_de_results)
```

### Answer:
- 1 gene removed (MYC)

---

# Part 8 — Log2 Fold Change

## Task 8.1

```r
de_results$log2FC <-
  log2(de_results$FoldChange)

de_results
```

---

## Task 8.2 — Interpretation

```r
# positive log2FC:
# higher in Treatment

# negative log2FC:
# lower in Treatment

# log2FC = 0:
# no change between conditions
```

---

## Task 8.3

```r
de_results[de_results$log2FC > 0.5, ]
```

---

# Part 9 — Biological Interpretation

```r
# 1. EGFR, BRCA1, VEGFA and STAT3 appear strongly upregulated

# 2. BCL2 appears downregulated

# 3. Fold change quantifies biological differences between conditions

# 4. log2FC creates symmetric interpretation and compresses large values

# 5. Metadata links samples to biological conditions
```

---

# Bonus Challenge

## B1 — Regulation Column

```r
de_results$Regulation <- ifelse(
  de_results$log2FC > 0.5,
  "Upregulated",
  ifelse(
    de_results$log2FC < -0.5,
    "Downregulated",
    "Stable"
  )
)

de_results
```

---

## B2 — Count Categories

```r
table(de_results$Regulation)
```

---

## B3 — Upregulated + Mean Expression > 300

```r
de_results[
  de_results$Regulation == "Upregulated" &
  de_results$MeanExpression > 300,
]
```

---

# 🧠 Key Takeaways

- differential expression compares conditions
- metadata defines experimental groups
- fold change measures biological effect size
- log2FC standardizes interpretation
- filtering improves downstream analysis

These concepts form the basis of:
- DESeq2
- edgeR
- limma
- transcriptomic differential expression workflows
