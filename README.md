# Custom Object Detection Using YOLOv8 🎯🤖

This project demonstrates how to perform **custom object detection using YOLOv8** in Python.  
It supports detecting objects from images using trained YOLOv8 models and provides scripts for both compact batch detection and single image detection.

---

## 🚀 Features

- 🧠 Custom object detection using **YOLOv8**
- 📷 Detect objects in single images
- 📁 Batch / compact detection support
- 🖼️ Automatic bounding box visualization
- ⚡ Fast and accurate inference
- 🐍 Simple Python execution

---

## 📂 Project Structure

```
Custom_Object_Detection_Using_YoloV8/
├── detect_compact.py        # Compact / batch object detection script
├── detection_single.py      # Single image object detection script
└── README.md                # Project documentation
```

---

## 🛠️ Requirements

Make sure you have:

- Python 3.8 or higher
- pip package manager
- YOLOv8 dependencies installed

Required Python libraries typically include:

```bash
pip install ultralytics opencv-python numpy
```

---

## 📦 Installation

### 1. Clone Repository

```bash
git clone https://github.com/UNICDEB/Custom_Object_Detection_Using_YoloV8.git
cd Custom_Object_Detection_Using_YoloV8
```

---

### 2. (Optional) Create Virtual Environment

**Windows**
```bash
python -m venv venv
venv\Scripts\activate
```

**Linux / macOS**
```bash
python3 -m venv venv
source venv/bin/activate
```

---

### 3. Install Dependencies

```bash
pip install ultralytics opencv-python numpy
```

---

## ▶️ How to Run

### 🔹 Single Image Detection

Run:

```bash
python detection_single.py
```

This script will:
- Load the YOLOv8 model
- Read a single input image
- Perform object detection
- Display or save the output image

---

### 🔹 Compact / Batch Detection

Run:

```bash
python detect_compact.py
```

This script will:
- Process multiple images or continuous detection
- Perform inference using YOLOv8
- Save detection results automatically

---

## 🖼️ Output

- Detected objects are drawn with bounding boxes and labels
- Output images are saved locally or displayed in a window
- Confidence scores shown for each detected object

---

## ⚙️ Custom Model

You can replace the YOLO model file path inside the scripts to use your **own trained custom model**:

```python
model = YOLO("your_custom_model.pt")
```

---

## 📌 Notes

- First run may download YOLO model weights automatically.
- GPU acceleration improves performance significantly.
- Adjust confidence threshold and image path inside scripts as needed.

---

## 🤝 Contributing

Contributions are welcome!

1. Fork this repository  
2. Create a feature branch  
3. Commit your changes  
4. Submit a Pull Request  

---

## 📄 License

This project is open source. Refer to repository for license details.

