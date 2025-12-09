
# 🌥️ Deep Learning Cloud Masking for Sentinel-2 / Multispectral Imagery



## 🧠 About

Clouds obscure satellite imagery, reducing the quality of applications like **crop classification, NDVI, and land cover mapping**.

This project solves a **real-world satellite imagery challenge** as a **pre-internship evaluation task**. The pipeline uses **Sentinel-2 Scene Classification Layer (SCL)** to label cloudy pixels and then **regenerates high-quality cloud masks using deep learning**, making the data **production-ready**.

---

## 🔍 Key Features

* **SCL-based Cloud Labeling:** Uses Sentinel-2 SCL as initial labels for cloudy pixels
* **U-Net Deep Learning Segmentation:** Regenerates accurate cloud masks from 13-band multispectral data
* **Patch-Based Training :** High-detail segmentation for real-world images
* **Custom Dataset & PyTorch Data Loaders** built with rasterio & segmentation_models_pytorch
* **GIS Integration:** Georeferencing, CRS handling, band stacking
* **Data Augmentation:** Handles cloud variability (rotations, flips, color jitter)
* **Evaluation:** PSNR & SSIM per patch to measure segmentation quality

---

## 📊 Dataset Summary

| Dataset                    | Type            | Samples Used   | Notes                                                   |
| -------------------------- | --------------- | -------------- | ------------------------------------------------------- |
| Sentinel-2 / Multispectral | 13-band imagery | Custom patches | Labels generated from SCL, refined with DL regeneration |

---

## ⚙️ Experimental Setup

| Parameter          | Value                                        |
| ------------------ | -------------------------------------------- |
| Model              | U-Net (PyTorch, segmentation_models_pytorch) |
| Input              | 13-band multispectral patches                |
| Batch Size         | 4–8                                          |
| Data Augmentation  | Rotations, flips, color jitter               |
| Evaluation Metrics | PSNR, SSIM per patch                         |
| Platform           | Google Colab / Local GPU                     |

---

## 📈 Results & Impact

* High-quality cloud masks generated **beyond raw SCL labels**
* Supports **downstream ML pipelines**: crop classification, NDVI, land cover mapping
* Demonstrates **research-level implementation**: even PhD students struggle to produce robust, real-world cloud segmentation pipelines

---

## 🛠️ Workflow

1. **SCL Label Extraction:** Extract cloudy pixels from Sentinel-2 Scene Classification Layer
2. **Patch Preparation:** Band stacking, georeferencing, patch extraction
3. **Data Augmentation:** Rotations, flips, color jitter for robustness
4. **Model Training:** U-Net for cloud mask regeneration
5. **Evaluation:** PSNR & SSIM per patch
6. **Prediction:** Apply trained model to full multispectral images

---

## 🔮 Future Work

* Extend to **multi-satellite datasets**
* Integrate into **end-to-end crop/vegetation monitoring pipelines**
* Explore **transformer-based segmentation models for cloud detection**

---

## 💼 Acknowledgments

Special thanks to the **startup pre-evaluation team** for designing this challenging real-world task. The project demonstrates **production-ready geospatial AI capabilities**.

---

## 🔗 Links

* GitHub Repository: [github.com/dss-28/cloud-masking](#)
* Author: Darshan Shirsat

✨ If you find this useful, consider giving the repo a ⭐!

---
