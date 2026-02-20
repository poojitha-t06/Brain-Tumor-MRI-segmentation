# 🏥 Deep Learning for Medical Imaging (CS328) Projects

This repository contains three classical image processing projects implemented as part of **CS328 – Deep Learning for Medical Imaging**.

Each notebook focuses on a different medical imaging segmentation task.

---

# 📁 Projects Included

| Notebook | Project Title |
|-----------|---------------|
| `brain_tumor_mri_segmentation.ipynb` | Brain Tumor MRI Segmentation |
| `retinal_vessel_extraction.ipynb` | Retinal Vessel Extraction |
| `cell_nuclei_separation.ipynb` | Cell Nuclei Separation |

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
