# 🏢 Shape Complexity Classification using EDA

This project analyzes and clusters 1183 bitmap images of building layouts (shapes) to classify them into **low**, **medium**, and **high** complexity groups. It also predicts similar layouts based on user input by leveraging shape-based features and clustering methods.

---

## 📌 Problem Statement

Given bitmap images (640×480 pixels) of building layouts, the goal is to:

- Cluster the layouts based on structural complexity.
- Develop a model to predict layout categories based on user-defined features.
- Define and refine shape complexity criteria using geometrical and statistical descriptors.

---

## 🔍 Solution Overview

1. **Exploratory Data Analysis (EDA):**
   - Filtered out unique images.
   - Extracted features such as:
     - Area of yellow polygon (building layout).
     - Length and width of the tight bounding box.
     - Number of corners (vertices) in the shape.

2. **Feature Engineering:**
   - Manually derived geometric features:
     - **Solidity**
     - **Compactness**
     - **Roundness**
     - **Hu Moments**

3. **Clustering Approaches:**
   - **Method 1: K-Means Clustering**  
     Based on manually engineered features.
   - **Method 2: CNN + Hierarchical Clustering**  
     Used pretrained **VGG16** for automatic feature extraction.

4. **Prediction Model:**
   - Takes user input for area, bounding box dimensions, and desired complexity.
   - Uses Euclidean distance to suggest the top 5 matching layouts.

---

## 📐 Features Extracted

- **Area of Yellow Region:** Using OpenCV color filtering.
- **Bounding Box Dimensions:** Using Canny edge detection and minimal area rectangle.
- **Number of Corners:** Detected using "good features to track" from OpenCV.
- **Solidity:** Ratio of contour area to convex hull area.
- **Compactness:**  
  \[
  \text{Compactness} = \frac{{\text{Perimeter}^2}}{4\pi \times \text{Area}}
  \]
- **Roundness:**  
  \[
  \text{Roundness} = \frac{4 \times \text{Area}}{\pi \times \text{Perimeter}^2}
  \]
- **Hu Moments:** 7 invariant descriptors used for shape analysis and object recognition.

---

## 🧠 Complexity Classification Criteria

- **Number of Corners:**
  - More corners → more complexity.

- **Curvature (Roundness):**
  - More round/curved edges → higher complexity.

- **Compactness:**
  - High perimeter with relatively low area → more complex.

---

## 🧮 Prediction Mechanism

- User provides values for area, length & width of bounding box, and desired complexity.
- Inputs are normalized and converted into a vector.
- The system computes Euclidean distances between this vector and the dataset.
- It suggests 5 nearest images by iteratively tweaking input values (±5%).

---

## 💡 Future Suggestions

We propose a more nuanced method to improve complexity evaluation:

1. Extract coordinates of all detected corners.
2. Compute all pairwise side lengths.
3. Calculate:
   - Average of the **smallest 20%** of lengths.
   - Average of **all** side lengths.
4. Define a new metric **B** = (Average of shortest sides) / (Average of all sides).

### Interpretation of B:
- **B << 1** → corners are unevenly spaced → high complexity.
- **B ≈ 1** → corners are evenly spaced → low complexity.

This new metric improves discrimination between similarly shaped layouts with different spatial characteristics.

---

## 🛠️ Tech Stack

- **Language:** Python
- **Libraries:** 
  - OpenCV
  - NumPy
  - Scikit-learn
  - Matplotlib
  - TensorFlow/Keras (for CNNs)


