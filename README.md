# 🌍 Infinite Earth: AI-Powered Seismic Data Recovery

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-ee4c2c)
![License](https://img.shields.io/badge/License-MIT-green)
![Domain](https://img.shields.io/badge/Domain-Geophysics%20%7C%20Energy-purple)

> **Turning sparse, corrupted seismic data into high-fidelity geological interpretations using Physics-Aware Deep Learning.**

---

## 📖 Overview

**Infinite Earth** is a deep learning framework designed to solve the **Seismic Inpainting** problem. Traditional seismic acquisition often results in sparse or incomplete datasets due to cost constraints, dead traces, or acquisition gaps. Standard interpolation methods (like linear interpolation or FX-Decon) often fail to preserve complex non-linear structures like faults and salt bodies.

This project utilizes a **U-Net Autoencoder** trained via **Self-Supervised Learning** to intelligently reconstruct missing seismic traces. By learning the structural physics of the subsurface, the model restores geological continuity in datasets with up to **50% missing data**.

---

## 🧠 The Problem & Solution

### 📉 The Challenge: Sparse Acquisition
Seismic surveys are capital-intensive. To reduce costs, surveys are often acquired with coarse sampling intervals, or legacy data is left with significant gaps (dead traces). This "aliased" data leads to high uncertainty in interpretation and increases drilling risk.

### 🚀 The AI Solution: Physics-Aware Inpainting
Instead of treating seismic data as just "images," we treat them as physical wavefields. We employ a **Random Trace Decimation** strategy during training:
1.  **Input:** Real seismic data with 50% of traces randomly deleted (simulating sparse acquisition).
2.  **Task:** The AI must reconstruct the missing geology based on the surrounding structural context.
3.  **Result:** A model that learns to reconnect broken horizons and preserve fault planes without human labeling.

---

## 📂 Dataset

The model was trained and validated using the **F3 Netherlands** seismic dataset, a standard benchmark for open-source geophysical analysis.

* **Source:** [F3 Demo 2023 - TerraNubis](https://terranubis.com/datainfo/F3-Demo-2023)
* **Description:** The dataset contains complex geological features including faulted sedimentary layers and salt structures, making it an ideal testbed for structural reconstruction.

> *Note: While trained on F3, the model's architecture is domain-agnostic and can be fine-tuned on proprietary surveys.*

---

## 🏗️ Model Architecture

We implemented a custom **U-Net (Fully Convolutional Network)** optimized for geophysical signal processing.

* **Encoder (Contracting Path):** 5-layer convolutional downsampling to capture global geological context (e.g., "This is a salt dome").
* **Bottleneck:** Compresses input into high-level abstract features.
* **Decoder (Expanding Path):** Upsampling layers that reconstruct the data to original resolution.
* **Skip Connections:** Critical for preserving high-frequency details (seismic amplitudes) by forwarding features directly from Encoder to Decoder.

**Loss Function:** We utilized **L1 Loss** (Mean Absolute Error) instead of MSE. L1 Loss enforces sharper, high-contrast reconstructions, preventing the "blurry" artifacts common in standard interpolation.

---

## 💼 Business Value

This project addresses critical efficiency gaps in the energy exploration sector:

1.  **💰 Cost Reduction:** Simulates the quality of high-density broadband surveys using lower-cost, sparse acquisition geometry.
2.  **🛡️ Risk Mitigation:** Provides clearer definition of fault planes and stratigraphic terminations, reducing uncertainty in reservoir modeling.
3.  **♻️ Legacy Asset Revival:** Unlocks new value from old, sparse, or damaged 2D/3D datasets without the need for expensive re-acquisition.

---

## 🛠️ Installation & Usage

### Prerequisites
* Python 3.8+
* PyTorch
* Segyio (for seismic I/O)
* Numpy, Matplotlib

