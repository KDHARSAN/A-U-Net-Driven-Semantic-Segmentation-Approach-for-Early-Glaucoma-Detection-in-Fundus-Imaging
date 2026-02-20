# Automated Glaucoma Detection Using U-Net

## Overview
This project implements an end-to-end deep learning system for automated glaucoma detection from retinal fundus images using a U-Net-based semantic segmentation architecture. The system segments the optic disc (OD) and optic cup (OC), computes the Cup-to-Disc Ratio (CDR), and classifies glaucoma based on structural biomarkers.

---

## Problem Statement
Glaucoma is a progressive optic neuropathy that causes irreversible vision loss. Diagnosis relies on optic disc and cup assessment and CDR measurement. Manual evaluation is time-consuming, observer-dependent, and not scalable. This project automates the process using deep learning.

---

## Dataset

- Modality: Color Fundus Images  
- Resolution: 512 × 512  
- Total Images: 1,200  
  - Normal: 600  
  - Glaucoma: 600  
- Split: 80% Training / 20% Testing  
- Augmentation:
  - Rotation (±15°)
  - Horizontal Flip
  - Brightness Scaling (±20%)
  - Zoom (0.8–1.2×)
  - Normalization (0–1)

---

## Model Architecture

- Architecture: U-Net
- Depth: 5 Encoder–Decoder Blocks
- Initial Filters: 64
- Total Parameters: ~31M
- Activation: ReLU
- Output: Sigmoid
- Loss: Dice Loss + Binary Cross-Entropy
- Optimizer: Adam
- Learning Rate: 1e-4
- Batch Size: 8
- Epochs: 50–100

---

## Glaucoma Classification

CDR Calculation:

CDR = Vertical Cup Diameter / Vertical Disc Diameter

Classification Rule:
- CDR < 0.5 → Normal
- 0.5 ≤ CDR < 0.6 → Suspect
- CDR ≥ 0.6 → Glaucoma

---

## Performance Metrics

### Segmentation

| Metric | Optic Disc | Optic Cup |
|--------|------------|-----------|
| Dice   | 0.96       | 0.92      |
| IoU    | 0.93       | 0.87      |
| Pixel Accuracy | 97.8% | 95.1% |

### Classification

- Accuracy: 94.3%
- Sensitivity: 92.1%
- Specificity: 96.5%
- AUC-ROC: 0.97
- Inference Time: 0.12 sec/image

---

## Project Structure
