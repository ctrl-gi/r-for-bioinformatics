---
title: "Exercise 7 — Advanced RNA-seq Visualization with ggplot2 & pheatmap"
---

# Exercise 7 — Advanced RNA-seq Visualization

In real RNA-seq analysis, base R plots are rarely used for final figures.

Instead, we use:
- ggplot2 (for publication-quality plots)
- pheatmap (for heatmaps with clustering)
- patchwork / gridExtra (to combine plots)

This exercise will teach you how to create:
- modern RNA-seq visualizations
- structured multi-panel figures
- publication-style plots

---

# 🎯 Learning Objectives

By the end of this exercise, you should be able to:

- Use ggplot2 for gene expression plots
- Create boxplots and barplots using ggplot2
- Use pheatmap for clustered heatmaps
- Combine multiple plots into one figure
- Compare visualization styles (base R vs ggplot2)
- Interpret multi-panel RNA-seq figures

---

# 📦 Setup

## Task 0.1 — Load libraries

```r
library(ggplot2)
library(pheatmap)
library(gridExtra)
```

---

# 🧬 Data Setup

We will reuse a simplified RNA-seq dataset.

## Task 1.1 — Expression matrix

```r
genes <- c("TP53","EGFR","MYC","BRCA1","ACTB","GAPDH","VEGFA","CDKN1A")

counts <- matrix(c(
  120,130,125,200,210,220,
  300,290,310,450,470,490,
  80,75,90,150,160,170,
  500,520,510,800,820,850,
  1000,980,1020,1100,1120,1150,
  900,920,910,950,970,960,
  150,160,155,300,320,310,
  200,190,210,400,420,410
), nrow = 8, byrow = TRUE)

rownames(counts) <- genes
colnames(counts) <- c("C1","C2","C3","T1","T2","T3")
```

---

# Part 1 — Converting to Long Format (IMPORTANT)

ggplot2 works best with long-format data.

## Task 1.2

Convert matrix → data frame:

```r
df <- data.frame(
  Gene = rep(rownames(counts), times = ncol(counts)),
  Sample = rep(colnames(counts), each = nrow(counts)),
  Expression = as.vector(counts)
)
```

---

## Task 1.3

Add condition column:

```r
df$Condition <- ifelse(grepl("C", df$Sample),
                       "Control",
                       "Treatment")
```

---

# Part 2 — ggplot2 Visualizations

---

## Task 2.1 — Gene expression boxplot

```r
ggplot(df, aes(x = Gene, y = Expression)) +
  geom_boxplot()
```

---

## Task 2.2 — Improve aesthetics

Add:
- fill by condition
- axis rotation
- title

---

## Task 2.3 — Sample-level comparison

Create boxplot:
- x = Sample
- y = Expression
- fill = Condition

---

## Task 2.4 — Interpretation

Answer:
- which group shows higher expression?
- are distributions consistent across samples?

---

# Part 3 — Barplots in ggplot2

---

## Task 3.1 — Mean expression per gene

First compute:

```r
gene_means <- rowMeans(counts)
```

Convert to data frame:

```r
plot_df <- data.frame(
  Gene = names(gene_means),
  MeanExpression = gene_means
)
```

---

## Task 3.2 — Barplot

```r
ggplot(plot_df, aes(x = Gene, y = MeanExpression)) +
  geom_bar(stat = "identity")
```

---

## Task 3.3 — Improve visualization

Add:
- color fill
- rotated labels
- title

---

# Part 4 — pheatmap Visualization

---

## Task 4.1 — Basic heatmap

```r
pheatmap(counts)
```

---

## Task 4.2 — Scaled heatmap (IMPORTANT)

```r
pheatmap(scale(counts))
```

---

## Task 4.3 — Interpretation

Answer:
- which genes cluster together?
- do Control and Treatment separate?

---

# Part 5 — Combining Plots (VERY IMPORTANT)

---

## Task 5.1 — Create ggplot objects

```r
p1 <- ggplot(plot_df, aes(x = Gene, y = MeanExpression)) +
  geom_bar(stat = "identity") +
  theme(axis.text.x = element_text(angle = 90))
```

```r
p2 <- ggplot(df, aes(x = Gene, y = Expression)) +
  geom_boxplot()
```

---

## Task 5.2 — Combine plots

Using grid.arrange:

```r
grid.arrange(p1, p2, ncol = 2)
```

---

## Task 5.3 — Interpretation

Answer:
- what does each plot tell you?
- why is combining plots useful?

---

# Part 6 — Multi-panel Figure Thinking

---

## Task 6.1

Create:
- one plot showing gene means
- one plot showing sample distributions
- one heatmap

---

## Task 6.2

Combine them into one figure

---

## Task 6.3

Reflect:
- how does this resemble a paper figure?

---

# Part 7 — Biological Interpretation

```r
# 1. Which genes are most variable?
# 2. Do Control and Treatment separate visually?
# 3. Why is scaling important in heatmaps?
# 4. Why do we use ggplot2 instead of base R?
# 5. What does this tell you about RNA-seq structure?
```

---

# Bonus Challenge

## B1

Create a ggplot heatmap-style visualization using geom_tile()

---

## B2

Order genes by mean expression before plotting

---

## B3

Make a publication-ready figure:
- title
- clean theme
- rotated labels
- consistent colors

---

# 🧠 Key Concepts Learned

- ggplot2 grammar of graphics
- long-format transformation
- pheatmap clustering
- scaled expression visualization
- multi-panel figure construction
- publication-style visualization

---

⬅️ [Previous Exercise](../basics/06_rnaseq_visualization_basics) | 🏠 [Home](../index) | ➡️ Coming Soon
