---
title: "Exercise 3 - GEX"
---

# Exercise 3 — Mini Gene Expression Analysis (Vectors + Data Frames)

In real RNA-seq analysis, we rarely work with a single gene or a simple vector.

Instead, we combine:
- multiple genes
- multiple samples
- expression matrices
- sample metadata

This exercise combines everything from Exercises 1 and 2 into a small biological dataset.

---

# Part 1 — Creating a Multi-Gene Dataset

We now extend from a single gene to **multiple genes across samples**.

## Task 1.1

Create the following vectors:

```r
gene <- c("TP53","EGFR","MYC","BRCA1","ACTB","GAPDH","VEGFA","CDKN1A")

sample_id <- c("S1","S2","S3","S4","S5","S6","S7","S8")

expression <- c(12.4, 15.1, 8.7, 20.3, 17.8, 5.2, 13.5, 18.1)

condition <- c("Control","Control","Control","Treatment",
               "Treatment","Treatment","Control","Treatment")
```

---

## Task 1.2

Combine into a data frame called `df`.

---

# Part 2 — Inspecting Structure

## Task 2.1

Run:

- `str(df)`
- `head(df)`
- `summary(df)`

Questions:
1. What type is each column?
2. How many observations are there?

---

# Part 3 — Gene-Level Filtering

## Task 3.1

Find all rows where:
- expression > 15

---

## Task 3.2

Which genes correspond to expression > 15?

---

## Task 3.3

Find genes where:
- expression < 10

---

## Task 3.4

How many genes fall into:
- high expression (>15)
- low expression (<10)

---

# Part 4 — Condition-Based Analysis

## Task 4.1

Split data into:
- Control group
- Treatment group

---

## Task 4.2

Calculate:
- mean expression (Control)
- mean expression (Treatment)

---

## Task 4.3

Which condition has higher overall expression?

---

# Part 5 — Combined Logic (VERY IMPORTANT)

This is where RNA-seq thinking starts.

## Task 5.1

Find genes where:
- condition = "Treatment"
AND
- expression > 15

---

## Task 5.2

Find genes where:
- condition = "Control"
AND
- expression < 10

---

## Task 5.3

Interpret:
- What do these groups represent biologically?

---

# Part 6 — Adding Biological Meaning

## Task 6.1

Create a new column:

```r
expression_category
```

Rules:
- "High" if expression > 15
- "Medium" if 10–15
- "Low" if < 10

---

## Task 6.2

Count how many genes fall into each category.

---

# Part 7 — Gene Expression Ranking

## Task 7.1

Sort dataset by expression:
- highest to lowest

---

## Task 7.2

Identify:
- top 3 highest expressed genes

---

# Part 8 — Mini Biological Interpretation

Answer in comments:

```r
# 1. Which gene appears most active?
# 2. Do Treatment samples show higher expression?
# 3. Why is it useful to categorize expression levels?
# 4. What would change if this was a real RNA-seq dataset?
```

---

# Bonus Challenge

## B1

Create a scaled expression column:

```r
expression_scaled = expression / max(expression)
```

---

## B2

Find genes that are:
- high expression AND in Treatment group

---

## B3

Create a summary table:
- mean expression per condition

---

⬅️ [Previous Exercise](../basics/02_dataframes) | 🏠 [Home](../index) | ➡️ [Next Exercise](../basics/04_expression_matrix_basics)
