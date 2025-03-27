# Composite Silhouette 

[![PyPI Version](https://img.shields.io/pypi/v/composite-silhouette?logo=pypi)](https://pypi.org/project/composite-silhouette/)

Composite Silhouette is a Python package for robust clustering evaluation.
It introduces a composite metric that combines micro-averaged and macro-averaged silhouette using statistical weighting.
This provides a more nuanced assessment of clustering quality, helping identify the optimal number of clusters and compare performance across different clustering scenarios with greater confidence.
The framework is especially useful for data scientists, ML engineers, and researchers who want reliable metrics for centroid-based clustering.

## Overview and Methodology 
In standard clustering evaluation, the **silhouette coefficient** is widely used to measure how well each data point fits into its cluster in terms of intra-cluster cohesion and inter-cluster separation.
It can be aggregated as:
- **Micro-average:** The overall average silhouette score across all data points.
- **Macro-average:** The per-cluster average silhouette score.

**Composite Silhouette** merges these two perspectives using a statistically-driven weighting strategy.
The method performs repeated subsampled clustering to compute both micro- and macro-averaged silhouette scores.
A Wilcoxon signed-rank test is then applied to their paired differences across subsamples to determine if one consistently and significantly outperforms the other.
The final score is the weighted combination of the sample averages of micro- and macro-averaged scores: *w<sub>m</sub> · S<sub>micro</sub> + w<sub>M</sub> · S<sub>macro</sub>*
This convex combination keeps the result within the range of the individual scores and ties it meaningfully to both.
When a statistically significant difference is found, more weight (at least 75%) is assigned to the dominant metric, while the other still contributes proportionally to the average difference.

