---
title: "Exercise 4 — RNA-seq Expression Matrix Basics"
---

# Exercise 4 — RNA-seq Expression Matrix Basics

Welcome to your first **RNA-seq style dataset**.

So far, we have worked with:
- vectors
- simple data frames
- one expression value per row

However, real RNA-seq datasets usually look very different.

Instead of:
- one gene at a time

we usually work with:
- thousands of genes
- multiple samples
- expression matrices

In this exercise, we will build and explore a small RNA-seq expression matrix similar to the type used in:
- DESeq2
- edgeR
- limma
- bulk RNA-seq workflows

---

# 🧬 Biological Context

Suppose we performed bulk RNA-seq on:
- 3 Control samples
- 3 Treatment samples

Expression values below represent simplified normalized counts for several genes.

---

# Part 1 — Creating an Expression Matrix

## Task 1.1

Create the following vector of genes:

```r
genes <- c("TP53","EGFR","MYC","BRCA1",
           "ACTB","GAPDH","VEGFA","CDKN1A")
```

---

## Task 1.2

Create the following matrix of expression values:

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

Store this matrix as `counts`.

---

## Task 1.3

Assign:
- row names = genes
- column names:

```r
Control_1
Control_2
Control_3
Treatment_1
Treatment_2
Treatment_3
```

---

## Task 1.4

Print the matrix.

---

# Part 2 — Understanding Matrix Structure

## Task 2.1

Use:
- `dim()`
- `nrow()`
- `ncol()`
- `rownames()`
- `colnames()`

Questions:
1. How many genes are present?
2. How many samples are present?
3. What do rows represent?
4. What do columns represent?

---

## Task 2.2

Retrieve:
- expression values for TP53
- expression values for BRCA1
- expression value of MYC in Treatment_2

Hints:

```r
counts["TP53", ]

counts["MYC", "Treatment_2"]
```

---

# Part 3 — Per-Gene Summaries

In RNA-seq analysis, we often summarize genes across samples.

---

## Task 3.1

Calculate:
- mean expression per gene

Hint:

```r
rowMeans(counts)
```

Store as:
```r
gene_means
```

---

## Task 3.2

Calculate:
- maximum expression per gene
- minimum expression per gene

Hints:

```r
apply(counts, 1, max)

apply(counts, 1, min)
```

---

## Task 3.3

Identify:
- highest expressed gene overall
- lowest expressed gene overall

---

# Part 4 — Sample-Level Summaries

Now analyze samples instead of genes.

---

## Task 4.1

Calculate:
- mean expression per sample

Hint:

```r
colMeans(counts)
```

---

## Task 4.2

Which sample has:
- highest overall expression?
- lowest overall expression?

---

## Task 4.3

Compare:
- average Control expression
- average Treatment expression

Hints:
- select columns by name
- use `rowMeans()` or `mean()`

---

# Part 5 — Filtering Low-Expression Genes

Filtering low-expression genes is one of the first steps in RNA-seq analysis.

Suppose genes with mean expression < 150 are considered lowly expressed.

---

## Task 5.1

Find genes with:
- mean expression < 150

---

## Task 5.2

Create a filtered matrix containing only genes with:
- mean expression ≥ 150

Store as:

```r
filtered_counts
```

---

## Task 5.3

How many genes were removed?

---

# Part 6 — Fold Change Thinking

One key RNA-seq concept is comparing:
- Treatment vs Control

---

## Task 6.1

Calculate:
- mean Control expression per gene
- mean Treatment expression per gene

Store as:
```r
control_mean
treatment_mean
```

---

## Task 6.2

Calculate fold change:

```r
treatment_mean / control_mean
```

Store as:
```r
fold_change
```

---

## Task 6.3

Identify:
- genes with fold change > 1.5

---

## Task 6.4

Biological interpretation:
- what does high fold change indicate?

---

# Part 7 — Log Transformation

RNA-seq data is often log-transformed.

---

## Task 7.1

Create:
```r
log_counts <- log2(counts + 1)
```

Questions:
1. Why do we add `+1`?
2. Why is log transformation useful?

---

## Task 7.2

Compare:
- original values
- log-transformed values

for:
- TP53
- BRCA1

---

# Part 8 — Matrix Exploration

## Task 8.1

Find:
- highest value in the matrix
- lowest value in the matrix

Hints:

```r
max(counts)

min(counts)
```

---

## Task 8.2

Find:
- gene corresponding to highest expression value

---

# Part 9 — Mini Biological Interpretation

Answer in comments:

```r
# 1. Which genes appear highly expressed?
# 2. Do Treatment samples show globally higher expression?
# 3. Why do we filter low-expression genes?
# 4. Why are matrices more useful than simple vectors?
# 5. How does this resemble real RNA-seq data?
```

---

# Bonus Challenge

## B1

Create a metadata data frame:

| Sample | Condition |
|---|---|
| Control_1 | Control |
| Control_2 | Control |
| Control_3 | Control |
| Treatment_1 | Treatment |
| Treatment_2 | Treatment |
| Treatment_3 | Treatment |

Store as:
```r
metadata
```

---

## B2

Find genes with:
- fold change > 1.5
AND
- mean expression > 200

---

## B3

Sort genes by fold change from highest to lowest.

---

# 🧠 Key Concepts Learned

- RNA-seq expression matrices
- genes × samples structure
- row-wise vs column-wise operations
- filtering genes
- fold change
- log transformation
- metadata thinking

These concepts are foundational for:
- DESeq2
- edgeR
- limma
- bulk RNA-seq analysis
- scRNA-seq expression matrices

---

# 🔁 Navigation

⬅️ [Previous: Exercise 3](../basics/03_mini_expression_analysis)

🏠 [Back to Main Menu](../index)

➡️ Next: Coming soon
