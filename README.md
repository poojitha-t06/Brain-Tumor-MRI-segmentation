# 🧠 Brain Tumor MRI Segmentation Using OTSU and Sauvola

## 📌 Project Overview

This project evaluates classical image processing techniques for brain tumor segmentation in MRI images.

The objective is to analyze how well traditional thresholding methods (Otsu and Sauvola) perform on medical imaging data and understand the limitations of non-learning-based approaches in tumor segmentation.

This work serves as a **classical baseline study** for brain tumor MRI segmentation.

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


  

  # 🚀 How to Run This Project

## 1️⃣ Clone the Repository

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name

```
## 2️⃣ Create Virtual Environment (Recommended)

```bash
python -m venv venv
```

### Activate Environment

**Windows**
```bash
venv\Scripts\activate
```
---


## 3️⃣ Install Required Libraries

```bash
pip install numpy opencv-python matplotlib scikit-image
```

If using Jupyter:

```bash
pip install notebook
```

---

## 4️⃣ Download Dataset

- Download the dataset from the provided link.
- Extract images and masks into the project directory.


- Update dataset paths inside the notebook if necessary.

---

## 5️⃣ Run the Notebook

Start Jupyter Notebook:

```bash
jupyter notebook
```

Open:

```
brain_tumor_mri_segmentation.ipynb
```

Run all cells sequentially.
