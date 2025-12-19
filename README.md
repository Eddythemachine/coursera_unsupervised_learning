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
- **Initialization Issues:** Standard K-Means is sensitive to random starting points, which can lead to "Local Optima" (bad results).

### 3. Optimization Techniques
- **K-Means++:** A smarter initialization technique that picks starting centroids far apart from each other. (Default in Scikit-Learn).
- **Mini-Batch K-Means:** An optimized version for large datasets that updates centroids using small random batches of data instead of the entire dataset.

### 4. Model Evaluation & Metrics
- **Inertia:** Sum of squared distances (measures how "messy" clusters are). Lower is better.
- **Distortion:** Average squared distance.
- **The Elbow Method:** A technique to scientifically choose the best number of clusters ($k$) by plotting Inertia and finding the inflection point.

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