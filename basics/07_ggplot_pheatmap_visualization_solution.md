---
title: "Exercise 7 — Solutions"
---

# Exercise 7 — Advanced RNA-seq Visualization (Solutions)

---

# Part 0 — Setup

```r
library(ggplot2)
library(pheatmap)
library(gridExtra)
```

---

# Part 1 — Long Format Conversion

## Task 1.2

```r
df <- data.frame(
  Gene = rep(rownames(counts), times = ncol(counts)),
  Sample = rep(colnames(counts), each = nrow(counts)),
  Expression = as.vector(counts)
)
```

---

## Task 1.3

```r
df$Condition <- ifelse(grepl("C", df$Sample),
                       "Control",
                       "Treatment")
```

---

# Part 2 — ggplot2 Boxplot

## Task 2.1

```r
ggplot(df, aes(x = Gene, y = Expression)) +
  geom_boxplot()
```

---

## Task 2.2 (Improved)

```r
ggplot(df, aes(x = Gene, y = Expression, fill = Condition)) +
  geom_boxplot() +
  theme(axis.text.x = element_text(angle = 90)) +
  ggtitle("Gene Expression by Condition")
```

---

## Task 2.3

```r
ggplot(df, aes(x = Sample, y = Expression, fill = Condition)) +
  geom_boxplot() +
  theme(axis.text.x = element_text(angle = 90)) +
  ggtitle("Expression Across Samples")
```

---

## Task 2.4 — Interpretation

```r
# Treatment samples generally show higher expression
# distributions vary slightly across samples
```

---

# Part 3 — Barplots in ggplot2

## Task 3.1

```r
gene_means <- rowMeans(counts)

plot_df <- data.frame(
  Gene = names(gene_means),
  MeanExpression = gene_means
)
```

---

## Task 3.2

```r
ggplot(plot_df, aes(x = Gene, y = MeanExpression)) +
  geom_bar(stat = "identity")
```

---

## Task 3.3 (Improved)

```r
ggplot(plot_df, aes(x = Gene, y = MeanExpression, fill = Gene)) +
  geom_bar(stat = "identity") +
  theme(axis.text.x = element_text(angle = 90)) +
  ggtitle("Mean Gene Expression")
```

---

# Part 4 — pheatmap

## Task 4.1

```r
pheatmap(counts)
```

---

## Task 4.2

```r
pheatmap(scale(counts))
```

---

## Task 4.3 — Interpretation

```r
# scaled heatmap shows relative expression patterns
# genes cluster based on similarity
# samples show partial separation of Control vs Treatment
```

---

# Part 5 — Combining Plots

## Task 5.1

```r
p1 <- ggplot(plot_df, aes(x = Gene, y = MeanExpression)) +
  geom_bar(stat = "identity") +
  theme(axis.text.x = element_text(angle = 90)) +
  ggtitle("Mean Expression per Gene")
```

```r
p2 <- ggplot(df, aes(x = Gene, y = Expression)) +
  geom_boxplot() +
  theme(axis.text.x = element_text(angle = 90)) +
  ggtitle("Gene-wise Distribution")
```

---

## Task 5.2

```r
grid.arrange(p1, p2, ncol = 2)
```

---

## Task 5.3 — Interpretation

```r
# p1 shows average gene-level signal
# p2 shows distribution across samples
# combining plots gives global + local view
```

---

# Part 6 — Multi-panel Figure Thinking

## Task 6.1–6.2

```r
p3 <- ggplot(df, aes(x = Sample, y = Expression, fill = Condition)) +
  geom_boxplot() +
  theme(axis.text.x = element_text(angle = 90)) +
  ggtitle("Sample Distribution")

grid.arrange(p1, p2, p3, ncol = 3)
```

---

## Task 6.3 — Interpretation

```r
# this resembles a multi-panel figure in papers
# each panel shows a different biological view
```

---

# Part 7 — Biological Interpretation

```r
# 1. VEGFA, BRCA1, ACTB show strong variability
# 2. Treatment samples trend higher overall
# 3. scaling removes magnitude bias and reveals patterns
# 4. ggplot2 allows structured, layered visualization
# 5. RNA-seq data is inherently high-dimensional
```

---

# Bonus

## B1 — Heatmap-style ggplot

```r
ggplot(df, aes(x = Sample, y = Gene, fill = Expression)) +
  geom_tile()
```

---

## B2 — Ordered genes

```r
plot_df$Gene <- factor(plot_df$Gene,
                       levels = plot_df$Gene[order(plot_df$MeanExpression)])

ggplot(plot_df, aes(x = Gene, y = MeanExpression)) +
  geom_bar(stat = "identity") +
  theme(axis.text.x = element_text(angle = 90))
```

---

## B3 — Publication-style plot

```r
ggplot(plot_df, aes(x = Gene, y = MeanExpression, fill = MeanExpression)) +
  geom_bar(stat = "identity") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 90)) +
  ggtitle("Publication-style Gene Expression Plot")
```

---

# 🧠 Key Takeaways

- ggplot2 = structured grammar of graphics
- pheatmap = clustering-based visualization
- heatmaps reveal expression structure
- combining plots gives multi-scale interpretation
- visualization is critical for RNA-seq interpretation
