# ev-foreign-object-detection-yolov4tiny
---

## 🔍 Project Overview

This repository demonstrates how to **train a custom YOLOv4-tiny object detector** for detecting **foreign objects in Electric Vehicle (EV) wireless charging applications**.

YOLOv4-tiny is a lightweight real-time object detection model that offers fast inference speeds while maintaining strong accuracy, making it suitable for embedded systems and edge devices.

---

## ⚡ Key Features

* End-to-end YOLOv4-tiny custom training pipeline.
* Dataset preparation and annotation in YOLO format.
* Step-by-step instructions for Colab and Google Drive setup.
* Custom config (`.cfg`) tuning for YOLOv4-tiny.
* Model evaluation with test images.

---

## 🛠️ Requirements

* **Google Colab** (recommended) or local GPU setup.
* **Darknet** (AlexeyAB fork).
* Python libraries:

  ```bash
  pip install opencv-python numpy matplotlib
  ```
* Pre-labeled dataset in YOLO format (`.jpg` + `.txt`).

---

## 📂 Project Structure

```
yolov4-tiny-custom/
│── yolov4_tiny_custom_training_14c.ipynb   # Main notebook
│── model/                               # Folder for saving trained weights
│── obj.data                                # Training configuration
│── obj.names                               # Class names
│── yolov4-tiny-custom.cfg                  # Custom YOLO config file
│── process.py                              # Script to generate train/test splits
```

---

## 🚀 Step-by-Step Workflow

### 1️⃣ Clone the Darknet Repository

We begin by cloning the official **AlexeyAB/darknet** repo and compiling it with GPU/CUDA support for faster training.

```bash
!git clone https://github.com/AlexeyAB/darknet
```

---

### 2️⃣ Setup Google Drive Folders

* Create a folder named **`yolov4-tiny`** in Google Drive.
* Inside it, create a sub-folder **`training`** for saving model weights.

---

### 3️⃣ Prepare Custom Dataset

* Collect and label your dataset in YOLO format.
* Organize it as:

  ```
  obj/
     ├── image1.jpg
     ├── image1.txt
     ├── image2.jpg
     ├── image2.txt
  ```
* Zip the folder into **`obj.zip`** and upload to Google Drive.

📌 Reference: [YOLO labeling tutorial](https://github.com/AlexeyAB/darknet#pre-trained-models).

---

### 4️⃣ Upload Required Files

You need:

* `yolov4-tiny-custom.cfg` → modified config file.
* `obj.data` → paths & classes info.
* `obj.names` → class labels.
* `process.py` → script to split dataset into `train.txt` and `test.txt`.

---

### 5️⃣ Configure YOLOv4-Tiny

Edit the `.cfg` file:

* Change **filters** in final conv layer = `(classes + 5) * 3`.
* Update `classes=` with number of target classes.
* Adjust `max_batches` and `steps` depending on dataset size.

---

### 6️⃣ Train the Model

Start training with:

```bash
!./darknet detector train data/obj.data cfg/yolov4-tiny-custom.cfg yolov4-tiny.conv.29 -map
```

💡 Training checkpoints will be saved in the **`training/`** folder.

---

### 7️⃣ Test the Model

Run inference on test images:

```bash
!./darknet detector test data/obj.data cfg/yolov4-tiny-custom.cfg backup/yolov4-tiny-custom_best.weights data/test.jpg
```

Output images with bounding boxes will be saved in the working directory.

---

## 📊 Results

| Metric        | Value (example) |
| ------------- | --------------- |
| mAP\@0.5      | \~99.74%           |
| Inference FPS | \~41 ms            |

---

## 🔮 Future Work

* Experiment with **YOLOv7/YOLOv8** for improved accuracy.
* Deploy model on **Jetson Nano / Raspberry Pi**.
* Optimize with **TensorRT** or **OpenVINO**.

---

## 📜 License

This project uses the [MIT License](LICENSE).

---
