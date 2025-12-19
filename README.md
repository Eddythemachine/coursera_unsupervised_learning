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

---

## 🔬 Labs & Practical Exercises

### Lab 1: K-Means Clustering & Image Quantization
**Objective:** Master K-Means parameter tuning and apply clustering to image compression.

#### A. Synthetic Data Analysis
- **Sensitivity to Initialization:** We ran K-Means on synthetic blobs using different `random_state` values (10 vs 20) to observe how starting points affect the final cluster shapes.
- **Finding the Elbow:** We calculated Inertia for $k=1$ to $10$ on a dataset generated via `make_blobs` to identify the optimal cluster count.

#### B. Image Color Quantization
- **Concept:** Treating an image not as a picture, but as a dataset of pixels (Rows = Total Pixels, Columns = R, G, B values).
- **Process:**
  1. Reshaped a 480x640 image into a flat table (307,200 rows x 3 columns).
  2. Applied K-Means to find the "dominant colors" (clusters).
  3. Replaced every pixel with its nearest cluster center color.
- **Result:** Successfully compressed an image from millions of potential colors down to just $k$ colors (e.g., $k=8$) while retaining the image structure.

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
   - Choose your global Python version or your specific virtual environment.

4. **Install Dependencies**:
   Open the VS Code terminal (`Ctrl + ` ` `) and run:
   ```bash
   pip install -r requirements.txt