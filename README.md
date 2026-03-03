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
| `white_blood_cell_segmentation.ipynb` | White Blood Cell Segmentation - K-Means vs Fuzzy C-Means |
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

This project performs segmentation of **White Blood Cell (WBC) nucleus** from microscopic blood smear images using two unsupervised clustering methods:

- **K-Means (Hard Clustering)**
- **Fuzzy C-Means (Soft Clustering)**

The goal is to compare hard vs soft clustering and evaluate boundary quality.

---

## 📂 Dataset

KRD WBC Dataset  

🔗 Dataset Link: https://www.kaggle.com/datasets/inhvnnhn/krd-wbc-dataset

Dataset Structure:

KRD WBC Dataset/
- train/
  - images/
  - mask/

- Total images used: **480**
- Each image has a corresponding ground truth mask.

---

## 🛠 Methods Implemented

### 1️⃣ Preprocessing

- Images resized to **128 × 128**
- Converted from **RGB → LAB color space**
- Only **L channel** used for clustering
- Masks converted to binary (0 and 1)

---

### 2️⃣ K-Means Clustering (Hard Segmentation)

- Number of clusters: **3**
- Pixel intensities clustered using K-Means
- Each pixel assigned to one cluster
- Darkest cluster selected as nucleus
- Binary mask generated

✔ Fast  
✔ Simple  
✘ No uncertainty handling  

---

### 3️⃣ Fuzzy C-Means (Soft Segmentation)

- Number of clusters: **3**
- Fuzziness parameter: **m = 2**
- Each pixel gets membership values
- Final label chosen using maximum membership
- Darkest cluster selected as nucleus

✔ Handles ambiguity  
✔ Soft pixel assignment  
✘ Slower than K-Means  

---

## 📊 Evaluation Metric

Boundary-based evaluation was used.

Steps:
- Morphological gradient applied to get boundaries
- Compared predicted boundary with ground truth boundary

Metrics computed:
- Accuracy
- Precision
- Recall
- F1-Score

---

## 📈 Results (Full Dataset – 480 Images)

### 🔹 K-Means

- Accuracy: **0.6438**
- Precision: **0.0347**
- Recall: **0.5595**
- F1 Score: **0.0615**

### 🔹 Fuzzy C-Means

- Accuracy: **0.6367**
- Precision: **0.0337**
- Recall: **0.5646**
- F1 Score: **0.0602**

---

## 🔎 Observations

- Both methods give similar performance.
- Recall is moderate (~0.56), meaning nucleus boundary is often detected.
- Precision is low, indicating false boundary detections.
- FCM slightly improves recall but is computationally slower.
- K-Means is faster and easier to implement.
- Results depend strongly on staining variation and intensity distribution.
---

