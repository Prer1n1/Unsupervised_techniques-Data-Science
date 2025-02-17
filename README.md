# Unsupervised_techniques-Data-Science

This implementation explores various clustering and anomaly detection techniques, including k-Means, DBSCAN, Spectral Clustering, and Isolation Forest. Each method is used to analyze and partition data points into meaningful clusters or identify anomalies. The performance of clustering algorithms is evaluated using silhouette scores, while Isolation Forest helps detect and remove anomalies before further clustering analysis.

1. k-Means Clustering Implementation

The KMeans class implements the K-Means clustering algorithm, which partitions data into k clusters. The implementation supports both random and k-means++ initialization methods for centroids to improve convergence.

Parameters:
X: Feature matrix representing the data points.
k: Number of clusters.
max_iters: Maximum iterations for convergence.
tol: Convergence tolerance (if centroids change below this threshold, the algorithm stops).
init: Centroid initialization method (random or k-means++).

Clustering Process:
Centroids are initialized based on the chosen method.
Data points are assigned to the nearest centroid.
New centroids are calculated as the mean of assigned points.
Steps 2 and 3 repeat until convergence or max iterations are reached.
Silhouette Score Calculation and Visualization:

The Silhouette Score evaluates clustering quality by measuring how similar points are within their clusters compared to other clusters. A higher score (closer to 1) indicates better-defined clusters. The average silhouette score and standard deviation are plotted for different values of k and initialization methods to assess clustering performance.

2. DBSCAN Implementation

The DBSCAN (Density-Based Spatial Clustering of Applications with Noise) algorithm groups data points based on density, identifying outliers as noise.

Parameters:
X: Feature matrix.
eps: Maximum distance to consider two points as neighbors.
min_pts: Minimum points required to form a dense region.
Clustering Process:
For each point:
If already labeled, move to the next point.
Find neighbors within eps distance.
If neighbors < min_pts, mark as noise.
Otherwise, start a new cluster and expand it.

Cluster Expansion:
Add the point to the cluster.
For each neighbor:
If unvisited, add to the cluster and continue expansion.
If previously marked as noise, reassign to the cluster.

Supporting Functions:
Euclidean Distance Function: Computes pairwise distances.
Region Query Function: Finds neighbors within eps.
Expand Cluster Function: Recursively assigns points to clusters.

3. Graph-based Clustering with Spectral Clustering
Spectral Clustering leverages graph theory to group data points based on similarity.

Gaussian Similarity Matrix:

The function gaussian_similarity(X, sigma) constructs a similarity matrix W using the Gaussian kernel:
where xi, xj are data points, and sigma controls kernel width.

Unnormalized Spectral Clustering:

Compute the Degree Matrix (D), where each diagonal entry is the sum of W.
Compute the Laplacian Matrix: .
Extract k eigenvectors of L to reduce dimensionality.
Apply k-Means clustering on the eigenvector matrix.

4. Anomaly Detection with the Isolation Forest

The Isolation Forest algorithm detects anomalies by recursively partitioning data and measuring path lengths in isolation trees.
Implementation Components:
build_forest: Constructs multiple isolation trees.
build_isolationforest: Recursively builds an isolation tree by randomly selecting features and split values.
compute_anomaly_scores: Computes anomaly scores based on path lengths across trees. A higher score indicates a higher likelihood of being an anomaly.

Anomaly Detection and Cluster Analysis:
Data is scaled.
Isolation Forest is applied with different contamination levels (1%, 5%, 10%, 15%).
Anomaly scores determine a threshold for marking points as anomalies.
Anomalies are removed, leaving only normal data points.
k-Means clustering (k=2) is applied to the cleaned dataset.
The Silhouette Score evaluates clustering quality post-anomaly removal.
Results include contamination percentage, silhouette score, and remaining data points.
