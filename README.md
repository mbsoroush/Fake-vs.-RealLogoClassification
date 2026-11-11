# 🏷️ Fake vs. Real Logo Classification

![Python](https://img.shields.io/badge/Python-3.x-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-Deep%20Learning-red)
![Torchvision](https://img.shields.io/badge/Torchvision-ResNet18-orange)
![Computer Vision](https://img.shields.io/badge/Field-Computer%20Vision-green)

---

## 🔰 Overview

This project is a **Deep Learning-based Fake vs. Real Logo Classification System** built using PyTorch and Convolutional Neural Networks (CNNs).

It aims to distinguish between counterfeit and genuine brand logos using image classification techniques.

The project explores two approaches:
1. **Baseline Model** → Training a ResNet18 architecture from scratch for binary logo classification.
2. **Transfer Learning** → Fine-tuning a pretrained ResNet18 model using ImageNet weights, data augmentation, and hyperparameter adjustments to improve classification performance.

The final model achieves **97.25% test accuracy**, demonstrating the effectiveness of Transfer Learning for logo authenticity classification.

---

## 📦 Dataset

The project uses a dataset containing **825 logo images** belonging to two categories:

- ❌ **Fake:** 550 images
- ✅ **Genuine:** 275 images

Each record contains:
- An image filename.
- A brand name.
- A classification label (Fake or Genuine).

### 📊 Dataset Distribution

| Category | Number of Images |
|---|---:|
| Fake | 550 |
| Genuine | 275 |
| **Total** | **825** |

### Dataset Splitting

The dataset is divided into training, validation, and testing subsets. The splitting process is performed separately for each brand.

| Dataset | Number of Images |
|---|---:|
| Training | 583 |
| Validation | 60 |
| Testing | 182 |
| **Total** | **825** |

---

## ⚙️ Installation & Requirements

The notebook was developed using Python and PyTorch in a Kaggle Notebook environment.

Install the required libraries:

```bash
pip install torch torchvision
pip install numpy pandas matplotlib seaborn
pip install scikit-learn opencv-python pillow
```

Clone the repository:

```bash
git clone https://github.com/mbsoroush/Fake-Real-Logo-Classification.git
cd Fake-Real-Logo-Classification
```

**Note:** The dataset must be downloaded and its path configured in the notebook before execution. The original notebook uses a Kaggle dataset directory.

---

## 🧹 Data Preprocessing

Before training, the logo images undergo several preprocessing steps:

1. ✅ **Dataset Loading**
   - Load image metadata using Pandas.
   - Read image filenames, brand names, and labels from `file_mapping.csv`.
   - Inspect class distribution and brand representation.

2. ✅ **Image Loading**
   - Load images using PIL.
   - Convert images to RGB format.

3. ✅ **Image Resizing**
   - Baseline model: Resize images to **128 × 128** pixels.
   - Improved model: Resize images to **224 × 224** pixels.

4. ✅ **Tensor Conversion**
   - Convert images into PyTorch tensors.
   - Prepare labels as numerical values:
     - `0` → Fake
     - `1` → Genuine

5. ✅ **Dataset Splitting**
   - Training set → 583 images.
   - Validation set → 60 images.
   - Test set → 182 images.
   - Split images separately for each brand.

---

## 🧠 Model Training Steps

The project implements two different training approaches using ResNet18.

### 1. Baseline Model

The initial approach uses ResNet18 without pretrained weights.

**Model Configuration:**

- Architecture: `ResNet18`
- Pretrained Weights: None
- Input Resolution: `128 × 128`
- Batch Size: `16`
- Epochs: `10`
- Optimizer: `Adam`
- Learning Rate: `0.001`
- Loss Function: `CrossEntropyLoss`

**Baseline Results:**

- Test Accuracy: **79.67%**
- Test Loss: **0.4027**

The baseline model provides a starting point for evaluating the effectiveness of transfer learning.

### 2. Transfer Learning with ResNet18

To improve classification performance, a pretrained ResNet18 model is used.

The model is initialized with ImageNet pretrained weights, and its final fully connected layer is replaced with a new classification layer containing two output classes.

**Model Configuration:**

- Base Architecture: `ResNet18`
- Pretrained Weights: `IMAGENET1K_V1`
- Input Resolution: `224 × 224`
- Batch Size: `16`
- Epochs: `10`
- Optimizer: `Adam`
- Learning Rate: `0.0001`
- Loss Function: `CrossEntropyLoss`
- Framework: PyTorch

The model is trained and evaluated using separate training, validation, and test DataLoaders.

### 3. Data Augmentation

To improve generalization and introduce additional image variations, the following augmentation techniques are applied to training images:

- ✅ Random Horizontal Flip
- ✅ Random Rotation (10 degrees)
- ✅ Color Jitter (brightness, contrast, saturation, and hue adjustments)

Validation and test images are resized and converted to tensors without random augmentation.

### 4. Training Process

During training:

1. Load batches of images and labels.
2. Perform forward propagation through ResNet18.
3. Calculate classification loss using Cross Entropy Loss.
4. Perform backpropagation.
5. Update model parameters using Adam.
6. Evaluate the model on the validation dataset after each epoch.
7. Track training loss, validation loss, and validation accuracy.

---

## 📊 Model Evaluation & Results

The final model is evaluated using the held-out test dataset.

The following evaluation metrics are calculated:

- Accuracy
- Precision
- Recall
- F1-Score
- Confusion Matrix

### Final Results

<details>
<summary>📈 Classification Report</summary>

| Class | Precision | Recall | F1-Score |
|---|---:|---:|---:|
| Fake | 0.98 | 0.98 | 0.98 |
| Genuine | 0.95 | 0.97 | 0.96 |
| **Weighted Average** | **0.97** | **0.97** | **0.97** |

</details>

- 🎯 **Test Accuracy:** 97.25%
- 📉 **Test Loss:** Evaluated during final testing.
- 🧪 **Test Samples:** 182

### Performance Comparison

| Model | Test Accuracy |
|---|---:|
| ResNet18 (Training from Scratch) | 79.67% |
| ResNet18 (ImageNet Pretrained) | **97.25%** |

The results demonstrate a significant improvement in classification performance through Transfer Learning.

### 📉 Training Visualization

The notebook includes visualizations of:

- Training and validation loss curves.
- Training and validation accuracy curves.
- Confusion matrix.
- Random test image predictions with actual and predicted labels.

---

## 🖼️ Example Predictions

The notebook includes a visualization function that selects random images from the test dataset and displays their actual and predicted labels.

Each image is presented with:

- **True Label:** The actual classification (Fake or Genuine).
- **Predicted Label:** The classification produced by the trained ResNet18 model.

This visualization provides an intuitive way to inspect the model's predictions and identify potential misclassifications.

---

## 🧪 Technologies & Libraries

The project is developed using the following technologies:

- **Python** → Main programming language.
- **PyTorch** → Deep Learning framework.
- **Torchvision** → Pretrained models and image transformations.
- **ResNet18** → CNN architecture for image classification.
- **OpenCV** → Image processing.
- **PIL (Pillow)** → Image loading and manipulation.
- **NumPy** → Numerical computations.
- **Pandas** → Dataset and metadata management.
- **Matplotlib** → Data and training visualization.
- **Seaborn** → Confusion matrix visualization.
- **Scikit-learn** → Dataset splitting and model evaluation.

---

## 📁 Project Structure

```text
Fake-Real-Logo-Classification/
│
├── fake-real-logo-classification.ipynb
│
└── README.md
```

---

## 🚀 How to Run

The notebook can be executed using Kaggle or a local Jupyter environment.

1. ✅ Clone the repository:

   ```bash
   git clone https://github.com/mbsoroush/Fake-Real-Logo-Classification.git
   ```

2. ✅ Download the dataset and extract its contents.

3. ✅ Open `fake-real-logo-classification.ipynb`.

4. ✅ Configure the dataset path and ensure `file_mapping.csv` is accessible.

5. ✅ Install the required dependencies.

6. ✅ Run the notebook cells sequentially to perform preprocessing, model training, and evaluation.

---

## 🏁 Conclusion

This project demonstrates the application of Deep Learning and Computer Vision techniques to **Fake vs. Real Logo Classification**.

The main achievements include:

1. ✅ **Binary Image Classification**
   - Developed a CNN-based classification system using ResNet18.
   - Classified brand logos into Fake and Genuine categories.

2. ✅ **Transfer Learning**
   - Compared training ResNet18 from scratch with ImageNet pretrained weights.
   - Improved test accuracy from **79.67% to 97.25%**.

3. ✅ **Data Augmentation**
   - Applied image transformations to improve model generalization.

4. ✅ **Model Evaluation**
   - Evaluated the final model using accuracy, precision, recall, F1-score, and confusion matrix.
   - Visualized model performance and sample predictions.

5. 🔮 **Future Improvements**
   - Expand the dataset with more brands and logo variations.
   - Experiment with other CNN architectures and pretrained models.
   - Explore object detection approaches for identifying counterfeit logos in complex images.
   - Investigate model robustness against image distortions and different capture conditions.

---

## ⚖️ License

This project is licensed under the [Creative Commons Attribution–NonCommercial–NoDerivatives 4.0 International License (CC BY-NC-ND 4.0)](https://creativecommons.org/licenses/by-nc-nd/4.0/).

You are free to share and redistribute this work for non-commercial purposes, provided that:

- Appropriate credit is given to the original author.
- A link to the license is provided.
- Any modifications or changes are clearly indicated.
- The work is not used for commercial purposes.
- Modified versions are not distributed.
