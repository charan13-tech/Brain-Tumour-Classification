# Brain Tumor Classification using CNN

An ongoing deep learning project for classifying brain MRI images into different tumor categories using a Convolutional Neural Network (CNN).

> ⚠️ **This project is currently under development.** The repository contains the initial dataset preparation, CNN implementation, training pipeline, and evaluation workflow. Further experimentation and analysis are still planned.

---

## 🚧 Project Status

**Status: In Progress**

The current implementation establishes a CNN-based brain MRI classification pipeline. Dataset loading, image resizing, label encoding, model construction, training, and evaluation code have been implemented.

However, the project is still being developed, and further experimentation, analysis, and potential improvements are required before considering the project complete.

---

## 📌 Overview

The objective of this project is to develop a CNN-based image classification model capable of classifying brain MRI images into four categories represented in the dataset:

- **Glioma Tumor**
- **Meningioma Tumor**
- **No Tumor**
- **Pituitary Tumor**

The current notebook focuses on building and evaluating a custom CNN using the available MRI image dataset.

This project is intended as an educational and research-oriented machine learning project and should not be interpreted as a clinically validated diagnostic system.

---

## 🎯 Current Objectives

The current implementation focuses on:

- Loading the brain MRI dataset.
- Organizing images according to their class labels.
- Resizing MRI images to a fixed input size.
- Encoding class labels for neural-network training.
- Creating a train/validation split.
- Building a custom CNN architecture.
- Training the CNN model.
- Using callbacks to improve the training process.
- Evaluating the trained model on the testing dataset.
- Generating classification and confusion-matrix based evaluation.

---

## 📂 Dataset

The notebook uses the **Brain Tumor Classification MRI** dataset through Kaggle-style paths.

The dataset is organized into separate `Training` and `Testing` directories, with four class folders:

```text
Training/
├── glioma_tumor/
├── meningioma_tumor/
├── no_tumor/
└── pituitary_tumor/

Testing/
├── glioma_tumor/
├── meningioma_tumor/
├── no_tumor/
└── pituitary_tumor/
```

The images are resized to **150 × 150 pixels** before being passed to the CNN.

The input shape used by the model is:

```text
(150, 150, 3)
```

The notebook uses the training dataset for a stratified **90/10 train-validation split**.

---

## ⚙️ Current Implementation

### 1. Dataset Loading

The notebook loads images from the `Training` and `Testing` directories using OpenCV.

Each image is read and resized to:

```text
150 × 150
```

The corresponding folder name is used as the image label.

### 2. Image Preprocessing

The currently implemented preprocessing consists primarily of:

- Reading images using OpenCV.
- Resizing images to `150 × 150`.
- Converting image and label lists into NumPy arrays.
- Shuffling the training data.

The notebook does **not currently implement data augmentation or a separate image-normalization pipeline**.

### 3. Label Handling

Class labels are converted into numerical representations using `LabelEncoder`.

The encoded labels are then converted into categorical/one-hot representations using `to_categorical`.

### 4. Train/Validation Split

The training dataset is divided into:

- **90% training data**
- **10% validation data**

The split uses stratification so that the class distribution is maintained between the training and validation sets.

### 5. CNN Model

A custom CNN is constructed using Keras' `Sequential` API.

### 6. Model Training

The model is trained using the prepared training and validation datasets.

The training process includes:

- Adam optimizer
- Categorical cross-entropy loss
- Accuracy as a training metric
- Maximum of 30 epochs
- Early stopping
- Learning-rate reduction
- Best-model checkpointing

### 7. Model Evaluation

After training, the saved best model is evaluated on the testing dataset.

The notebook includes code for:

- Test loss
- Test accuracy
- Classification report
- Precision
- Recall
- F1-score
- Confusion matrix

---

## 🧠 CNN Model

The current CNN consists of multiple convolutional blocks followed by fully connected layers.

The implemented architecture is:

```text
Input: 150 × 150 × 3

Conv2D   32 filters, 3×3, ReLU
Conv2D   64 filters, 3×3, ReLU
MaxPooling2D 2×2
Dropout 0.3

Conv2D   64 filters, 3×3, ReLU
Conv2D   64 filters, 3×3, ReLU
Dropout 0.3
MaxPooling2D 2×2
Dropout 0.3

Conv2D   128 filters, 3×3, ReLU
Conv2D   128 filters, 3×3, ReLU
Conv2D   128 filters, 3×3, ReLU
MaxPooling2D 2×2
Dropout 0.3

Conv2D   128 filters, 3×3, ReLU
Conv2D   256 filters, 3×3, ReLU
MaxPooling2D 2×2
Dropout 0.3

Flatten

Dense 512, ReLU
Dense 512, ReLU
Dropout 0.3

Dense 4, Softmax
```

The model summary reports:

- **Total parameters:** 4,447,044
- **Trainable parameters:** 4,447,044

The final four-unit Softmax layer corresponds to the four classification categories.

---

## 📊 Model Training

The model is compiled with:

