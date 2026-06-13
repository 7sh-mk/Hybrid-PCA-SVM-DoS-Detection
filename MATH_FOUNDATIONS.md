#  Mathematical Foundations

This file documents the core Linear Algebra concepts used in this project.

---

##  Standard Scaling (Z-score Normalization)

Before applying PCA, all features must be normalized so no single feature
dominates due to its scale.

$$Z = \frac{x - \mu}{\sigma}$$

- $x$ = original feature value
- $\mu$ = mean of the feature
- $\sigma$ = standard deviation

---

##  Covariance Matrix

Captures how features relate to each other across the dataset.
High covariance = redundant features that PCA can eliminate.

$$C = \frac{1}{N-1} \sum_{i=1}^{N}(X_i - \bar{X})(X_i - \bar{X})^T$$

In this project: the covariance matrix had shape **(318 × 318)**,
revealing significant multicollinearity across network traffic features.

---

## Eigen-Decomposition

The core of PCA. Finds the principal directions of maximum variance.

$$Cv = \lambda v$$

- $C$ = covariance matrix
- $v$ = eigenvector (principal component direction)
- $\lambda$ = eigenvalue (amount of variance explained)

---

##  Orthogonality of Principal Components

PCA components are orthogonal — they capture independent variance
with no overlap.

$$v_i^T v_j = 0 \quad \text{for } i \neq j$$

The dot product of the first two PCs in this project = **0.000000000000000**
 Confirmed orthogonal.

---

##  Explained Variance Ratio

Determines how many principal components to keep.

$$EVR_i = \frac{\lambda_i}{\sum_{k=1}^{n} \lambda_k}$$

In this project:
- PC1 captured **30.53%** of total variance
- Top 56 components retained **95%** of total variance
- Original: 318 features → Reduced: **56 components**

---

##  Data Projection

Projects the high-dimensional data into the reduced PCA space.

$$X_{projected} = X_{scaled} \cdot W$$

- $X_{scaled}$ = standardized data matrix (700,774 × 318)
- $W$ = projection matrix (318 × 56)
- $X_{projected}$ = reduced data (700,774 × 56)

---

##  Normal Equation

Computes the optimal coefficients for the decision boundary.

$$\hat{X} = (A^TA)^{-1}A^Tb$$

- $A$ = feature matrix with bias column
- $b$ = target labels
- $\hat{X}$ = learned coefficients

Decision boundary threshold:

$$\hat{X}_0 + \hat{X}_1x_1 + \hat{X}_2x_2 = 0.5$$

---

##  SVM Hyperplane

The SVM finds the optimal separating hyperplane with maximum margin.

$$w^Tx + b = 0$$

---

##  RBF Kernel

Allows SVM to classify non-linearly separable data by mapping it
into a higher-dimensional space.

$$K(x_i, x_j) = \exp\left(-\gamma \|x_i - x_j\|^2\right)$$

In this project: RBF kernel achieved **Precision = 98.77%** on attack detection.

---

##  Singular Value Decomposition (SVD)

An alternative to eigen-decomposition, numerically more stable
for high-dimensional datasets.

$$X_{scaled} = U \Sigma V^T$$

- $U$ = orthonormal basis for column space
- $\Sigma$ = diagonal matrix of singular values
- $V^T$ = orthonormal basis for row space
