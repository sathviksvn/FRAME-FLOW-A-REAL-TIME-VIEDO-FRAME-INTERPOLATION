# FRAME-FLOW: A Real-Time Video Frame Interpolation

## Overview

Video Frame Interpolation (VFI) generates intermediate frames between consecutive frames to achieve smoother motion. Traditional methods often struggle with fast motion, complex scenes, and require manual specification of the number of frames. **Frame Flow** addresses these challenges by automating the interpolation process and reducing computational redundancy. The model uses the **IFNet architecture** within a Teacher-Student framework, enhanced by **U-Net-based refinement** for improved feature extraction and motion estimation.

A key innovation is the model's ability to dynamically determine the number of frames to generate. This is achieved by calculating the structural similarity (SSIM) between consecutive frames and stopping frame generation when the similarity exceeds 0.98. While this introduces a slight increase in inference time, the **RIFE architecture** ensures that the student model retains a low inference time, minimizing the impact on overall performance. The method shows a 35.43% reduction in storage requirements, improves frame efficiency, and achieves high-quality results with **SSIM** of 0.9624 and **PSNR** of 36.72 dB. This approach has applications in video enhancement, slow-motion generation, and medical imaging, such as minimizing radiation exposure in X-ray frames.

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
