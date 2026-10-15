# image-interpolation-from-scratch
Implementation of Bilinear and Bicubic image interpolation from scratch in Python, evaluated via MSE &amp; PSNR metrics.
# Image Interpolation & Dynamic Range Scaling from Scratch (Python)

An implementation of fundamental Digital Image Processing techniques using pure Python and NumPy without relying on high-level computer vision libraries (such as OpenCV) for geometric transformations.

This project covers:
1. **Dynamic Range Stretching / Min-Max Normalization**
2. **Bilinear Interpolation** implemented from scratch
3. **Bicubic Interpolation** with custom cubic convolution weighting
4. **Quantitative Evaluation** using MSE (Mean Squared Error) and PSNR (Peak Signal-to-Noise Ratio)

---

## 📌 Features

### 1. Min-Max Dynamic Range Scaling
Maps image pixel intensities linearly from $[\min(A), \max(A)]$ to $[0, 1]$:
$$f(x, y) = \frac{A(x, y) - \min(A)}{\max(A) - \min(A)}$$

### 2. Interpolation from Scratch
- **Bilinear Interpolation:** Computes a weighted average of the 4 nearest neighbors using linear distances in both axes.
- **Bicubic Interpolation:** Samples a 4x4 neighborhood (16 pixels) with a piecewise cubic convolution polynomial:
  $$\begin{cases} 1.5\vert{}x\vert{}^3 - 2.5\vert{}x\vert{}^2 + 1, & \vert{}x\vert{} \le 1 \\ -0.5\vert{}x\vert{}^3 + 2.5\vert{}x\vert{}^2 - 4\vert{}x\vert{} + 2, & 1 < \vert{}x\vert{} < 2 \\ 0, & \text{otherwise} \end{cases}$$
- Utilizes mirror/edge padding to handle image boundaries without artifacts.

---

## 📊 Experimental Results & Performance Metrics

Reconstructed lower-resolution images (`Chronometerlow2.tif`, `Chronometerlow5.tif`, `Chronometerlow34.tif`) back to the reference resolution ($2140 \times 2136$) and evaluated against the original ground-truth image:

| Test Image | Method | MSE ↓ | PSNR (dB) ↑ |
| :--- | :--- | :---: | :---: |
| **Chronometerlow2.tif** | Bilinear | 15.08 | 36.35 |
| | **Bicubic** | **12.89** | **37.03** |
| **Chronometerlow5.tif** | Bilinear | **242.67** | **24.28** |
| | **Bicubic** | 250.94 | 24.14 |
| **Chronometerlow34.tif** | Bilinear | 48.16 | 31.30 |
| | **Bicubic** | **35.67** | **32.61** |

> **Key Takeaway:** Bicubic interpolation consistently retains sharper edges and produces higher PSNR / lower MSE across moderately downscaled inputs compared to Bilinear interpolation.

---

## 🚀 Getting Started

### Prerequisites
- Python 3.9+
- NumPy
- Pillow (PIL)

### Installation
```bash
git clone [https://github.com/](https://github.com/)<your-username>/image-interpolation-from-scratch.git
cd image-interpolation-from-scratch
pip install numpy pillow
```

### Usage
Run the main script to process test images and calculate metrics:
```bash
python main.py
```

---

## 📄 Documentation
For the full mathematical derivations and detailed visual comparisons, check the [Project Report](docs\EE 475 hw1.pdf).
