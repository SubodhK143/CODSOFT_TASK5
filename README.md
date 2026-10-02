# 👤 Face Detection GUI using Python, OpenCV & Tkinter

A simple **Face Detection GUI application** built with Python that can detect human faces from both **uploaded images** and a **live webcam feed**.

The application uses **OpenCV's Haar Cascade Classifier** for face detection and **Tkinter** to provide a user-friendly graphical interface.

---

## 📌 Project Overview

This project demonstrates how to build a desktop-based computer vision application using:

* 🐍 Python
* 👁️ OpenCV
* 🖼️ Pillow (PIL)
* 🖥️ Tkinter
* 📷 Webcam / Camera
* 🤖 Haar Cascade Face Detection

The application provides two detection modes:

1. **Image Face Detection** – Select an image from your computer and detect faces.
2. **Camera Face Detection** – Use your webcam for real-time face detection.

---

## ✨ Features

* 📁 Upload and analyze images
* 📷 Real-time webcam face detection
* 👤 Detect multiple faces
* 🟩 Draw bounding boxes around detected faces
* 🔢 Display the number of detected faces
* 🖥️ Simple graphical user interface
* ⚡ Real-time detection using OpenCV
* 🎨 Custom Tkinter interface

---

## 🏗️ Project Architecture

```text
                 ┌─────────────────────┐
                 │   Face Detection GUI │
                 └──────────┬──────────┘
                            │
              ┌─────────────┴─────────────┐
              │                           │
       ┌──────▼──────┐             ┌──────▼──────┐
       │ Open Image  │             │   Camera    │
       └──────┬──────┘             └──────┬──────┘
              │                           │
              ▼                           ▼
       Load Image                    Capture Frame
              │                           │
              └─────────────┬─────────────┘
                            ▼
                   ┌─────────────────┐
                   │ Convert to      │
                   │ Grayscale       │
                   └────────┬────────┘
                            ▼
                  ┌─────────────────────┐
                  │ Haar Cascade        │
                  │ Face Detection      │
                  └──────────┬──────────┘
                             ▼
                    ┌────────────────┐
                    │ Draw Bounding  │
                    │ Boxes           │
                    └────────┬───────┘
                             ▼
                    ┌────────────────┐
                    │ Display Number │
                    │ of Faces       │
                    └────────────────┘
```

---

## 🛠️ Technologies Used

| Technology   | Purpose                           |
| ------------ | --------------------------------- |
| Python       | Application development           |
| OpenCV       | Image processing & face detection |
| Tkinter      | GUI development                   |
| Pillow       | Image conversion & GUI display    |
| Haar Cascade | Face detection algorithm          |
| Webcam       | Real-time video input             |

---

## 📂 Project Structure

```text
face-detection-gui/
│
├── face_detection.py
├── README.md
├── requirements.txt
└── screenshots/
    └── face-detection-demo.png
```

> You can rename `face_detection.py` according to the actual Python filename in your repository.

---

## ⚙️ Prerequisites

Make sure Python 3.x is installed.

Check your Python version:

```bash
python --version
```

or:

```bash
python3 --version
```

A working webcam is required for **Camera Detection**.

---

## 📦 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/face-detection-gui.git
```

Navigate into the project:

```bash
cd face-detection-gui
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

Linux/macOS:

```bash
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install opencv-python pillow
```

Tkinter is generally included with standard Python installations.

For Linux, if Tkinter is missing:

```bash
sudo apt install python3-tk
```

---

## 📄 requirements.txt

Create a `requirements.txt` file:

```text
opencv-python
Pillow
```

Install all dependencies using:

```bash
pip install -r requirements.txt
```

---

## ▶️ How to Run

Run the Python application:

```bash
python face_detection.py
```

The GUI will open with two options:

```text
┌──────────────────────────────────┐
│          Face Detection           │
│                                  │
│          [ Open Image ]          │
│                                  │
│       [ Camera Detection ]       │
│                                  │
│          Face Detected: 2        │
└──────────────────────────────────┘
```

---

## 🖼️ Image Detection

Click:

```text
Open Image
```

The application will:

1. Open a file selection dialog.
2. Load the selected image.
3. Resize the image.
4. Convert the image to grayscale.
5. Run Haar Cascade face detection.
6. Draw a rectangle around each detected face.
7. Display the total number of detected faces.

Example:

