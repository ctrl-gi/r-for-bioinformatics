---
title: "Exercise 6 — Solutions"
---

# Exercise 6 — Solutions: RNA-seq Visualization Basics

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
  "Control_1","Control_2","Control_3","Control_4",
  "Treatment_1","Treatment_2","Treatment_3","Treatment_4"
)
```

---

# Part 2 — Basic Matrix Inspection

## Task 2.1

```r
dim(counts)
rownames(counts)
colnames(counts)
```

---

## Task 2.2

```r
gene_means <- rowMeans(counts)
gene_means
```

---

# Part 3 — Barplots

## Task 3.1

```r
barplot(gene_means)
```

---

## Task 3.2 (Improved)

```r
barplot(
  gene_means,
  names.arg = genes,
  main = "Mean Expression per Gene",
  xlab = "Genes",
  ylab = "Mean Expression",
  las = 2
)
```

---

## Task 3.3

### Interpretation:
- ACTB, GAPDH, BRCA1 are highly expressed
- MYC and CDKN1A are relatively low

---

# Part 4 — Histograms

## Task 4.1

```r
hist(counts)
```

---

## Task 4.2

```r
hist(
  counts,
  main = "Distribution of RNA-seq Counts",
  xlab = "Expression Value",
  ylab = "Frequency"
)
```

---

## Task 4.3

### Interpretation:
- distribution is right-skewed
- most values are low to moderate
- few genes have very high expression

---

# Part 5 — Log Transformation

## Task 5.1

```r
log_counts <- log2(counts + 1)
```

---

## Task 5.2

```r
hist(
  log_counts,
  main = "Log2-transformed Expression",
  xlab = "log2(count + 1)"
)
```

---

## Task 5.3

### Interpretation:
- log transform reduces skewness
- distribution becomes more symmetric
- easier to compare samples

---

# Part 6 — Boxplots

## Task 6.1

```r
boxplot(counts)
```

---

## Task 6.2

```r
boxplot(
  counts,
  main = "Sample-wise Expression Distribution",
  xlab = "Samples",
  ylab = "Expression",
  las = 2
)
```

---

## Task 6.3

### Interpretation:
- samples are broadly similar
- Treatment samples slightly higher
- no extreme outliers observed

---

# Part 7 — Heatmaps

## Task 7.1

```r
heatmap(counts)
```

---

## Task 7.2

```r
heatmap(log_counts)
```

---

## Task 7.3

### Interpretation:
- Treatment samples cluster together
- highly expressed genes form visible blocks
- log transformation improves pattern visibility

---

# Part 8 — Gene-Specific Visualization

## Task 8.1

```r
barplot(counts["TP53", ],
        main = "TP53 Expression Across Samples",
        xlab = "Samples",
        ylab = "Expression",
        las = 2)
```

---

## Task 8.2

```r
barplot(counts["VEGFA", ],
        main = "VEGFA Expression Across Samples",
        xlab = "Samples",
        ylab = "Expression",
        las = 2)
```

---

## Task 8.3

### Interpretation:
- VEGFA shows stronger Treatment increase
- TP53 is more stable across conditions

---

# Part 9 — Sample Comparison

## Task 9.1

```r
sample_means <- colMeans(counts)
sample_means
```

---

## Task 9.2

```r
barplot(
  sample_means,
  main = "Mean Expression per Sample",
  xlab = "Samples",
  ylab = "Mean Expression",
  las = 2
)
```

---

## Task 9.3

### Interpretation:
- Treatment samples are generally higher
- Control samples are consistent

---

# Part 10 — Interpretation

```r
# 1. Visualizations help identify patterns quickly
# 2. Log transformation reduces skew and improves comparability
# 3. Boxplots reveal variability and outliers
# 4. Heatmaps show gene-sample structure clearly
# 5. Heatmaps were most informative for global patterns
```

---

# Bonus

## B1 — Filtered Heatmap

```r
filtered <- counts[rowMeans(counts) > 400, ]

heatmap(filtered)
```

---

## B2 — Log Boxplot

```r
boxplot(log_counts,
        main = "Log-transformed Boxplot",
        las = 2)
```

---

## B3 — Sorted Plot

```r
sorted <- counts[order(rowMeans(counts), decreasing = TRUE), ]

barplot(rowMeans(sorted),
        names.arg = rownames(sorted),
        las = 2)
```

---

# 🧠 Key Takeaways

- RNA-seq data is highly skewed
- visualization is essential for QC
- log transformation improves interpretability
- heatmaps reveal structure across genes and samples
- boxplots help compare sample distributions
