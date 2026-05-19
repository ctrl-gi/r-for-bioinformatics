---
title: "Exercise 6 — RNA-seq Visualization Basics"
---

# Exercise 6 — RNA-seq Visualization Basics

In RNA-seq analysis, visualization is extremely important.

Before performing advanced analysis, researchers often:
- inspect expression distributions
- compare samples
- identify patterns
- detect outliers
- visualize biological differences

In this exercise, we will create basic RNA-seq visualizations using base R.

These concepts are foundational for:
- exploratory data analysis (EDA)
- quality control (QC)
- differential expression interpretation
- publication figures

---

By the end of this exercise, you should be able to:

- Create barplots
- Create histograms
- Create boxplots
- Create heatmaps
- Visualize gene expression patterns
- Compare Control vs Treatment samples
- Interpret expression distributions

---

# 🧬 Biological Context

Suppose we performed RNA-seq on:
- 4 Control samples
- 4 Treatment samples

We now want to visualize expression patterns across genes and samples.

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

# Part 2 — Basic Matrix Inspection

## Task 2.1

Check:
- dimensions
- row names
- column names

---

## Task 2.2

Calculate:
- mean expression per gene

Store as:

```r
gene_means
```

---

# Part 3 — Barplots

Barplots are useful for comparing:
- genes
- samples
- conditions

---

## Task 3.1

Create a barplot of:
- mean expression per gene

Hint:

```r
barplot(gene_means)
```

---

## Task 3.2

Improve readability by adding:
- gene labels
- main title
- axis labels

Example arguments:

```r
names.arg
main
xlab
ylab
las
```

---

## Task 3.3

Questions:
1. Which genes appear highly expressed?
2. Which genes appear lowly expressed?

---

# Part 4 — Histograms

Histograms help visualize:
- expression distributions

---

## Task 4.1

Create a histogram of:
- ALL expression values in the matrix

Hint:

```r
hist(counts)
```

---

## Task 4.2

Add:
- title
- axis labels

---

## Task 4.3

Interpret:
1. Are most genes lowly or highly expressed?
2. Is the distribution symmetric or skewed?

---

# Part 5 — Log Transformation

RNA-seq data is often log-transformed before visualization.

---

## Task 5.1

Create:

```r
log_counts <- log2(counts + 1)
```

---

## Task 5.2

Create a histogram of:
- log-transformed counts

---

## Task 5.3

Compare:
- original histogram
- log-transformed histogram

Questions:
1. Which distribution looks more balanced?
2. Why is log transformation useful?

---

# Part 6 — Boxplots

Boxplots are commonly used for:
- sample comparison
- QC analysis
- identifying outliers

---

## Task 6.1

Create a boxplot for:
- all samples

Hint:

```r
boxplot(counts)
```

---

## Task 6.2

Add:
- sample names
- title
- axis labels

---

## Task 6.3

Interpret:
1. Which samples appear similar?
2. Are Treatment samples generally higher?
3. Are there potential outliers?

---

# Part 7 — Heatmaps

Heatmaps are one of the most important RNA-seq visualization tools.

They display:
- genes
- samples
- expression intensity

---

## Task 7.1

Create a heatmap using:

```r
heatmap(counts)
```

---

## Task 7.2

Create a heatmap using:
- log-transformed counts

---

## Task 7.3

Interpret:
1. Which genes appear highly expressed?
2. Do Treatment samples cluster together?
3. Why are heatmaps useful?

---

# Part 8 — Gene-Specific Visualization

## Task 8.1

Create a barplot for:
- TP53 expression across samples

Hint:

```r
barplot(counts["TP53", ])
```

---

## Task 8.2

Create a barplot for:
- VEGFA expression across samples

---

## Task 8.3

Interpret:
1. Which gene changes more strongly between conditions?
2. Which gene appears more stable?

---

# Part 9 — Control vs Treatment Comparison

## Task 9.1

Calculate:
- average expression per sample

Hint:

```r
colMeans(counts)
```

---

## Task 9.2

Create a barplot of:
- sample mean expression

---

## Task 9.3

Interpret:
1. Do Treatment samples show higher expression?
2. Are Control samples consistent?

---

# Part 10 — Mini Biological Interpretation

Answer in comments:

```r
# 1. Why are visualizations important in RNA-seq analysis?
# 2. Why do we log-transform RNA-seq data?
# 3. Why are boxplots useful for QC?
# 4. Why are heatmaps widely used in transcriptomics?
# 5. Which visualization did you find most informative?
```

---

# Bonus Challenge

## B1

Create a heatmap for only:
- highly expressed genes

Define highly expressed as:
- mean expression > 400

---

## B2

Create a boxplot using:
- log-transformed counts

Compare with:
- raw counts

---

## B3

Sort genes by mean expression before plotting.

---

# 🧠 Key Concepts Learned

- exploratory data analysis
- RNA-seq visualization
- distributions
- log transformation
- QC thinking
- heatmaps
- sample comparison

These concepts are essential for:
- RNA-seq QC
- transcriptomic interpretation
- differential expression workflows
- publication-quality analysis

---

# 🔁 Navigation

⬅️ [Previous: Exercise 5](../rnaseq/05_differential_expression_basics)

🏠 [Back to Main Menu](../index)

➡️ Next: Coming soon
