# 🧵 Textile Guard – Textile Pattern Defect Detection System

<div align="center">

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?style=for-the-badge&logo=python)
![Flask](https://img.shields.io/badge/Flask-2.x-black?style=for-the-badge&logo=flask)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange?style=for-the-badge&logo=tensorflow)
![OpenCV](https://img.shields.io/badge/OpenCV-4.x-green?style=for-the-badge&logo=opencv)
![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)

*An intelligent machine learning system for automated textile fabric defect detection.*

</div>

---

## 📖 Project Overview

**Textile Guard** is a machine learning–powered web application designed to detect defects in textile patterns using computer vision. The system allows textile manufacturers to upload fabric images and automatically identifies pattern irregularities, weaving defects, and quality anomalies — replacing slow, error-prone manual inspection with fast and reliable automated analysis.

By leveraging deep learning models trained on real-world fabric imagery, Textile Guard helps quality control teams catch defects earlier in the production pipeline, reducing waste, lowering costs, and improving product consistency.

---

## ✨ Features

- 🔍 **Automatic Defect Detection** – Detects common textile defects such as holes, stains, broken threads, and pattern misalignments
- 🖼️ **Image Upload Interface** – Simple web UI for uploading fabric images directly from a browser
- ⚡ **Real-Time Analysis** – Fast inference powered by optimized deep learning models
- 📊 **Confidence Scoring** – Each prediction includes a confidence score for reliability assessment
- 🗂️ **Defect Classification** – Classifies the type of defect detected, not just its presence
- 📁 **Batch Processing** – Supports analysis of multiple images in a single session
- 📈 **Result Visualization** – Annotated output images with highlighted defect regions
- 🌐 **Web-Based Access** – Accessible from any device via a modern browser with no installation required on the client side

---

## 🎥 Demo / Screenshots

> **Note:** Replace the placeholder paths below with actual screenshots once the application is running.

### 🏠 Home / Upload Page
```
[ Screenshot: Web interface showing the image upload panel ]
```

### 🔎 Detection Result Page
```
[ Screenshot: Annotated fabric image with defect regions highlighted ]
```

### 📊 Prediction Dashboard
```
[ Screenshot: Confidence score and defect classification summary ]
```

*To run a live demo locally, follow the [Installation Guide](#️-installation-guide) below.*

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────┐
│                        User Browser                      │
│              (HTML / CSS / JavaScript UI)                │
└───────────────────────┬─────────────────────────────────┘
                        │  HTTP Request (image upload)
                        ▼
┌─────────────────────────────────────────────────────────┐
│                    Flask Web Server                      │
│          • Route handling & request processing           │
│          • Image pre-processing (OpenCV)                 │
│          • Model inference (TensorFlow / PyTorch)        │
│          • Result formatting & response                  │
└───────────────────────┬─────────────────────────────────┘
                        │
          ┌─────────────┴──────────────┐
          ▼                            ▼
┌─────────────────┐        ┌──────────────────────┐
│   ML Model      │        │   Image Storage       │
│ (Saved weights  │        │ (Uploaded & processed │
│  .h5 / .pt)     │        │  fabric images)       │
└─────────────────┘        └──────────────────────┘
```

**Workflow:**
1. User uploads a fabric image via the web interface
2. Flask backend receives the image and passes it through pre-processing (resizing, normalization) using OpenCV
3. The pre-processed image is fed into the trained ML model
4. The model returns a defect classification with a confidence score
5. The annotated result image and report are returned to the browser

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | HTML5, CSS3, JavaScript (ES6+) |
| **Backend** | Python 3.9+, Flask 2.x |
| **Machine Learning** | TensorFlow 2.x / PyTorch, Keras |
| **Computer Vision** | OpenCV 4.x |
| **Dataset** | Textile fabric pattern images (custom / TILDA / public datasets) |
| **Development Tools** | VS Code, GitHub, Jupyter Notebook |
| **Deployment** | Flask development server / Gunicorn (production) |

---

## ⚙️ Installation Guide

### Prerequisites

Ensure you have the following installed on your system:
- Python 3.9 or higher
- pip (Python package manager)
- Git

### Step 1 – Clone the Repository

```bash
git clone https://github.com/Krishna201i/Textile-Guard.git
cd Textile-Guard
```

### Step 2 – Create a Virtual Environment

```bash
# Create virtual environment
python -m venv venv

# Activate on Windows
venv\Scripts\activate

# Activate on macOS / Linux
source venv/bin/activate
```

### Step 3 – Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4 – Download or Place the Trained Model

Place your trained model file (e.g., `model.h5` or `model.pt`) in the `model/` directory:

```
Textile-Guard/
└── model/
    └── textile_defect_model.h5
```

> If no pre-trained model is available, follow the [Model Training](#-model-training-explanation) section to train from scratch.

### Step 5 – Run the Application

```bash
python app.py
```

### Step 6 – Open in Browser

```
http://127.0.0.1:5000
```

---

## 🚀 Usage Instructions

1. **Launch the app** using `python app.py` and open `http://127.0.0.1:5000` in your browser
2. **Click "Upload Image"** on the home page and select a fabric image (`.jpg`, `.jpeg`, or `.png`)
3. **Click "Analyze"** to submit the image for defect detection
4. **View the results** — the system displays:
   - The uploaded image with annotated defect regions
   - The predicted defect type (e.g., *hole*, *stain*, *broken thread*, *good*)
   - A confidence score (e.g., *95.3% confidence*)
5. **Download the report** (if available) or upload another image for further analysis

---

## 📦 Dataset Information

The model is trained on textile fabric images containing various defect categories. Supported datasets include:

| Dataset | Description |
|---|---|
| **TILDA Textile Dataset** | Benchmark dataset with labeled fabric defects |
| **Custom Dataset** | Fabric images collected from real manufacturing environments |
| **Augmented Data** | Artificially augmented images (rotation, flipping, brightness) |

### Dataset Directory Structure

```
dataset/
├── train/
│   ├── defective/
│   └── non_defective/
├── validation/
│   ├── defective/
│   └── non_defective/
└── test/
    ├── defective/
    └── non_defective/
```

> **Note:** Due to licensing or size constraints, the dataset is not included in this repository. Please refer to the dataset sources or contact the author to obtain the data.

---

## 🤖 Model Training Explanation

The defect detection model is a Convolutional Neural Network (CNN) trained using transfer learning.

### Training Pipeline

1. **Data Preprocessing**
   - Images resized to `224x224` pixels
   - Pixel values normalized to `[0, 1]`
   - Data augmentation applied (random flip, rotation, zoom)

2. **Model Architecture**
   - Base model: `MobileNetV2` / `ResNet50` (pre-trained on ImageNet)
   - Custom classification head: `GlobalAveragePooling → Dense(256, ReLU) → Dropout(0.5) → Dense(N, Softmax)`
   - Fine-tuned on the textile defect dataset

3. **Training Configuration**
   - Optimizer: `Adam` (learning rate: `0.0001`)
   - Loss function: `Categorical Crossentropy`
   - Metrics: `Accuracy`, `Precision`, `Recall`
   - Early stopping and learning rate scheduling applied

4. **To Train the Model**

```bash
python train.py --epochs 50 --batch_size 32 --data_dir dataset/
```

5. **Model saved to:**

```bash
model/textile_defect_model.h5
```

---

## 📁 Folder Structure

```
Textile-Guard/
│
├── static/
│   ├── css/
│   │   └── style.css          # Application styles
│   ├── js/
│   │   └── main.js            # Frontend JavaScript
│   └── uploads/               # Uploaded fabric images
│
├── templates/
│   ├── index.html             # Home / upload page
│   └── result.html            # Detection results page
│
├── model/
│   └── textile_defect_model.h5  # Trained ML model weights
│
├── dataset/                   # Training / validation / test images
│
├── app.py                     # Flask application entry point
├── train.py                   # Model training script
├── predict.py                 # Inference / prediction logic
├── preprocess.py              # Image pre-processing utilities
├── requirements.txt           # Python dependencies
├── README.md                  # Project documentation
└── LICENSE                    # License file
```

---

## 🔮 Future Improvements

- [ ] 🌐 **Cloud Deployment** – Deploy on AWS / GCP / Azure with auto-scaling
- [ ] 📱 **Mobile App** – Build a companion mobile application for on-floor inspection
- [ ] 🎯 **Object Detection** – Upgrade from classification to pixel-level defect localization using YOLO or Mask R-CNN
- [ ] 📊 **Analytics Dashboard** – Add historical trend analysis and defect frequency reporting
- [ ] 🔗 **API Integration** – Expose a REST API for integration with existing factory ERP/MES systems
- [ ] 🤖 **AutoML Pipeline** – Automate retraining when new labeled data is available
- [ ] 🌍 **Multi-language UI** – Support for multiple languages for global deployment
- [ ] 🔒 **User Authentication** – Role-based access control for enterprise use

---

## 🤝 Contributing Guidelines

Contributions are welcome and appreciated! To contribute:

1. **Fork** the repository
2. **Create** a new branch for your feature or fix:
   ```bash
   git checkout -b feature/your-feature-name
   ```
3. **Make** your changes and write clear, concise commit messages
4. **Test** your changes thoroughly before submitting
5. **Push** your branch:
   ```bash
   git push origin feature/your-feature-name
   ```
6. **Open a Pull Request** with a clear description of the changes and the problem they solve

### Code of Conduct
Please be respectful and constructive in all interactions. This project follows the [Contributor Covenant Code of Conduct](https://www.contributor-covenant.org/).

---

## 📄 License

This project is licensed under the **MIT License**.

```
MIT License

Copyright (c) 2024 Krishna201i

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
```

See the [LICENSE](LICENSE) file for full details.

---

## 👨‍💻 Author

<div align="center">

**Krishna201i**

[![GitHub](https://img.shields.io/badge/GitHub-Krishna201i-black?style=for-the-badge&logo=github)](https://github.com/Krishna201i)

*"Building intelligent systems to solve real-world manufacturing challenges."*

---

⭐ **If you found this project helpful, please consider giving it a star!** ⭐

</div>