| Configuration | Current Setting |
|---|---|
| Optimizer | Adam |
| Loss | Categorical Cross-Entropy |
| Metric | Accuracy |
| Maximum Epochs | 30 |
| Validation | 10% stratified split |

### Training Callbacks

Three callbacks are implemented:

**EarlyStopping**

- Monitors `val_loss`
- Patience: 5 epochs
- Restores the best weights

**ReduceLROnPlateau**

- Monitors `val_loss`
- Reduction factor: `0.2`
- Patience: 3 epochs
- Minimum learning rate: `1e-6`

**ModelCheckpoint**

- Monitors `val_accuracy`
- Saves the best model
- Saved as:

```text
best_model.keras
```

---

## 📈 Evaluation

The notebook contains an evaluation pipeline using the saved best model.

The implemented evaluation includes:

- Test accuracy
- Test loss
- Precision
- Recall
- F1-score
- Classification report
- Confusion matrix

Training and validation accuracy/loss are also plotted to examine model learning behaviour across epochs.

### Current Metrics

The notebook contains code for calculating the final metrics, but reliable final numerical results are not included in the current project state.

Therefore, numerical performance results are intentionally **not reported here**.

> Final performance metrics will be added after the remaining experiments and model evaluation are completed.

---

## 🔬 Current Results

| Component | Status |
|---|---|
| Dataset loading | ✅ Completed |
| Image resizing | ✅ Completed |
| Label encoding | ✅ Completed |
| Train/validation split | ✅ Completed |
| CNN architecture | ✅ Completed |
| Model compilation | ✅ Completed |
| Model training pipeline | ✅ Implemented |
| Training/validation plots | ✅ Implemented |
| Best-model checkpointing | ✅ Implemented |
| Test evaluation code | ✅ Implemented |
| Classification report | ✅ Implemented |
| Confusion matrix | ✅ Implemented |
| Precision / Recall / F1 evaluation | ✅ Implemented |
| Final performance analysis | 🚧 Pending |
| Model improvement/tuning | 🚧 In Progress |
| Deployment | ⏳ Planned |

---

## 🚧 Work in Progress

The project is currently at the initial CNN experimentation stage.

Areas that may require further development include:

- Further model experimentation and tuning.
- Detailed analysis of validation and testing performance.
- Error analysis of incorrectly classified MRI images.
- Comparing different CNN configurations.
- Improving the overall robustness of the model.
- Organizing the final model and inference workflow.
- Preparing the project for potential deployment.

These items should **not** be considered completed features.

---

## 🔮 Future Work

Potential future improvements include:

- Data augmentation.
- Improved image preprocessing and normalization.
- Transfer learning using pretrained CNN architectures.
- Hyperparameter optimization.
- Comparison between different deep learning architectures.
- Grad-CAM or other explainability techniques.
- Validation using additional/external datasets.
- Development of an inference pipeline.
- Web or API-based deployment.

These are planned possibilities and are **not currently implemented in the notebook**.

---

## 🛠️ Technologies Used

The notebook currently uses:

- **Python**
- **TensorFlow**
- **Keras**
- **NumPy**
- **Pandas**
- **OpenCV**
- **Scikit-learn**
- **Matplotlib**
- **Seaborn**
- **Pillow**
- **tqdm**
- **ipywidgets**

---

## 🚀 How to Run

The current notebook was developed using a **Kaggle environment** and expects the dataset to be available through Kaggle-style paths.

The notebook currently references:

```text
/kaggle/input/brain-tumor-classification-mri/
```

with:

```text
Training/
Testing/
```

directories underneath it.

### Running on Kaggle

1. Open the notebook in Kaggle.
2. Add the Brain Tumor Classification MRI dataset.
3. Ensure the dataset is available at the expected Kaggle input path.
4. Run the notebook cells sequentially.
5. The best model is saved as:

```text
best_model.keras
```

### Running Outside Kaggle

The dataset paths in the notebook will need to be modified to match the local dataset location.

For example:

```python
train_path = "path/to/Training"
test_path = "path/to/Testing"
```

The current notebook does not include a separate application or deployment interface.

---

## 📁 Project Structure

The repository is currently centered around the Jupyter Notebook:

```text
brain-tumor-classification/
│
├── brain-tumour-classification.ipynb
├── README.md
└── ...
```

Additional files such as the trained model or application code can be added as the project develops.

---

## ⚠️ Limitations

- The project is still under development.
- The current implementation uses a custom CNN and has not been extensively compared with other architectures.
- The notebook currently does not implement data augmentation.
- The notebook currently does not implement a dedicated explainability method.
- The current model has not been presented as a clinically validated system.
- Performance may vary when applied to MRI images from different datasets, scanners, acquisition conditions, or populations.
- Additional experimentation and validation are required before drawing strong conclusions about model performance.

---

## ⚕️ Disclaimer

> This project is intended for educational and research purposes only. It is not a medical diagnostic tool and should not be used as a substitute for professional medical advice, diagnosis, or treatment.

---

## 👨‍💻 Author

**Author:** [Your Name]
