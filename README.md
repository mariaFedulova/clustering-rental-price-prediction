# Clustering Methods: Implementation & Comparison

## Project Overview
This project explores several unsupervised clustering approaches: K-means, DBSCAN, hierarchical, and Gaussian Mixture by implementing selected algorithms manually and comparing them against standard library implementations. The clustering outputs are then evaluated both on internal quality metrics and as engineered features in a downstream regression model.

## Tools & Technologies
- **Python Libraries**: NumPy, Pandas, Matplotlib, Scikit-learn
- **Clustering Algorithms**: centroid-based clustering (custom + library), density-based clustering (custom + library), hierarchical (agglomerative) clustering, Gaussian mixture models
- **Regression Model**: Lasso Regression (with feature scaling)
- **Evaluation Metrics**: Silhouette Score, Distortion, MAE, RMSE, R²
- **Dataset**: real estate listings with geographic and categorical attributes

---

## K-means Clustering (Custom Implementation)
A centroid-based clustering algorithm was implemented from scratch, using a distance-weighted initialization strategy to spread starting centroids across the data and improve convergence stability. The model was applied to geographic coordinates and benchmarked against a standard library implementation.

**Key Findings:**
- Custom and library implementations produced comparable quality metrics, confirming the manual implementation was correct
- The library version ran noticeably faster due to internal optimizations
- Adding the resulting cluster label as an input feature to a regression model changed its predictive performance

---

## DBSCAN Clustering (Custom Implementation)
A density-based clustering algorithm was implemented from scratch using a straightforward neighbor-search approach, with its radius parameter selected via a distance-distribution plot. Results were compared against a standard library implementation, which relies on a spatial indexing structure for faster neighbor lookups.

**Key Findings:**
- Both versions produced consistent cluster assignments and identified outlier points
- The manual implementation scales quadratically with data size, while the indexed library version scales much better on larger datasets
- Unlike centroid-based clustering, this method determined the number of clusters automatically and could form clusters of arbitrary shape

---

## AgglomerativeClustering and Gaussian Mixture algorithms
Library implementations of agglomerative (bottom-up) clustering and a Gaussian mixture model (fit via an iterative expectation-maximization procedure) were applied to the same data for further comparison.

**Key Findings:**
- Hierarchical clustering's higher computational cost comes from building a full pairwise distance structure over all data points
- The probabilistic method assigned soft, probability-based cluster membership, allowing for non-spherical cluster shapes
- Both were evaluated using the same internal metrics and downstream regression impact as the other methods

---

## Clustering on Alternative Feature Sets
Beyond geographic coordinates, clustering was repeated using a different set of categorical/numeric attributes to test whether an alternative feature space produces clusters that are more useful for the downstream prediction task.

**Key Findings:**
- Cluster quality and their contribution to the regression model varied depending on which features were used for clustering
- Different feature spaces captured different structure in the data, leading to different downstream results

---

## Overall Conclusion
The custom implementations matched library results in clustering quality, validating their correctness, while showing the clear performance advantage of optimized, index-based implementations at scale. Using cluster assignments as engineered features for a downstream regression model demonstrated that clustering can add predictive value beyond describing data structure on its own with the choice of clustering features meaningfully affecting the outcome.