```text
Input Image
     │
     ▼
OpenCV Image
     │
     ▼
Grayscale Conversion
     │
     ▼
Haar Cascade
     │
     ▼
Face Detection
     │
     ▼
Bounding Boxes + Face Count
```

---

## 📷 Real-Time Camera Detection

Click:

```text
Camera Detection
```

The application accesses the default webcam:

```python
video_capture = cv2.VideoCapture(0)
```

Each video frame is processed continuously.

The application:

* Captures the frame
* Converts it to grayscale
* Detects faces
* Draws bounding boxes
* Counts detected faces
* Updates the GUI

The next frame is scheduled using:

```python
root.after(10, detect_faces)
```

---

## 🤖 Face Detection Algorithm

This project uses OpenCV's pre-trained **Haar Cascade Classifier**:

```python
cv2.data.haarcascades + 'haarcascade_frontalface_default.xml'
```

The classifier is loaded using:

```python
face_cascade = cv2.CascadeClassifier(
    cv2.data.haarcascades +
    'haarcascade_frontalface_default.xml'
)
```

Face detection is performed using:

```python
faces = face_cascade.detectMultiScale(
    gray,
    scaleFactor=1.1,
    minNeighbors=5,
    minSize=(30, 30)
)
```

---

## 🧠 Important OpenCV Concepts

### Grayscale Conversion

Face detection is performed on grayscale images:

```python
gray = cv2.cvtColor(
    image,
    cv2.COLOR_BGR2GRAY
)
```

### Face Detection

```python
faces = face_cascade.detectMultiScale(
    gray,
    scaleFactor=1.1,
    minNeighbors=5,
    minSize=(30, 30)
)
```

### Drawing Bounding Boxes

```python
cv2.rectangle(
    image,
    (x, y),
    (x + w, y + h),
    (0, 255, 0),
    2
)
```

### Counting Faces

```python
num_faces = len(faces)
```

---

## 🔍 Detection Parameters

The project uses:

```python
scaleFactor=1.1
minNeighbors=5
minSize=(30, 30)
```

### `scaleFactor`

Controls how much the image is reduced at each image scale.

### `minNeighbors`

Controls how many neighboring detections are required before considering a detection valid.

### `minSize`

Defines the minimum possible face size to detect.

These parameters can be adjusted depending on lighting, camera quality, and detection requirements.

---

## 🎯 Learning Objectives

This project helped demonstrate practical concepts including:

* Python GUI development
* OpenCV fundamentals
* Computer vision basics
* Haar Cascade classifiers
* Image processing
* Video stream processing
* Webcam integration
* Tkinter event handling
* Real-time frame processing
* Python libraries and package management

---

## 🚀 Possible Future Improvements

The project can be extended with:

* 😎 Eye detection
* 🙂 Smile detection
* 👤 Face recognition
* 📸 Capture detected faces
* 💾 Save detection results
* 🎥 Record processed video
* 📊 Detection statistics
* 🔐 Face authentication
* 🧠 Deep-learning-based face detection
* 🌐 Web-based interface using Flask or FastAPI
* 🐳 Docker containerization

---

## ⚠️ Limitations

Haar Cascade detection can be affected by:

* Poor lighting
* Face orientation
* Occlusion
* Low-resolution images
* Large viewing angles
* Camera quality

For more advanced applications, deep-learning-based detection models can provide improved robustness.

---

## 🔒 Privacy Note

This application processes images and webcam frames locally through the Python application. If you extend the project to store, transmit, or recognize faces, make sure to consider applicable privacy, consent, and data-protection requirements.

---

## 💡 Use Cases

This project can serve as a foundation for:

* Attendance systems
* Smart surveillance prototypes
* Face-based access control
* Computer vision learning
* Webcam-based applications
* Security prototypes
* AI/ML learning projects

---

## 📸 Project Screenshots

Add screenshots of your application here:

```text
screenshots/
├── image-detection.png
└── camera-detection.png
```

Then add them to your README:

```markdown
![Image Detection](screenshots/image-detection.png)

![Camera Detection](screenshots/camera-detection.png)
```

---

## 🧪 Example Output

When faces are detected, the application displays:

```text
Faces Detected: 2
```

and draws bounding boxes around the detected faces.

---

## 👨‍💻 Author

**Subodh Kumar**

🐙 GitHub: [SubodhK143](https://github.com/)
