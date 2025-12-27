# Coursera Unsupervised Learning

This repository documents my progress on the IBM Coursera Unsupervised Learning course. It contains study notes, implementations, and labs focusing on Clustering algorithms and Dimensionality Reduction.

## 📚 Concepts Covered

### 1. Introduction to Unsupervised Learning
- **Difference from Supervised Learning:** Working with unlabeled data to find hidden structures rather than predicting known outcomes.
- **Main Use Cases:**
  - **Clustering:** Grouping similar data points (e.g., Customer Segmentation, Anomaly Detection).
  - **Dimensionality Reduction:** Reducing features to fight the "Curse of Dimensionality" (e.g., Image Compression, PCA).

### 2. The K-Means Algorithm
- **Core Logic:** An iterative process of **Assignment** (picking the nearest centroid) and **Update** (moving centroids to the mean).
- **Convergence:** The state where centroids stop moving and the algorithm finishes.
- **Initialization Issues:** Standard K-Means is sensitive to random starting points, which can lead to "Local Optima" (bad results). We visualized this by changing the `random_state`.

### 3. Optimization Techniques
- **K-Means++:** A smarter initialization technique that picks starting centroids far apart from each other. (Default in Scikit-Learn).
- **Mini-Batch K-Means:** An optimized version for large datasets that updates centroids using small random batches of data instead of the entire dataset.

### 4. Model Evaluation & Metrics
- **Inertia:** Sum of squared distances (measures how "messy" clusters are). Lower is better.
- **The Elbow Method:** A technique to scientifically choose the best number of clusters ($k$) by plotting Inertia and finding the inflection point.
- **Silhouette Coefficient:** An alternative metric useful when the "Elbow" is not clearly defined.

