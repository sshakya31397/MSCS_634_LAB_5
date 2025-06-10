# MSCS 634 - Lab 5: Clustering with Hierarchical and DBSCAN

**Author:** Sauhard Shakya 
**Course:** MSCS 634  
**Assignment:** Lab 5 – Clustering Techniques on the Wine Dataset

---

## Overview

This lab explores unsupervised clustering methods using the **Wine dataset** from the `sklearn.datasets` module. The lab focused on applying two clustering techniques:

- **Agglomerative Hierarchical Clustering**
- **Density-Based Spatial Clustering (DBSCAN)**

The goal was to uncover natural groupings in the data and understand how parameter tuning affects clustering outcomes. Visualizations and evaluation metrics such as Silhouette Score, Homogeneity Score, and Completeness Score were used to assess clustering performance.

---

## Dataset Summary

- **Samples:** 178  
- **Features:** 13 chemical measurements related to wine (e.g., alcohol, ash, flavanoids)
- **Data Type:** All continuous float values
- **Missing Values:** None detected

### Sample Data (First 5 Rows)

| alcohol | malic\_acid | ash  | alcalinity\_of\_ash | magnesium | ... | proline |
| ------- | ----------- | ---- | ------------------- | --------- | --- | ------- |
| 14.23   | 1.71        | 2.43 | 15.6                | 127.0     | ... | 1065.0  |
| 13.20   | 1.78        | 2.14 | 11.2                | 100.0     | ... | 1050.0  |
| 13.16   | 2.36        | 2.67 | 18.6                | 101.0     | ... | 1185.0  |


### Feature Ranges (Descriptive Stats)
- **Alcohol:** min 11.03, max 14.83  
- **Malic Acid:** min 0.74, max 5.80  
- **Proline:** min 278, max 1680  
- **Flavanoids:** avg 2.03, std dev 1.00

---

## Clustering Methods Used

### 1. Hierarchical Clustering
- **Technique:** Agglomerative Clustering with Ward linkage
- **Visualization:** Scatter plots and dendrogram
- **Observation:** Clear separation was visible for 3 clusters; matches with known wine types.

### 2. DBSCAN Clustering
- **Standardized Data:** Yes (via `StandardScaler`)
- **Initial attempt:** `eps=1.5`, `min_samples=5` — result: **no clusters formed**, all data labeled as noise.
- **Tuning attempted:** `eps` values from 0.3 to 1.3 — still resulted in 0 clusters.
- **Conclusion:** DBSCAN did not perform well on raw feature space.

### ✅ PCA + DBSCAN Fix
- **Used PCA to reduce dimensions to 2**
- **Final working config:** `eps=0.5`, `min_samples=3`
- **Clusters Formed:** 2+
- **Visuals:** Distinct clusters with better separation in PCA-reduced space

---

## Key Insights

- Standardization is essential before clustering with DBSCAN or Hierarchical methods.
- DBSCAN is sensitive to parameter tuning (`eps`, `min_samples`) and struggled in high-dimensional feature space.
- PCA helped reveal clustering structure that DBSCAN alone missed.
- Hierarchical clustering worked better without needing dimensionality reduction.

---

## Challenges Faced

- DBSCAN often labeled all points as noise until PCA was applied.
- Selecting the right `eps` required trial-and-error.
- Interpreting clusters was difficult in higher dimensions without visualization support (e.g., PCA).

---

## Files Included

- `Wine_Clustering_Analysis.ipynb` – Main notebook with data loading, clustering, and plots
- `README.md` – This summary document

---

## How to Run

1. Clone the repo:
   ```bash
   git clone https://github.com/yourusername/MSCS_634_Lab_5.git
   cd MSCS_634_Lab_5
