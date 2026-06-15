# 🛡️ Cyber Attack Detection System

An intelligent, machine-learning-based system designed to **detect and classify cyber attacks within network traffic**. This project analyzes various network connection metrics to accurately distinguish malicious activities from normal network traffic.

---

## 🎯 Key Features
- **Exploratory Data Analysis (EDA):** Comprehensive statistical analysis and visualization of network traffic characteristics.
- **Feature Engineering:** Extraction of high-impact features from raw packet data to boost model performance.
- **Advanced Normalization:** Logarithmic transformation applied to handle highly skewed network data distributions.
- **Imbalanced Data Management:** Implementation of **SMOTE** to oversample minority attack classes, preventing model bias.
- **High-Performance Detection:** Leverages ensemble learning to achieve an impressive accuracy rate exceeding 84%.

---

## 📊 Dataset Source & Summary
The project utilizes the **Cyber Attack Detection Using Network Traffic** dataset, which is publicly available on Kaggle.

🔗 **Dataset Link:** [Kaggle - Cyber Attack Detection Using Network Traffic](https://www.kaggle.com/datasets/juanschafle/cyber-attack-detection-using-network-traffic)

The dataset contains **100,000 network connection records** with the following key attributes:
- `duration`: The length of the network connection.
- `src_bytes` & `dst_bytes`: The volume of data sent and received.
- `packet_count`: The total number of packets exchanged.
- `protocol`: The network protocol used (e.g., TCP, UDP).
- `failed_logins`: The number of unsuccessful login attempts.
- `attack_type`: The target classification label (including **DDoS**, **PortScan**, **BruteForce**, and **Normal** traffic).

---

## 🛠️ Data Pipeline & Preprocessing

### 1. Feature Engineering
To improve the model's predictive power, three new domain-specific features were engineered:
- **Data Transfer Ratio:** `Data_transfer_ratio = src_bytes / dst_bytes`
- **Bytes Per Second:** `bytes_per_second = (src_bytes + dst_bytes) / (duration + 1)`
- **Login Success Rate:** `login_success_rate = failed_logins / packet_count`

### 2. Handling Skewness
Network traffic volumes often exhibit heavily skewed distributions. A **Log Transformation (`np.log1p`)** was applied to continuous numerical features to stabilize variance and normalize the distribution.

### 3. Categorical Encoding
- The categorical target variable (`attack_type`) was mapped using `LabelEncoder`.
- The network protocols were converted into distinct numerical identifiers using **One-Hot Encoding (`pd.get_dummies`)**.

### 4. Class Balancing (SMOTE)
Since certain cyber attacks occur less frequently than normal behavior, **SMOTE (Synthetic Minority Over-sampling Technique)** was deployed to balance the dataset classes, ensuring fair representation during training.

---

## 🤖 Modeling & Evaluation

A **Random Forest Classifier** was selected as the final production model after benchmarking multiple algorithms. The dataset was split into an 80/20 train-test ratio.

### 📈 Model Performance Metrics
The model delivered excellent results on the unseen testing set:

| Metric | Score |
| :--- | :--- |
| **Accuracy** | **84.16%** |
| **Precision** | **84.18%** |
| **Recall** | **84.16%** |
| **F1-Score** | **84.15%** |

---

## 🚀 Installation & Usage

### Prerequisites
Ensure you have Python installed. You can install all the required dependencies using pip:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn imbalanced-learn
