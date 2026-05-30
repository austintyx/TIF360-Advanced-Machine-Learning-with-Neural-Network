# Project J: Structure-Preserving Microscopy Image Denoising with Convolutional Neural Networks

## Overview
This notebook contains the experiments, analysis, and figure generation for the project **“Structure-Preserving Microscopy Image Denoising with Convolutional Neural Networks.”** The goal of the project is to compare classical and learned denoising methods for microscopy images, with emphasis on both **noise removal** and **preservation of meaningful image structure**.

The notebook evaluates three main denoising approaches:

- **BM3D** as a classical baseline
- **Residual CNN** as a simpler learned baseline
- **U-Net** as the main multiscale convolutional model

The final comparison is based on both reconstruction quality and structure-aware metrics.

---

## Research Question
Can a U-Net-style convolutional neural network denoise microscopy images more effectively than a classical baseline and a simpler learned baseline, while also preserving meaningful structural content as measured by both reconstruction-based and structure-aware metrics?

---

## Contents of the Notebook
The notebook is organized into the following main parts:

1. **Data loading and preprocessing**
   - Loads paired noisy and clean microscopy image patches
   - Converts images to floating-point format
   - Clips intensities to the range `[0, 1]`
   - Splits the dataset into training, validation, and test subsets

2. **Baseline methods**
   - Applies **BM3D** as a classical denoising baseline

3. **Learned models**
   - Trains a **Residual CNN**
   - Trains a **U-Net**

4. **Evaluation**
   - Computes:
     - **PSNR**
     - **SSIM**
     - **Gradient correlation**
     - **Gradient MAE**
   - Evaluates all methods on the same held-out test subset

5. **Visualization**
   - Generates qualitative comparison figures
   - Generates quantitative summary plots for the report/poster

---

## Dataset
The project uses paired noisy and clean microscopy image patches.

- Total dataset size: **1000 paired images**
- Image size: **256 × 256 × 1**
- Split:
  - **700 training**
  - **150 validation**
  - **150 test**

For the final report-facing evaluation, a deterministic held-out subset of **30 test patches** is used for fair comparison across all methods, including BM3D.

---

## Training Setup
The learned models were trained with the following settings:

- **Optimizer:** Adam
- **Learning rate:** `5e-4`
- **Batch size:** `16`
- **Epochs:** `8`

Model selection is based on validation performance.

---

## Evaluation Metrics
The notebook reports both reconstruction-based and structure-aware metrics:

- **PSNR**: measures reconstruction fidelity
- **SSIM**: measures structural similarity
- **Gradient correlation**: measures how well edge/gradient structure is preserved
- **Gradient MAE**: measures absolute error in image gradients

These gradient-based metrics are particularly important because microscopy denoising should preserve faint structures and local boundaries, not only improve average pixel similarity.

---

## Main Findings
The final results show that:

- Both learned models outperform **BM3D**
- **U-Net** achieves the best overall performance
- The improvement of U-Net over Residual CNN is **modest but consistent** across all reported metrics

Final mean values on the held-out 30-image test subset:

| Method         | PSNR   | SSIM   | Gradient Corr. | Gradient MAE |
|----------------|--------|--------|----------------|--------------|
| U-Net          | 36.57  | 0.9769 | 0.6592         | 0.00150      |
| Residual CNN   | 36.37  | 0.9685 | 0.6549         | 0.00190      |
| BM3D           | 28.45  | 0.8726 | 0.6306         | 0.00700      |
| Noisy input    | 27.50  | 0.7544 | 0.4767         | 0.01199      |

---

## Output Figures
The notebook generates the report/poster figures, including:

- **Qualitative comparison figure**
  - Clean target
  - Noisy input
  - BM3D
  - Residual CNN
  - U-Net

- **Quantitative comparison figure**
  - PSNR
  - SSIM
  - Gradient correlation
  - Gradient MAE

---

## Requirements
Typical Python packages used in this notebook include:

- `numpy`
- `pandas`
- `matplotlib`
- `torch`
- `torchvision`
- `scikit-image`
- `bm3d` or equivalent BM3D implementation
- `jupyter`

Install dependencies with pip as needed, for example:

```bash
pip install numpy pandas matplotlib torch torchvision scikit-image jupyter
