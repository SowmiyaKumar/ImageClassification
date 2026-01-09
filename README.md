# Colon Cancer Histopathology Image Classification

**Course:** Computational Machine Learning
**Project Type:** Group Project (equal contribution)
**Institution:** RMIT University

---

## 👥 Contributors

* **Sowmiya Kumar** 
* **Mohammad Reyaz Mohammad Rafi**

> Although this was a group project, **both contributors were involved across all stages** of the project, including data handling, model design, evaluation, literature comparison, and reporting.

---

## 📌 Project Overview

This project develops a **machine learning system for colon cancer histopathology image analysis**, focusing on **cell-level classification** using small RGB image patches derived from microscopy slides.

The project was approached as a **realistic biomedical ML pipeline**, rather than a simple algorithm comparison, with strong emphasis on:

* Data leakage prevention
* Class imbalance handling
* Robust evaluation
* Independent comparison with peer-reviewed literature
* Extension into **semi-supervised learning**

---

## 🎯 Problem Definition

Each image patch (27×27 RGB) is associated with two prediction tasks:

1. **Cancer Status (Binary)**

   * `isCancerous`: Cancerous vs Non-cancerous

2. **Cell Type (Multi-class)**

   * Fibroblast
   * Inflammatory
   * Epithelial
   * Other

The key challenge is **accurate classification under severe class imbalance**, limited labeled data, and patient-level correlations.

---

## 🧬 Dataset & Constraints

* Modified version of the **CRCHistoPhenotypes** dataset
* 27×27 RGB cell patches extracted from 500×500 histopathology images
* Data from **99 patients**:

  * First 60 patients: full labels (cell type + cancer status)
  * Remaining 39 patients: cancer labels only
* **Important constraint**:

  * Raw image files are **excluded from this repository** due to large size
  * Only structured data files and code are included

📂 **Data directory**

```
data/
├── metadata_csv_files.csv
├── labels.csv
└── (image files excluded due to size constraints)
```

---

## 🔒 Data Leakage Prevention

To ensure clinically realistic evaluation:

* **Patient-wise splitting** was strictly enforced
* Images from the same patient **never appear in both train and test sets**
* This avoids inflated performance caused by spatial similarity between patches

This decision is explicitly justified and documented in the analysis.

---

## ⚙️ Methodology

### 1. Exploratory Data Analysis (EDA)

* Analysed class imbalance across cell types
* Visual inspection of representative patches
* Identified dominance of epithelial cells and under-representation of “Other” class

---

### 2. Baseline Models

* **MLP on flattened pixels**
* Served as:

  * Sanity check
  * Lower-bound benchmark

Result:

* Poor macro F1 (~0.41)
* Failed to detect minority classes

---

### 3. CNN-Based Models (Supervised)

Progressive CNN experimentation:

| Model         | Key Features                           |
| ------------- | -------------------------------------- |
| Basic CNN     | 2 Conv layers + pooling                |
| Augmented CNN | Data augmentation + dropout            |
| Tuned CNN     | Class weights + LR scheduling + tuning |

**Best supervised cell-type model (test):**

* Accuracy ≈ **0.65**
* Macro F1 ≈ **0.58**

Still struggled with rare classes → motivated SSL.

---

## 🔁 Semi-Supervised Learning Extension

To address limited labeled data:

### SSL Strategy

* Used **~10,000 unlabeled images**
* Generated **pseudo-labels** using the best supervised CNN
* Merged pseudo-labeled data with original dataset
* Retrained model with:

  * Data augmentation
  * Class balancing
  * Early stopping

### Results (Cell Type Classification)

| Metric          | Supervised | Semi-Supervised |
| --------------- | ---------- | --------------- |
| Accuracy (Test) | ~0.65      | ~0.70           |
| Macro F1 (Test) | ~0.58      | **~0.64**       |

✅ Notable improvement for **minority class (Other)**
✅ Demonstrated effectiveness of SSL in medical imaging contexts

---

## 📊 Final Performance Summary

### Cell Type Classification (Best Model)

* **Semi-Supervised CNN**
* Test Accuracy: **~70%**
* Test Macro F1: **~0.64**

### Cancer Status Classification

* Strong generalisation
* Accuracy ≈ **89%**
* Macro F1 ≈ **0.88**
* Stable across validation and test sets

---

## 📚 Independent Literature Comparison

Compared against:

* **Sirinukunwattana et al. (2016)** – IEEE TMI
  *Locality Sensitive Deep Learning for Nuclei Classification*

| Model                      | Weighted F1 |
| -------------------------- | ----------- |
| Baseline MLP (ours)        | 0.41        |
| Tuned CNN (ours)           | 0.58        |
| Semi-Supervised CNN (ours) | **0.64**    |
| Softmax CNN + NEP (paper)  | **0.784**   |

### Interpretation

* Literature uses:

  * Larger datasets
  * More balanced labels
  * Different feature engineering
* Our results are competitive **given stricter leakage control and limited labels**

---

## 🧠 Key Learnings

* Patient-wise splitting is critical in medical ML
* Accuracy alone is misleading under class imbalance
* Macro F1 and per-class metrics provide better insight
* Semi-supervised learning is highly effective when labels are scarce
* Transparent comparison with literature strengthens credibility

---

## 🧰 Tech Stack

* **Language:** Python
* **Libraries:** TensorFlow / Keras, NumPy, Pandas, scikit-learn, Matplotlib
* **Environment:** Jupyter Notebook
* **ML Concepts:** CNNs, class weighting, data augmentation, SSL, evaluation metrics

---

## 📁 Repository Contents

```
.
├── data/                  # Structured data (images excluded)
├── notebooks/
│   └── colon_cancer_ml.ipynb
├
├── README.md
```

---

📄 References

1. Sirinukunwattana, K. et al. (2016).
Locality Sensitive Deep Learning for Detection and Classification of Nuclei in Routine Colon Cancer Histology Images.
IEEE Transactions on Medical Imaging.

---

## 🎓 Academic Note

This project was completed as part of **Computational Machine Learning coursework at RMIT University** and is shared for **learning and portfolio demonstration purposes only**.



