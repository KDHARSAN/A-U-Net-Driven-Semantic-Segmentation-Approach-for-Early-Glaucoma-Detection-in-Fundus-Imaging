# Automated Glaucoma Detection Using U-Net

## 1. Introduction
This project presents a fully automated glaucoma detection system based on a U-Net deep learning architecture. The system performs optic disc (OD) and optic cup (OC) segmentation from retinal fundus images, computes the Cup-to-Disc Ratio (CDR), and classifies glaucoma using structural biomarkers. The framework is designed for scalable clinical screening and tele-ophthalmology applications.

---

## 2. Problem Statement
Glaucoma is a progressive optic neuropathy that can cause irreversible vision loss. Diagnosis depends on accurate optic nerve head analysis, particularly OD/OC segmentation and CDR measurement. Manual grading is time-consuming (3–5 minutes per image), observer-dependent (5–10% variability), and not suitable for mass screening. This project automates the complete pipeline using deep learning.

---

## 3. Dataset Details

- Image Type: Color Fundus Images  
- Resolution: 512 × 512 pixels  
- Total Samples: 1,200  
  - Normal: 600  
  - Glaucoma: 600  
- Train/Test Split: 80% / 20%  
- Data Augmentation:
  - Rotation (±15°)
  - Horizontal Flip
  - Brightness Scaling (±20%)
  - Zoom (0.8×–1.2×)
  - Normalization (0–1 scaling)

---

## 4. Methodology

### 4.1 Preprocessing
- Image resizing to 512×512
- Pixel normalization
- Optional CLAHE contrast enhancement

### 4.2 U-Net Architecture
- 5 Encoder–Decoder blocks
- Initial Filters: 64
- Convolution Kernel: 3×3
- Activation: ReLU
- Output Layer: Sigmoid
- Skip connections between encoder and decoder
- Total Parameters: ~31 Million

### 4.3 Training Configuration
- Loss Function: Dice Loss + Binary Cross-Entropy
- Optimizer: Adam
- Learning Rate: 1e-4
- Batch Size: 8
- Epochs: 50–100
- Hardware: NVIDIA RTX 3060 (12GB VRAM)

---

## 5. Glaucoma Classification

### CDR Formula

CDR = Vertical Cup Diameter / Vertical Disc Diameter

### Classification Criteria
- CDR < 0.5 → Normal
- 0.5 ≤ CDR < 0.6 → Suspect
- CDR ≥ 0.6 → Glaucoma

---

## 6. Performance Metrics

### Segmentation Results

| Metric | Optic Disc | Optic Cup |
|--------|------------|-----------|
| Dice Coefficient | 0.96 | 0.92 |
| IoU | 0.93 | 0.87 |
| Pixel Accuracy | 97.8% | 95.1% |

### Classification Results
- Accuracy: 94.3%
- Sensitivity: 92.1%
- Specificity: 96.5%
- AUC-ROC: 0.97
- False Positive Rate: 3.5%
- False Negative Rate: 7.9%
- Inference Time: 0.12 seconds per image

---

## 7. Project Structure

```
glaucoma-detection/
│
├── data/
│   ├── train/
│   ├── test/
│   └── masks/
│
├── models/
│   └── unet_model.py
│
├── utils/
│   ├── preprocessing.py
│   ├── metrics.py
│   └── cdr_calculation.py
│
├── train.py
├── test.py
├── predict.py
├── requirements.txt
└── README.md
```

---

## 8. Installation

### Requirements
- Python 3.8+
- TensorFlow or PyTorch
- OpenCV
- NumPy
- scikit-learn
- matplotlib

### Setup Instructions

```
git clone https://github.com/your-username/glaucoma-detection.git
cd glaucoma-detection
pip install -r requirements.txt
```

---

## 9. Training

```
python train.py
```

Model checkpoints will be saved inside the `/models` directory.

---

## 10. Testing

```
python test.py
```

Outputs:
- Segmentation masks
- Dice and IoU scores
- Classification metrics

---

## 11. Inference

```
python predict.py --image path_to_image
```

Output:
- Segmented optic disc and cup masks
- Computed CDR value
- Predicted label (Normal / Suspect / Glaucoma)

---

## 12. Advantages
- Fully automated segmentation and classification
- High segmentation precision (Dice > 0.92)
- Fast inference (<0.2 sec/image)
- Clinically interpretable biomarker (CDR)
- Scalable for telemedicine screening

---

## 13. Limitations
- Sensitive to poor image quality
- Borderline CDR cases may require clinical review
- Requires annotated masks for supervised training

---

## 14. Future Work
- Attention U-Net / Residual U-Net
- Multi-class neuroretinal rim segmentation
- OCT image integration
- Explainable AI (Grad-CAM)
- Web-based deployment (Flask/FastAPI)

---

## 15. Conclusion
The proposed U-Net-based glaucoma detection system achieves strong segmentation performance (Dice ≥ 0.92) and high classification accuracy (94.3%). The framework demonstrates practical feasibility for automated, large-scale glaucoma screening in real-world clinical environments.
