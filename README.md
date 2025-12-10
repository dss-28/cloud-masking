Got it.
Here is **your exact README — unchanged — only the data section rewritten to be short**, exactly as you asked earlier.

I did **not** modify anything else. Only shortened the *Data Source, Downloading & Preprocessing* block while keeping placement and formatting identical.

---

# 🛰️ Cloud Reconstruction from Sentinel-2 Imagery

A deep-learning based **cloud removal and surface reconstruction** project built from **raw Sentinel-2 satellite data**, developed as part of an evaluation task for an AgriTech startup.

Cloud cover affects **all satellite-based domains** — agriculture, water, forestry, climate, and urban analytics. This project goes beyond simply detecting clouds and focuses on **reconstructing the hidden ground surface**.

---

## 🌥️ Problem Statement

Satellite imagery often suffers from heavy cloud cover. While Sentinel-2 provides a **Scene Classification Layer (SCL)** that marks:

* Cloud
* Cloud Shadow
* Snow

…it only **identifies** these regions.

### ❌ SCL does *not* reconstruct what lies beneath the clouds.

### ✔ This project builds models that actually **generate cloud-free imagery**.

---

# 📥 Data Source, Downloading & Preprocessing

This project uses **Sentinel-2 L2A imagery** from the **Microsoft Planetary Computer STAC API** (`pystac_client`).

To keep the workflow lightweight and Colab-friendly, two small datasets were collected:

### **1️⃣ Cloud-Free Dataset (5 tiles)**

`eo:cloud_cover < 20`, Jan 2023, same AOI.

### **2️⃣ Cloudy Dataset (5 tiles)**

`eo:cloud_cover > 20`, same time & AOI.

Downloads were intentionally capped using:

```python
items[:5]
```

because full Sentinel-2 tiles (~10k×10k px) are too large for Colab without downscaling.

---

## 🗜️ Downscaling & Patching

Since full tiles are inefficient to process:

* Tiles were **downscaled** to manageable resolution
* Then **patched into small 256×256 crops**

Both cloudy and clear tiles were patched and used for model training.

---

## 🗂️ Dataset Packaging

All imagery is stored as **GeoTIFF (TIF)**.

Final exports include:

### **📦 `sentinel2_raw_tifs.zip`**

* 5 clear tiles
* Downscaled versions
* Patch folders

### **📦 `sentinel2_cloudy_tifs.zip`**

* 5 cloudy tiles
* SCL masks
* Downscaled & patched versions

---

## 📊 Data Source & Preprocessing (Existing Summary)

* **Data Source:** Planetary Computer Sentinel-2 stack
* **Preprocessing:**

  * Downscaled tiles
  * Split into patches
  * SCL-based cloud masking

---

## 🚀 Objective

Build a deep-learning pipeline that:

* Takes a **cloudy Sentinel-2 tile patch**
* Uses the SCL mask for supervision
* **Reconstructs the hidden land surface**
* Outputs a **clean, usable multi-band patch**

---

## 🤖 Model Architectures

### 1️⃣ CNN Encoder–Decoder (Baseline)

* Encodes cloudy input → latent vector → reconstructs surface

**Training Details**

* Adam (5e-5)
* 10 epochs
* Cloud-only MSE
* Batch size: 4
* Clipping: 1.0

**CNN Training Results**

```
Initial Loss: 0.0317
Final Loss:   0.002138
```

---

### 2️⃣ U-Net (Improved Model)

* Skip connections preserve spatial detail
* Multi-scale feature extraction

**Training Details**

* Adam (5e-5)
* 20 epochs
* Masked MSE
* Batch size: 4

**U-Net Training Results**

```
Initial Loss: 0.0873
Final Loss:   0.003369
```

---

## ⭐ Results

Both models successfully reconstructed cloud-covered regions:

* **CNN Encoder–Decoder:** ~0.0021 masked MSE
* **U-Net:** ~0.0034 masked MSE

---

## 🌍 Applicability Across Domains

Cloud reconstruction is beneficial for:

* Agriculture (NDVI, crop monitoring)
* Water resource analysis
* Forestry
* Urban development
* Disaster management

---

## 📁 Project Structure

```
├── cnn.ipynb
├── unet.ipynb
└── README.md
```

---

## 🔧 Tech Stack

* Python
* PyTorch
* Rasterio
* NumPy / OpenCV
* Sentinel-2 Multispectral Imagery

---

## 📌 Future Work

* Temporal cloud-free reference tiles
* Super-resolution
* API deployment
* PSNR/SSIM evaluation

---

## 🙌 Acknowledgment

This project was built during an evaluation task for an **AgriTech startup**, and represents my first real-world experience working with **raw satellite imagery**.

---

If you want, I can now generate a **perfect GitHub-style README with badges + diagrams + TOC**.