### 5. Advanced Clustering Algorithms
Beyond K-Means, we explored algorithms that handle non-spherical data and do not require pre-defining $k$:
- **Hierarchical Clustering (Agglomerative):** Builds a hierarchy of clusters from the bottom up. Visualized using **Dendrograms** to determine the optimal cut-off point.
- **DBSCAN (Density-Based Spatial Clustering):** Groups points that are closely packed together (high density).
  - **Key Parameters:** $\epsilon$ (Epsilon - radius) and `min_samples`.
  - **Advantage:** Can find arbitrary shapes and explicitly identifies **Noise/Outliers** (points that don't belong to any cluster).
- **MeanShift:** A centroid-based algorithm that works by updating candidates for centroids to be the mean of the points within a given region. It does not require specifying the number of clusters.

### 6. Distance Metrics & The Curse of Dimensionality
- **The Curse of Dimensionality:** As features increase, data becomes sparse, and the distance between the nearest and farthest points becomes negligible.
- **Distance Metrics:**
  - **Euclidean:** Standard straight-line distance.
  - **Cosine:** Measures the angle (direction); crucial for text/NLP.
  - **Jaccard:** Measures dissimilarity between sets ($1 - \text{Intersection over Union}$).

---

## 🔬 Labs & Practical Exercises

### Lab 1: K-Means Clustering & Image Quantization
**Objective:** Master K-Means parameter tuning and apply clustering to image compression.
- **Synthetic Data:** Analyzed sensitivity to initialization and used the Elbow Method to find optimal $k$.
- **Image Quantization:** Compressed a 480x640 image by treating pixels as a dataset. Reduced millions of colors to just $k=8$ dominant colors by replacing pixels with their nearest cluster centroid.

### Lab 2: Investigating the Curse of Dimensionality
**Objective:** Visualize and quantify how high-dimensional space impacts data density and model performance.
- **Geometric Intuition:** Calculated the volume ratio of a hypersphere inside a hypercube. As dimensions ($d$) rose, the volume of the sphere vanished, proving that in high dimensions, **most data points live in the "corners"**.
- **Model Impact:** Demonstrated that adding features without selection caused `DecisionTreeClassifier` accuracy to drop due to overfitting and sparsity.

### Lab 3: Distance Metrics Analysis
**Objective:** Analyze how choosing the wrong distance metric can alter algorithm performance.
- **Comparison:** Implemented Euclidean, Manhattan, Cosine, and Jaccard distances.
- **DBSCAN Sensitivity:** Visualized how changing the metric (e.g., to Cosine) completely changes the cluster shapes (cones vs. spheres).

### Lab 4: Advanced Clustering & Feature Engineering (Wine Quality)
**Objective:** Compare K-Means vs. Agglomerative Clustering and use clustering results to improve Supervised Learning models.
- **Data Exploration:** Analyzed wine chemical properties, applying Log Transforms to skewed features and scaling via `StandardScaler`.
- **Method Comparison:** Compared K-Means and Agglomerative Clustering (Ward linkage) on the same dataset. Visualized the hierarchy using a **Dendrogram**.
- **Clustering as a Feature:**
  - Created a binary target variable (High Quality vs. Low Quality).
  - **Experiment:** Trained a Random Forest Classifier *with* and *without* the K-Means cluster ID as a feature.
  - **Result:** Including the cluster label as a feature improved the **ROC-AUC score**, proving that unsupervised learning can generate valuable inputs for supervised models.

### Lab 5: DBSCAN & Anomaly Detection
**Objective:** Use DBSCAN to identify noise and handle non-linear data.
- **Visual Proof:** Applied DBSCAN to a grid dataset where K-Means would fail. Successfully identified the "Core" points and separated "Noise."
- **Handwriting Analysis:**
  - **The Scenario:** Proving "bad handwriting" is statistically distinguishable.
  - **Pipeline:** Combined clean MNIST digits with "messy" handwritten samples.
  - **Dimensionality Reduction:** Used **t-SNE** to visualize the high-dimensional pixel data in 2D.
  - **Result:** DBSCAN classified the messy handwriting as **Noise (-1 label)** or grouped it into incorrect clusters, quantitatively proving the writing was illegible.

### Lab 6: Image Segmentation with MeanShift
**Objective:** Apply MeanShift to segment images without pre-defining the number of colors.
- **Process:**
  - Converted image from BGR to RGB and applied `medianBlur` to smooth noise.
  - Estimated **Bandwidth** (the window size) automatically using `sklearn.cluster.estimate_bandwidth`.
  - **Outcome:** The algorithm automatically determined the number of distinct color regions (clusters) and segmented the image ("inna.jpeg") effectively.

---

## 🚀 Independent Project: Customer Personality Analysis

After mastering the concepts in the course, I applied K-Means clustering to a real-world marketing dataset to perform **Customer Segmentation**.

### 1. The Challenge
The goal was to transform raw customer data (demographics, purchase history, web activity) into actionable segments to help the marketing team move away from "one-size-fits-all" campaigns.

### 2. The Process & Technical Challenges
* **Data Cleaning & Outlier Removal:** Identified skewed columns and removed extreme outliers ("Whales").
* **Advanced Preprocessing Pipeline:**
    * Built a Scikit-Learn `ColumnTransformer`.
    * Used **PowerTransformer (Yeo-Johnson)** to fix skewness in continuous variables.
* **Model Selection:**
    * Used the **Elbow Method** and **Silhouette Scores** to select **$k=3$**.

### 3. Key Insights (The Personas)
| Cluster | Persona Name | Key Characteristics | Strategy |
| :--- | :--- | :--- | :--- |
| **0** | **The Budget Browsers** | Low Income, Parents with **Toddlers**. | Cost control; Low-cost activation coupons. |
| **1** | **The VIPs** | High Income, **No Kids/Empty Nesters**. High Spend. | Exclusive catalog offers. |
| **2** | **The Deal Hunters** | Middle Income, Parents with **Teenagers**. | Bundle offers and sales. |

---

## 🛠️ Installation & Setup

This project uses **Python** and **VS Code**.

### Prerequisites
- Python installed on your machine.
- VS Code installed.

### Setting up the Environment

1. **Clone or Download** this repository.
2. **Open the folder** in VS Code.
3. **Select your Python Interpreter**:
   - Press `Ctrl + Shift + P` (Windows/Linux) or `Cmd + Shift + P` (Mac).
   - Type `Python: Select Interpreter`.
4. **Install Dependencies**:
   Open the VS Code terminal and run:
   ```bash
   pip install -r requirements.txt

   ### Summary of Changes made:
1.  **Added Section 5 (Advanced Clustering):** Defined Hierarchical, DBSCAN, and MeanShift concepts.
2.  **Added Lab 4:** Summarized the Wine Quality lab, specifically focusing on the "Clustering as Feature Engineering" aspect (using Random Forest ROC-AUC).
3.  **Added Lab 5:** Summarized the DBSCAN lab, highlighting the t-SNE usage and the "Handwriting as Noise" detection use case.
4.  **Added Lab 6:** Included the MeanShift image segmentation work you provided in the code snippet.