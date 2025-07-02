# Sensor-Level Fusion for Secure Biometric Authentication using Cancelable Templates

![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Python Version](https://img.shields.io/badge/python-3.10+-blue)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

This project implements a robust and secure biometric authentication system using **cancelable biometric templates** on the **IITD (Indian Institute of Technology Delhi) touchless irisprint database**. The core idea is to transform raw biometric data into a non-reversible, revocable format, ensuring user privacy and enhancing security against data breaches.

## 📜 Table of Contents
- [The Problem with Traditional Biometrics](#-the-problem-with-traditional-biometrics)
- [Our Solution: Cancelable Biometrics](#-our-solution-cancelable-biometrics)
- [How It Works](#-how-it-works)
- [Key Features](#-key-features)
- [🛠️ Technology Stack](#️-technology-stack)
- [🚀 Setup and Installation](#-setup-and-installation)
- [📈 Performance & Results](#-performance--results)
- [🤝 Contributing](#-contributing)
- [📄 License](#-license)

## 🤔 The Problem with Traditional Biometrics

Traditional biometric systems store a user's raw or partially processed data (like fingerprint minutiae or an iris scan). This poses significant security risks:
-   **Irrevocable:** If this data is stolen, it's compromised forever. A user cannot simply "change" their fingerprint.
-   **Privacy Concerns:** Direct storage of personal biometric data is a major privacy violation.
-   **Cross-Contamination:** A breach in one system could compromise all other systems where the user has enrolled the same biometric data.

## 💡 Our Solution: Cancelable Biometrics

This project solves these problems by creating **cancelable biometric templates**. Instead of storing the user's actual biometric data, we store a mathematically **distorted version** of it.

> The transformation is a **one-way process**. It is computationally infeasible to reconstruct the original biometric data from the stored template. If a template is ever compromised, it can be "canceled," and a new template can be generated for the same user by simply issuing a new secret key.

## ⚙️ How It Works

The workflow is designed for maximum security and privacy:

1.  **Feature Extraction:** The process begins with pre-extracted features from the IITD irisprint dataset.
2.  **Secure Key Generation:** For each user, a unique and strong digital key is generated using cryptographic hashing (SHA256). This key acts as a secret password.
3.  **Orthogonal Matrix Transformation:** The secret key is used as a seed to generate a unique **orthogonal matrix** via the Gram-Schmidt process. This matrix serves as the user's personal transformation function.
4.  **Cancelable Template Creation:** The user's raw biometric feature vector is multiplied by their unique orthogonal matrix. The result is the **cancelable template**, which is the only piece of data stored in the database.
5.  **Model Training:** A Deep Neural Network (DNN) is trained to recognize users based on these secure templates.
6.  **Authentication:** When a user logs in, their live biometric data is captured, transformed with their secret key, and the resulting template is fed to the DNN for verification.

## ✨ Key Features

-   **Enhanced Security:** The system never stores raw biometric data, protecting it from direct theft.
-   **Privacy Preservation:** The one-way transformation ensures a user's biological identity cannot be reverse-engineered.
-   **Revocability:** If a database of templates is breached, they can all be rendered useless by issuing new keys to users.
-   **High Performance:** The trained model achieves outstanding accuracy, demonstrating that top-tier security does not have to compromise performance.

## 🛠️ Technology Stack

-   **Python 3.10+**
-   **TensorFlow & Keras**: For building and training the deep learning model.
-   **Scikit-learn**: For K-Fold cross-validation and performance metrics.
-   **NumPy**: For numerical operations and matrix manipulations.
-   **Matplotlib**: For plotting results and visualizations.
-   **Pickle**: For data serialization and loading.

## 🚀 Setup and Installation

Follow these steps to get the project running on your local machine.

1.  **Clone the Repository**
    ```bash
    git clone https://github.com/your-username/your-repo-name.git
    cd your-repo-name
    ```

2.  **Create and Activate a Virtual Environment**
    ```bash
    # For macOS/Linux
    python3 -m venv venv
    source venv/bin/activate

    # For Windows
    python -m venv venv
    venv\Scripts\activate
    ```

3.  **Install Dependencies**
    ```bash
    pip install -r requirements.txt
    ```
    *(Note: You will need to create a `requirements.txt` file containing the necessary libraries like `tensorflow`, `numpy`, `scikit-learn`, etc.)*

4.  **Prepare the Data**
    -   Download the `Feature.zip` file containing the pre-extracted biometric features.
    -   Place it in the root directory of the project.
    -   Unzip the file:
        ```bash
        unzip Feature.zip -d .
        ```

5.  **Run the Main Script**
    ```bash
    python your_main_script.py
    ```

## 📈 Performance & Results

The system's performance was rigorously evaluated and yielded excellent results:

-   **Validation Accuracy:** The model achieved an accuracy of **99.7%** on the validation set.
-   **Equal Error Rate (EER):** The system reached an EER of approximately **0.00487%**. This extremely low value signifies a near-perfect balance between security (low False Acceptance Rate) and convenience (low False Rejection Rate).
-   **K-Fold Cross-Validation:** The model's robustness was confirmed with 5-fold cross-validation, maintaining an average accuracy of **~99.8%** across all folds.

### Visualizations

**Model Accuracy & Loss**
The training history shows a stable and fast convergence, with validation accuracy closely tracking the training accuracy.
![Model Accuracy and Loss](https://github.com/Adarsh-365/Bio-metric-project/blob/main/index_files/figure-html/cell-13-output-2.png)

**FAR, FRR, and EER**
The plot of False Acceptance Rate (FAR) and False Rejection Rate (FRR) shows a clear intersection point, defining the Equal Error Rate.
![FAR and FRR vs Threshold](https://github.com/Adarsh-365/Bio-metric-project/blob/main/index_files/figure-html/cell-14-output-2.png)



## 📄 License

This project is licensed under the MIT License. See the `LICENSE` file for more details.

---
