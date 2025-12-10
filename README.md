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

## 🚀 Objective

Build a deep-learning pipeline that:

* Takes a **cloudy Sentinel-2 tile**
* Uses the SCL mask for supervision
* **Reconstructs the hidden land surface**
* Outputs a **clean, usable multi-band patch**

---

## 🤖 Model Architectures

Two reconstruction models were developed:

### 1️⃣ CNN Encoder–Decoder (Baseline)

A simple encoder–decoder architecture that:

* Encodes cloudy input
* Learns a latent representation
* Decodes to reconstruct missing surface information

This validated the **feasibility** of cloud reconstruction using DL.

#### Training Details (CNN)

* Optimizer: **Adam**, lr=5e-5
* Batch size: 4
* Epochs: 10
* Device: GPU if available
* Data augmentation: random horizontal/vertical flips
* Loss: **Cloud-only MSE**, computed only on cloud pixels
* Gradient clipping: max norm 1.0

```python
loss = cloud_only_mse(prediction, target, cloud_mask)
```

Model checkpoint: `simple_cnn_cloud.pth`

### CNN Encoder–Decoder Training Results

* Initial Loss: 0.0317
* Final Loss: 0.002138
* Observation: Rapid convergence within first few epochs, low final masked MSE, demonstrates effective reconstruction of clouded regions.

---

### 2️⃣ U-Net (Improved Model)

A U-Net with skip connections for richer spatial detail:

* Multi-scale feature extraction
* Better texture and boundary preservation
* Takes **cloudy input + SCL mask**

Produces a **clean, reconstructed multi-band patch**.

#### Training Details (U-Net)

* Optimizer: **Adam**, lr=5e-5
* Batch size: 4
* Epochs: 20
* Device: GPU if available
* Data augmentation: random horizontal/vertical flips
* Loss: **Masked MSE**, focuses on cloud pixels
* Gradient clipping: max norm 1.0

```python
loss = masked_mse(prediction, target, mask)
```

Model checkpoint: `unet_cloud.pth`

### U-Net Training Results

* Initial Loss: 0.0873
* Final Loss: 0.003369
* Observation: Rapid convergence in early epochs, stable low masked MSE, successfully reconstructs cloud-covered regions.

Both models are **working prototypes**, not production-ready, but strong proofs of concept.

---

## ⭐ Results

The models successfully reconstructed surface information hidden by clouds and cleaned cloud-occluded regions:

* **CNN Encoder–Decoder:** final masked MSE ~0.0021
* **U-Net:** final masked MSE ~0.0034

Both models demonstrate that deep learning can effectively recover information obscured by clouds, providing more reliable satellite data.

---

## 🌍 Applicability Across Domains

Although developed in an **AgriTech** context, cloud reconstruction benefits:

* Agriculture (NDVI, crop monitoring)
* Water resource analysis
* Forestry and land-cover monitoring
* Urban development and planning
* Disaster management (flood/landslide assessment)

---

## 📁 Project Structure

```
├── cnn_improved.ipynb
├── unet.ipynb
└── README.md
```

---

## 🔧 Tech Stack

* Python
* PyTorch
* Rasterio
* NumPy / OpenCV
* Sentinel-2 Multi-Spectral Imagery (13-band)

---

## 📌 Future Work

* Add temporal cloud-free reference tiles
* Introduce super-resolution for sharper outputs
* Deploy as an API / microservice
* Add quality evaluation metrics (PSNR, SSIM)

---

## 🙌 Acknowledgment

This project was built during an evaluation task for an **AgriTech startup**, and represents my first real-world experience working with **raw satellite imagery**.
