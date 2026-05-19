---
title: "Exercise 4 — Solutions"
---

# Exercise 4 — Solutions: RNA-seq Expression Matrix Basics

---

# Part 1 — Creating an Expression Matrix

## Task 1.1

```r
genes <- c("TP53","EGFR","MYC","BRCA1",
           "ACTB","GAPDH","VEGFA","CDKN1A")
```

---

## Task 1.2

```r
counts <- matrix(c(
  120, 130, 125, 200, 210, 220,
  300, 290, 310, 450, 470, 490,
  80,  75,  90,  150, 160, 170,
  500, 520, 510, 800, 820, 850,
  1000,980,1020,1100,1120,1150,
  900,920,910,950,970,960,
  150,160,155,300,320,310,
  200,190,210,400,420,410
), nrow = 8, byrow = TRUE)
```

---

## Task 1.3

```r
rownames(counts) <- genes

colnames(counts) <- c(
  "Control_1",
  "Control_2",
  "Control_3",
  "Treatment_1",
  "Treatment_2",
  "Treatment_3"
)
```

---

## Task 1.4

```r
counts
```

---

# Part 2 — Understanding Matrix Structure

## Task 2.1

```r
dim(counts)

nrow(counts)

ncol(counts)

rownames(counts)

colnames(counts)
```

### Answers:
- 8 genes
- 6 samples
- rows = genes
- columns = samples

---

## Task 2.2

```r
counts["TP53", ]

counts["BRCA1", ]

counts["MYC", "Treatment_2"]
```

---

# Part 3 — Per-Gene Summaries

## Task 3.1

```r
gene_means <- rowMeans(counts)

gene_means
```

---

## Task 3.2

```r
gene_max <- apply(counts, 1, max)

gene_min <- apply(counts, 1, min)

gene_max

gene_min
```

---

## Task 3.3

```r
highest_gene <- names(which.max(gene_means))

lowest_gene <- names(which.min(gene_means))

highest_gene

lowest_gene
```

### Answers:
- Highest = ACTB
- Lowest = MYC

---

# Part 4 — Sample-Level Summaries

## Task 4.1

```r
sample_means <- colMeans(counts)

sample_means
```

---

## Task 4.2

```r
names(which.max(sample_means))

names(which.min(sample_means))
```

---

## Task 4.3

```r
control_mean <- mean(counts[, c("Control_1",
                                "Control_2",
                                "Control_3")])

treatment_mean <- mean(counts[, c("Treatment_1",
                                  "Treatment_2",
                                  "Treatment_3")])

control_mean

treatment_mean
```

### Interpretation:
- Treatment samples show higher overall expression

---

# Part 5 — Filtering Low-Expression Genes

## Task 5.1

```r
gene_means[gene_means < 150]
```

---

## Task 5.2

```r
filtered_counts <- counts[gene_means >= 150, ]

filtered_counts
```

---

## Task 5.3

```r
nrow(counts) - nrow(filtered_counts)
```

### Answer:
- 2 genes removed

---

# Part 6 — Fold Change Thinking

## Task 6.1

```r
control_mean <- rowMeans(
  counts[, c("Control_1",
             "Control_2",
             "Control_3")]
)

treatment_mean <- rowMeans(
  counts[, c("Treatment_1",
             "Treatment_2",
             "Treatment_3")]
)
```

---

## Task 6.2

```r
fold_change <- treatment_mean / control_mean

fold_change
```

---

## Task 6.3

```r
fold_change[fold_change > 1.5]
```

---

## Task 6.4

### Interpretation:
- High fold change indicates genes that may be upregulated in Treatment samples

---

# Part 7 — Log Transformation

## Task 7.1

```r
log_counts <- log2(counts + 1)

log_counts
```

### Answers:
- +1 avoids log(0)
- log transformation reduces skew and compresses large values

---

## Task 7.2

```r
counts["TP53", ]

log_counts["TP53", ]
```

```r
counts["BRCA1", ]

log_counts["BRCA1", ]
```

---

# Part 8 — Matrix Exploration

## Task 8.1

```r
max(counts)

min(counts)
```

### Answers:
- max = 1150
- min = 75

---

## Task 8.2

```r
which(counts == max(counts), arr.ind = TRUE)
```

```r
rownames(counts)[5]
```

### Answer:
- ACTB contains the highest expression value

---

# Part 9 — Biological Interpretation

```r
# 1. ACTB, GAPDH and BRCA1 appear highly expressed

# 2. Yes, Treatment samples show globally higher expression

# 3. Low-expression genes are often noisy and less reliable

# 4. Matrices efficiently store thousands of genes across samples

# 5. Real RNA-seq datasets contain many more genes and samples
```

---

# Bonus Challenge

## B1 — Metadata

```r
metadata <- data.frame(
  Sample = colnames(counts),
  Condition = c("Control","Control","Control",
                "Treatment","Treatment","Treatment")
)

metadata
```

---

## B2 — Fold change >1.5 and mean expression >200

```r
gene_means <- rowMeans(counts)

selected <- fold_change > 1.5 & gene_means > 200

fold_change[selected]
```

---

## B3 — Sort genes by fold change

```r
sort(fold_change, decreasing = TRUE)
```

---

# 🧠 Key Takeaways

- RNA-seq data is stored as matrices
- rows = genes
- columns = samples
- row-wise operations summarize genes
- column-wise operations summarize samples
- filtering and fold change are core RNA-seq concepts
