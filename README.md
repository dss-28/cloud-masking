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

### 2️⃣ U-Net (Improved Model)

A U-Net with skip connections for richer spatial detail:

* Multi-scale feature extraction
* Better texture and boundary preservation
* Takes **cloudy input + SCL mask**

Produces a **clean, reconstructed multi-band patch**.

Both models are **working prototypes**, not production-ready, but strong proofs of concept.

---

## ⭐ Results

The prototypes successfully:

* Reconstructed surface information hidden by clouds
* Cleaned cloud-occluded regions
* Produced more stable NDVI and vegetation indicators (useful for agri)
* Generated more reliable inputs for any satellite-based analysis

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
├── data/
│   ├── raw_tiles/
│   └── scl_masks/
├── models/
│   ├── cnn_encoder_decoder.py
│   └── unet_reconstruction.py
├── notebooks/
│   └── exploration.ipynb
├── utils/
│   └── preprocessing.py
├── train.py
├── inference.py
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

---

If you want, I can add badges, installation instructions, visuals, or pipeline diagrams.
