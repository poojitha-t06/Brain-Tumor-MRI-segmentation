# 🏥 Deep Learning for Medical Imaging (CS328) Projects

This repository contains four classical image processing projects implemented as part of **CS328 – Deep Learning for Medical Imaging**.

Each notebook focuses on a different medical imaging segmentation task.

---

# 📁 Projects Included

| Notebook | Project Title |
|-----------|---------------|
| `brain_tumor_mri_segmentation.ipynb` | Brain Tumor MRI Segmentation |
| `retinal_vessel_extraction.ipynb` | Retinal Vessel Extraction |
| `cell_nuclei_separation.ipynb` | Cell Nuclei Separation |
| `white_bloodcell_segmentation.ipynb` | White Blood Cell Segmentation - K-Means vs Fuzzy C-Means |
---

# 1️⃣ Brain Tumor MRI Segmentation

## 📌 Project Overview

This project evaluates classical image processing techniques for brain tumor segmentation in MRI images.

The objective is to analyze how well traditional thresholding methods (Otsu and Sauvola) perform on medical imaging data and understand the limitations of non-learning-based approaches in tumor segmentation.

---

## 📂 Dataset

Brain MRI slices with corresponding binary tumor masks.

- **Total slices:** 3929  
- **Empty slices (no tumor):** 2556  
- **Tumor-containing slices:** 1373  

⚠️ Evaluation is performed **only on tumor-containing slices** to avoid bias caused by empty masks.

🔗 Dataset Link:  
https://www.kaggle.com/datasets/mateuszbuda/lgg-mri-segmentation/data

---

## 🛠 Methods Implemented

### 1️⃣ Preprocessing
- Image normalization
- Gaussian smoothing (for Otsu)
- Binary mask conversion

### 2️⃣ Segmentation Techniques
- **Otsu Global Thresholding**
- **Sauvola Adaptive Thresholding**

### 3️⃣ Post-Processing
- Morphological Opening
- Morphological Closing

### 4️⃣ Evaluation Metrics
- Dice Coefficient
- Jaccard Index (IoU)

Metrics are computed only on non-empty tumor slices.

---

## 📊 Final Results

| Method   | Dice Score | Jaccard Index |
|----------|------------|---------------|
| Otsu     | 0.145      | 0.081         |
| Sauvola  | 0.085      | 0.046         |

---

## 🔎 Observations

- Classical thresholding methods perform poorly on MRI tumor segmentation.
- MRI intensity inhomogeneity affects global threshold performance.
- Adaptive thresholding (Sauvola) did not outperform Otsu in this dataset.
- Post-processing improves stability but does not significantly increase segmentation accuracy.

---

## 🎯 Conclusion

Classical image processing techniques are insufficient for accurate brain tumor segmentation.

This project establishes a classical baseline and highlights the need for spatial learning models (e.g., U-Net) for improved medical image segmentation performance.

---

# 2️⃣ Retinal Vessel Extraction

## 📌 Project Overview

This project evaluates adaptive thresholding techniques for retinal blood vessel segmentation.

The goal is to compare classical local thresholding methods and analyze their effectiveness in detecting thin vascular structures (through sensitivity).

---

## 📂 Dataset

- DRIVE Retinal Vessel Dataset  
- Total Training Images Used: **20**

🔗 Dataset Link:  
https://www.kaggle.com/datasets/andrewmvd/drive-digital-retinal-images-for-vessel-extraction/data

---

## 🛠 Methods Implemented

### 1️⃣ Preprocessing
- RGB to Grayscale conversion
- Normalization

### 2️⃣ Segmentation Techniques
- **Niblack Thresholding**
- **Sauvola Thresholding**

Both methods are adaptive/local thresholding approaches suitable for uneven illumination.

### 3️⃣ Evaluation Metric
- **Sensitivity (Recall)**

Sensitivity is used because vessel segmentation is highly class-imbalanced (thin vessels vs background).

---

## 📊 Results

| Method   | Average Sensitivity |
|----------|--------------------|
| Niblack  | 0.2089 |
| Sauvola  | 0.9448 |

---

## 🔎 Observations

