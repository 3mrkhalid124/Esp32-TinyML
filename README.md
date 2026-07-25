# Esp32-TinyML
How to make more value of an ESP32 by adding TinyML to it

---

## 📌 Overview
Traditional logic (`if-else`) fails when dealing with complex environment noise, variable lighting, or gesture variations. By bringing **TinyML** to the ESP32, we can perform real-time pattern recognition directly on the edge—**100% offline**.

---

## 🚀 Key Features
* **Zero Internet Required:** Entirely processed locally on the ESP32 microcontroller.
* **Smart Pattern Recognition:** Handles complex sensor signals beyond hardcoded thresholds.
* **Low Latency:** High-speed inference using quantized ML models.

---

## 🛠️ Step-by-Step Implementation

<img width="1919" height="1019" alt="Edge Impulse Overview" src="https://github.com/user-attachments/assets/b3af1c9f-cb1e-4e57-8459-3c24aaa0bfe6" />

We utilized **[Edge Impulse](https://edgeimpulse.com/)** as the core end-to-end TinyML development platform to build, train, optimize, and deploy machine learning models tailored for the ESP32.

### 🔄 TinyML Lifecycle Workflow
1. **Build (Data Acquisition):** Collecting and labeling raw sensor datasets.
2. **Train (Impulse Design):** Preprocessing signals and extracting spatial/frequency features before passing them to neural network architectures.
3. **Optimize (Quantization):** Quantizing full-precision models down to 8-bit integers (INT8) to dramatically reduce Flash and RAM footprint.
4. **Deploy (C++ / C Library):** Exporting compiled C++ libraries ready to flash directly onto the ESP32 board for offline edge execution.

---

### 🎯 Setting Up the Edge Impulse Dashboard
<img width="1919" height="1020" alt="Dashboard Setup" src="https://github.com/user-attachments/assets/69498f1b-a0b8-48cf-a680-8f23e85dfedc" />

After signing up, we initialize a new project to orchestrate the entire TinyML workflow from one place:
* 📊 **Project Dashboard:** Tracks dataset split, model status, and deployment target configurations.
* 📥 **Data Acquisition Hub:** Manages dataset collection, labeling, and training/testing split ratios.
* ⚙️ **Target Setup:** Pre-configured for microcontroller deployment with optimized memory constraints.

---

### ⚡ Building the Impulse Pipeline
<img width="1919" height="1021" alt="Impulse Pipeline" src="https://github.com/user-attachments/assets/c6e7d9f5-4a5d-4ef6-ab04-d85e16e7e6a4" />

An Impulse defines the full machine learning pipeline—from raw signals to predictions:
* 📈 **Data Dependency:** Training data must be collected and split first before configuring processing or classification blocks.
* 🛠️ **Signal Processing Block:** Preprocesses input data and extracts relevant feature representations.
* 🧠 **Learning Block:** Trains deep learning models on extracted features to recognize target patterns automatically.

---

### 📥 Data Collection & Dataset Setup
<img width="1590" height="615" alt="Data Acquisition Options" src="https://github.com/user-attachments/assets/b279e1d9-5960-4d9c-8008-e38a667cedf2" />

To train an effective model, we populate our dataset using one of the available sources:
* 📤 **Upload Data:** Import local files (CSV, JSON, WAV, or images) directly from your machine.
* 🔄 **Import from Project:** Reuse existing datasets from other Edge Impulse projects.
* ☁️ **Add Storage Bucket:** Connect cloud storage services (like AWS S3 or Google Cloud) for automated data ingestion.

---

### 📤 Uploading Dataset & Auto-Labeling
<img width="1919" height="914" alt="Data Uploading" src="https://github.com/user-attachments/assets/3bd134dd-2df7-46f8-a42e-c9a6d8599059" />

We upload raw sensor files (`normal.wave.csv`) and configure automated data pipeline settings:
* **Train/Test Split:** Automatically splits data (80% Train / 20% Test) to evaluate model performance fairly.
* **Automatic Labeling:** Infer target classes directly from uploaded filenames.
* **Upload Status:** Confirmed successful ingestion of dataset files into Edge Impulse.

---

### ⚙️ Selecting the Processing Block
<img width="1013" height="898" alt="Processing Block" src="https://github.com/user-attachments/assets/7ed04517-bc91-49a7-8fcd-f4cb079a0df6" />

In this step, we configure how raw sensor signals are handled before feeding into the neural network:
* 🎯 **Selected Block:** **Raw Data**
* 💡 **Why Raw Data?** Passes un-processed sensor values directly to the model, saving compute cycles and memory overhead on resource-constrained boards.

---

### 🧠 Selecting the Learning Block
<img width="1915" height="912" alt="Learning Block" src="https://github.com/user-attachments/assets/21b41184-ceed-48d0-95df-1937132ad7d8" />

Next, we add a learning block to construct our neural network classifier:
* 🎯 **Selected Block:** **Classification**
* 🏷️ **Output Classes:** Learns underlying features to categorize input signals into distinct target classes (e.g., `normal` vs `abnormal`).

---

### 🧬 Feature Generation
<img width="1578" height="885" alt="Feature Generation" src="https://github.com/user-attachments/assets/9923568e-1eb8-4a36-93f8-97d989fe3a3f" />

After setting up the processing block, we generate feature matrices from the dataset:
* ⚙️ **Parameters Setup:** Review training set metrics and normalization options.
* 🚀 **Generate Features:** Converts time-series or sensor windows into structured feature vectors.
* 📊 **Feature Explorer:** Displays a 3D visualization of feature clusters to verify class separability.
> 💡 **Note:** The screenshots provided in this documentation are captured from an initial demonstration/test pipeline setup to illustrate the workflow interface. For real-world production deployment, ensure adequate dataset sizing, multiple class labels, and complete feature generation before training.
---

### 🏋️ Neural Network Architecture & Model Training
<img width="1919" height="915" alt="Model Training" src="https://github.com/user-attachments/assets/71ac62c5-bcc0-4618-a04b-c8f59b7acdca" />

We design and train the deep learning classification architecture:
* 🏗️ **Network Architecture:** Fully-connected Dense layers mapping input features down to target output classes.
* ⚡ **Training Hyperparameters:** Configure learning rate, epoch count, and training processor before clicking **Save & train**.
* 📉 **Performance Metrics:** Evaluates Accuracy, Loss, Precision, Recall, and inspects the **Confusion Matrix** to validate model readiness.

---

### 📦 Exporting Model & Library Deployment
<img width="1344" height="241" alt="Library Export" src="https://github.com/user-attachments/assets/b8f5e670-452c-4282-a20b-f03985b4f3be" />

Once trained, we export the optimized Edge Impulse pipeline into a standalone MCU library:
* 📥 **Export Format:** Exported as an **Arduino ZIP Library** (`ei-test-arduino-1.0.3-impulse-#1.zip`).
* 🔌 **Hardware Integration:** Included directly into Arduino IDE via `Sketch -> Include Library -> Add .ZIP Library...`.
* ⚡ **Offline Execution:** Contains all quantized neural network weights, DSP logic, and inference kernels compiled for ESP32.

---

## 🔌 Arduino IDE Setup & Hardware Deployment

Follow these steps to flash the trained model onto your ESP32 microcontroller and run offline inference:

1. **Installing the Library:**
   * Open **Arduino IDE**.
   * Navigate to **Sketch** ➔ **Include Library** ➔ **Add .ZIP Library...**.
   * Select the downloaded Edge Impulse library `.zip` file.

2. **Configuring Board Settings:**
   * Go to **Tools** ➔ **Board** ➔ **ESP32 Arduino** ➔ Select **ESP32 Dev Module**.
   * Connect your ESP32 board via USB.
   * Select the correct port via **Tools** ➔ **Port**.

3. **Loading & Flashing the Code:**
   * Go to **File** ➔ **Examples** ➔ Scroll down to your library name.
   * Select the **`static_buffer`** example (or board-specific example).
   * Click **Upload** to compile and flash the firmware.

4. **Verifying Offline Inference:**
   * Open **Serial Monitor** (**Tools** ➔ **Serial Monitor**).
   * Set baud rate to **`115200`**.
   * View real-time predictions, classification confidence scores, and inference latency **100% offline**! 🚀

---

## 📊 Traditional Logic vs. TinyML

| Feature | Traditional Logic (`if-else`) | TinyML on ESP32 |
| :--- | :--- | :--- |
| **Adaptability** | Rigid hardcoded thresholds | Learns complex, non-linear patterns |
| **Noise Tolerance** | Fails in noisy environments | Robust feature extraction & filtering |
| **Connectivity** | Local | 100% Offline (No Cloud needed) |
| **Latency** | Instant | Low Latency (~10-50ms inference) |

<img width="768" height="1376" alt="Comparison Diagram" src="https://github.com/user-attachments/assets/fb4f8ac2-2c9a-4ede-90bc-3e79f2f24a7b" />

---

## 🔗 Connect with Me
📫 Let's connect on [LinkedIn](https://www.linkedin.com/in/amr-khalid-a88398424)
