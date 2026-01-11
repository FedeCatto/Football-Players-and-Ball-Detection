# ⚽ Football Players & Ball Detection

This project focuses on the **design, training, and deployment of an object detection system** tailored for football (soccer) scenarios.  
The main objective is the accurate detection of **players**, **referees**, and the **ball** in both **static images** and **dynamic video footage**.

The system is designed with real-world broadcasting and analysis applications in mind.

---

## 📊 Dataset & Data Understanding

The dataset consists of **600 high-resolution images** (**1280×720 pixels**), split into:
- **Training set:** 520 images
- **Validation set:** 80 images

### Object Classes
The dataset includes three main classes:

- **Player (Class 0):** ~11,383 instances  
- **Referee (Class 1):** ~973 instances  
- **Ball (Class 2):** ~445 instances  

The dataset is **highly imbalanced**, reflecting real football scenarios where players dominate the scene and the ball is the rarest and most challenging object to detect.

---

## 🛠️ Data Cleaning & Preprocessing

Before training, a rigorous data cleaning phase was performed to ensure data integrity:

- **Consistency Check:**  
  Verified one-to-one correspondence between images and YOLO annotation files.
- **Corrupted File Removal:**  
  Removed empty annotation files that could negatively affect training.
- **Bounding Box Clipping:**  
  Corrected bounding boxes partially extending outside image boundaries to improve localization stability.

---

## 🚀 Model Configuration & Training

The **YOLOv8n (nano)** architecture was selected for this task.  
This lightweight model offers an excellent trade-off between **computational efficiency** and **detection performance**, making it suitable for potential **real-time applications**.

### Training Strategy
- **Transfer Learning:**  
  Pre-trained weights were used to leverage knowledge from large-scale datasets.
- **Data Augmentation:**  
  Advanced techniques were applied, including:
  - Mosaic augmentation  
  - MixUp  
  - Horizontal flips  
  - HSV color jittering  

  These augmentations improve robustness to lighting and perspective variations.
- **Training Parameters:**
  - Epochs: **50**
  - Optimizer: **Adam**
  - Input resolution: **640×640**

---

## 📈 Performance Evaluation

The model demonstrates strong overall detection capabilities, particularly for large objects.

### Global Metrics (Validation Set)
- **mAP@0.5:** 0.7049  
- **Precision:** 0.8620  
- **Recall:** 0.6670  

### Per-Class Performance (mAP@0.5)
- **Players:** 0.6563  
- **Referees:** 0.5621  
- **Ball:** 0.1100  

While player and referee detection is reliable, **ball detection remains the main challenge** due to:
- Small object size (~183 average pixels)
- Motion blur during fast shots
- Frequent occlusions

---

## 🎥 Video Inference & Qualitative Results

The trained model was tested on real football video footage using **OpenCV** for frame-by-frame processing.

### Visualization Strategy
- **Players:** Green bounding boxes  
- **Referees:** Blue bounding boxes  
- **Ball:** Yellow circle for improved visibility and trajectory tracking  

### Observations
Qualitative inspection confirms **stable detections of moving players**, demonstrating the system’s practical applicability in broadcasting and analysis environments.

---

## 🔮 Future Improvements

To address current limitations in ball detection, several future directions are proposed:

- Increase input image resolution
- Integrate **temporal information** across frames for object tracking
- Apply **multi-scale feature enhancement** techniques