- Niblack thresholding performs poorly for thin vessel detection.
- Sauvola significantly improves vessel sensitivity.
- Adaptive local thresholding is more suitable for retinal vessel segmentation compared to global approaches.

---

# 3️⃣ Cell Nuclei Separation (Watershed Segmentation)

## 📌 Project Overview

This project implements Watershed segmentation to separate overlapping cell nuclei.

The objective is to compare:

- Watershed **without proper marker control**
- Watershed **with marker-controlled preprocessing**

---

## 📂 Dataset

- Microscopy cell nuclei dataset (stage1_train)

🔗 Dataset Link:  
https://www.kaggle.com/datasets/mahmudulhasantasin/data-science-bowl-2018-competition-merged-mask

---

## 🛠 Methods Implemented

### 1️⃣ Preprocessing
- RGB to Grayscale conversion
- Otsu Binary Thresholding

### 2️⃣ Watershed Without Marker Control
- Direct distance transform
- Connected components
- Watershed segmentation

### 3️⃣ Marker-Controlled Watershed
- Morphological Opening
- Sure foreground extraction
- Sure background estimation
- Connected component labeling
- Marker-based watershed

---

## 📊 Evaluation Metrics

- **Dice Score**
- **Object Count Comparison**

---

## 📈 Results

### 🔹 Dice Score Comparison

| Method | Dice Score |
|--------|------------|
| Without Marker Control | 0.7229 |
| With Marker Control | 0.6454 |

### 🔹 Object Count Comparison

| Category | Count |
|----------|-------|
| Ground Truth Nuclei | 28 |
| Basic Watershed | 18 |
| Marker Controlled | 14 |

---

## 🔎 Observations

- Basic watershed achieves higher Dice score but under-segments objects.
- Marker-controlled watershed produces cleaner boundaries but detects fewer nuclei.
- Proper marker selection significantly affects instance segmentation quality.
- Classical watershed methods are sensitive to preprocessing choices.

---
# 4️⃣ White Blood Cell Segmentation

## 📌 Project Overview

This project focuses on segmenting White Blood Cells (WBCs) from microscopic blood smear images using classical image processing techniques.

The objective is to  Segment WBC nucleus & cytoplasm.

---

## 📂 Dataset

https://dl.raabindata.com/WBC/nucleus_cytoplasm_GT/

---

## 🛠 Methods Implemented

### 1️⃣ Data Preparation

- Input RGB microscopic blood smear images  
- Ground truth masks (binary)  
- Pixel reshaping from image → 2D feature space (N × 3)  
- Normalization of mask (0–1 scaling)  


### 2️⃣ K-Means Clustering (Hard Segmentation)

- Number of clusters: 3  
- Clustering performed on RGB pixel space  
- Each pixel assigned to exactly one cluster  
- Cluster means computed  
- Cluster with lowest intensity selected as nucleus  
- Binary mask generated from selected cluster  

✔ Hard assignment  
✔ Fast convergence  
✘ No uncertainty modeling  


### 3️⃣ Fuzzy C-Means (FCM) Clustering (Soft Segmentation)

- Number of clusters: 3  
- Fuzziness parameter: m = 2  
- Iterative optimization using membership matrix  
- Each pixel has soft membership values  
- Final label selected using argmax of membership  
- Darkest cluster selected as nucleus  

✔ Handles ambiguity better  
✔ Soft pixel memberships  
✘ Computationally heavier than K-Means  


---

## 📊 Evaluation Metric

### Dice Coefficient

\[
Dice = \frac{2|A \cap B|}{|A| + |B|}
\]

Where:

- **A** = Predicted nucleus mask  
- **B** = Ground truth mask  

Dice measures overlap between predicted segmentation and ground truth.


---

## 📈 Results

### 🔹 Average Dice Score (First 20 Images)

| Method   | Average Dice Score |
|----------|-------------------|
| K-Means  |0.868 |
| FCM      | 0.871 |



---

## 🔎 Observations

- K-Means performs fast and gives reasonable nucleus segmentation.  
- FCM models pixel uncertainty better due to soft clustering.  
- Selecting the correct nucleus cluster (based on minimum mean intensity) is crucial.  
- Both methods depend heavily on color distribution.  
- Performance varies with staining variations and lighting.
