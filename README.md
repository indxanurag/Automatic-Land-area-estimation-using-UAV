# Automated Land Area Estimation 🛰️🤖
### Using UAV Imagery & Deep Learning

> Fast, accurate, automated land classification — no expensive surveyors needed.

<p align="center">
  <img src="images/project_main.jpg" alt="UAV Land Area Estimation" width="700"/>
  <br/>
  <em>UAV imagery segmented into land types using U-Net + ResNet34</em>
</p>

---

## 📌 Overview

This is a **college minor project** that builds an end-to-end AI pipeline for automated land area estimation using drone/satellite imagery and deep learning. A **U-Net model with ResNet34 backbone** performs semantic segmentation on aerial images, classifying each pixel into one of 7 land types, and then calculates the real-world area of each land type in **m² or hectares**.

The goal: replace slow, expensive, error-prone manual surveying with a fast, automated system that works on any terrain.

---

## 🔥 The Problem

| Old / Manual Methods 😓 | What We Need ✅ |
|---|---|
| Surveyors walk with GPS over the land | Fast — done in minutes, not days |
| Takes many days for a large field | Works on any terrain |
| Needs expensive expert surveyors | No costly experts required |
| Hard to measure mountains or flooded land | Accurate and reliable |
| Prone to human errors | Fully automated |

---

## 💡 How It Works

<p align="center">
  <img src="images/pipeline.jpg" alt="System Pipeline" width="700"/>
  <br/>
  <em>3-step pipeline: Drone → AI Segmentation → Area Calculation</em>
</p>

**Step 1 — 🚁 Drone Takes Photos**
A UAV flies over the land and captures aerial images from above.

**Step 2 — 🤖 AI Reads the Photos**
The deep learning model (U-Net) reads each image and segments it — colouring different regions by land type (agriculture, forest, water, etc.).

**Step 3 — 📐 System Calculates Area**
Pixel counts per land type are converted to real-world area using the Ground Sampling Distance (GSD).

```
Area = Number of pixels × (0.5 m)²
```
> 1 pixel = 0.5m × 0.5m in real life (GSD = 0.5 m/pixel)

---

## 🗂️ Dataset — DeepGlobe

<p align="center">
  <img src="images/dataset_sample.jpg" alt="DeepGlobe Dataset Sample" width="650"/>
  <br/>
  <em>Sample DeepGlobe image (left) and its segmentation mask (right)</em>
</p>

- **~65,000** image patches of 256×256 pixels from satellite imagery worldwide
- **7 land types** labelled per pixel:

| Label | Land Type |
|---|---|
| 🟦 | Urban Land |
| 🟨 | Agriculture |
| 🟪 | Rangeland |
| 🟩 | Forest |
| 🔵 | Water |
| ⬜ | Barren Land |
| ⬛ | Unknown |

- **Split:** 80% Training / 20% Validation

---

## 🧠 Model — U-Net + ResNet34

<p align="center">
  <img src="images/unet_architecture.jpg" alt="U-Net Architecture" width="650"/>
  <br/>
  <em>U-Net encoder-decoder architecture with ResNet34 backbone</em>
</p>

| Setting | Value |
|---|---|
| Architecture | U-Net |
| Backbone | ResNet34 (pre-trained on ImageNet) |
| Epochs | 30 |
| Batch Size | 32 |
| Loss Function | BCE + Dice Loss |
| Training Platform | Google Colab (free GPU) |

---

## 📊 Results

<p align="center">
  <img src="images/results.jpg" alt="Segmentation Results" width="700"/>
  <br/>
  <em>Model output — predicted segmentation masks on test images</em>
</p>

### Overall Performance

| Metric | Score |
|---|---|
| 📐 Mean IoU | **81%** |
| 🎯 Mean Dice Score | **89%** |
| 🏆 Best Class (Water) | **91% IoU** |

### Per-Class Accuracy

| Land Type | IoU Score | Dice Score | Verdict |
|---|---|---|---|
| Agriculture | 89% | 94% | ✅ Very Good |
| Water | 91% | 95% | ✅ Excellent |
| Forest | 87% | 93% | ✅ Very Good |
| Urban Land | 83% | 91% | ✅ Good |
| Unknown | 61% | 76% | ⚠️ Needs Work |

### Sample Area Estimate Output

| Land Type | Pixels Found | Area (m²) | Area (ha) |
|---|---|---|---|
| Agriculture | 142,680 | 35,670 | 3.57 |
| Forest | 98,432 | 24,608 | 2.46 |
| Urban Land | 64,215 | 16,054 | 1.61 |
| Water | 21,048 | 5,262 | 0.53 |
| Barren Land | 9,261 | 2,315 | 0.23 |

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| 🐍 Python 3.10 | Main programming language |
| 🔥 PyTorch | Deep learning framework |
| 🧠 U-Net + ResNet34 | Segmentation model architecture |
| 🛰️ DeepGlobe Dataset | Satellite land cover images |
| 💻 Google Colab | Free GPU for model training |
| ☁️ Google Drive | Model storage and results |

---

## 🔮 Future Work

- Fly a **real drone** and capture actual field photos
- Process drone photos into an orthomosaic map using **OpenDroneMap**
- Run the trained model on real UAV images (not just satellite data)
- Build a **simple field-use app** for farmers and surveyors
- Target **cm-level accuracy** using RTK GPS drone
- Improve accuracy on the "Unknown" class

---

## 👥 Team

| Name | Roll No. | Contribution |
|---|---|---|
| Surya Kanta Roy | AU/2023/0008914 | Problem statement, solution design |
| Pradip Das | AU/2023/0009009 | Dataset, U-Net model training |
| Anurag Biswas | AU/2023/0009019 | Area calculation pipeline, results |
| Soumyadeep Das | AU/2023/0009231 | Tech stack, conclusion & future work |

**Guide:** Mr. Sayantan Singha Roy | Dept. of CSE | Adamas University | 2025–2026

---


## 📜 License

© 2025 Anurag Biswas, Pradip Das, Soumyadeep Das, Surya Kanta Roy. All rights reserved.

This project and all associated code, models, and documentation are the intellectual property of the team. No part of this project may be reproduced, distributed, modified, or used in any form without explicit written permission from the authors.

---

> *"From pixels to hectares — automated land mapping for a smarter India."*
