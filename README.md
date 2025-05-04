# FRAME-FLOW: A Real-Time Video Frame Interpolation

## Overview

**Video Frame Interpolation (VFI)** is a crucial technique in computer vision that generates intermediate frames between consecutive frames to achieve smoother motion. Traditional VFI methods often struggle with handling fast motion, complex scene dynamics, and require manual specification of the number of frames, making them inefficient for real-time applications. In this project, we propose **Frame Flow**, a deep learning-based real-time VFI model that optimizes frame generation by automating the interpolation process and reducing computational redundancy.

Our approach leverages the **IFNet architecture** within a Teacher-Student framework, enhanced with **U-Net-based refinement** for improved feature extraction and motion estimation. A key innovation of our model is its ability to dynamically determine the number of frames to generate, eliminating manual input. This is achieved by computing the structural similarity (SSIM) between consecutive frames and stopping frame generation when the similarity exceeds 0.98, ensuring adaptive and efficient interpolation.

Although this introduces a slight increase in inference time, the Teacher-Student architecture of **RIFE** ensures that the student model retains a low inference time, making the added SSIM computation negligible in terms of overall performance. Experimental results show that our adaptive method achieves a 35.43% reduction in storage requirements, significantly reduces redundant frames, and enhances computational efficiency. The model achieves **SSIM** of 0.9624 and **PSNR** of 36.72 dB, indicating high-quality frame synthesis. This research has wide-ranging applications in video enhancement, slow-motion generation, animation, and high-frame-rate content creation. Furthermore, it has potential future applications in medical imaging, where frame interpolation could minimize radiation exposure by reconstructing intermediate X-ray frames, though this remains an area for further study. The findings demonstrate that **Frame Flow** is an efficient and adaptive solution for real-time VFI, particularly in resource-constrained environments.

## Project Files

- **`frame-flow.ipynb`**: Jupyter Notebook implementing the frame interpolation models and functions.
- **`baseline.mp4`**: Video output generated using the Fixed Depth interpolation method.
- **`optimized.mp4`**: Video output generated using the Adaptive Depth interpolation method.
- **`psnr_comparison.png`**: Bar chart comparing the average PSNR (Peak Signal-to-Noise Ratio) of both methods.
- **`reduction_gain_comparison.png`**: Bar chart comparing the reduction and gain percentages (frame reduction, inference time increase, and storage reduction).
- **`ssim_comparison.png`**: Bar chart comparing the average SSIM (Structural Similarity Index) of both methods.
- **`model-frameflow.zip`**: Model weights and additional files required for frame interpolation.

## Methods Used

### Fixed Depth Interpolation
- **Inference Time**: 2.969 seconds
- **Frames Generated**: A fixed number of frames (depth=6) between the start and end frames.
- **SSIM**: 0.987
- **PSNR**: 41.99 dB

### Adaptive Depth Interpolation
- **Inference Time**: 10.4001 seconds
- **Frames Reduction**: 49.23%
- **Inference Time Increase**: 250.34%
- **Storage Reduction**: 35.43%
- **SSIM**: 0.9624
- **PSNR**: 36.72 dB

## Results

### Comparison of Fixed and Adaptive Methods

| Metrics (Avg)                | Fixed    | Adaptive |
| ---------------------------- | -------- | -------- |
| **Inference Time (sec)**      | 2.969    | 10.4001  |
| **Frame Reduction (%)**       | -        | 49.23    |
| **Inference Time Increase (%)** | -      | 250.34   |
| **Storage Reduction (%)**     | -        | 35.43    |
| **SSIM**                      | 0.987    | 0.9624   |
| **PSNR (dB)**                 | 41.99    | 36.72    |

### Graphs

#### **PSNR Comparison**  
![PSNR Comparison](psnr_comparison.png)

#### **Reduction & Gain Comparison**  
![Reduction & Gain Comparison](reduction_gain_comparison.png)

#### **SSIM Comparison**  
![SSIM Comparison](ssim_comparison.png)

## How It Works

1. **Model Setup**: The frame interpolation model is loaded and evaluated.
2. **Frame Interpolation**: The `generate_interpolated_frame()` function is used to generate intermediate frames between two consecutive frames.
3. **Adaptive vs Fixed Depth**: The Adaptive method dynamically adjusts the number of frames based on the similarity between the original frames and interpolated frames, while the Fixed Depth method generates a fixed number of frames.
4. **Metrics Calculation**: SSIM and PSNR are used to evaluate the quality of the generated frames.

## Requirements

To run this project, you will need the following libraries:

- **Python 3.x**
- **PyTorch**
- **OpenCV**
- **MoviePy**
- **NumPy**
- **Matplotlib**
- **Scikit-Image**
- **psutil**
- **torchvision**

You can install all dependencies using pip:

```bash
pip install torch opencv-python moviepy numpy matplotlib scikit-image psutil torchvision
