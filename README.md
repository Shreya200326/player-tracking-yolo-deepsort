# ⚽ Player Re-Identification using YOLOv8 and Deep SORT

This project detects and tracks players in a sports video using a custom-trained YOLOv8 model and Deep SORT tracking. It assigns consistent IDs to players across frames, even if they temporarily disappear from view.

---

## 📌 Features

- Detects players using a custom YOLOv8 model (`best.pt`)
- Tracks players across frames using Deep SORT
- Maintains consistent player IDs even after occlusion (up to 10 seconds)
- Real-time video display with bounding boxes and ID overlays

---

## 📂 Project Structure

```

player-reid-yolov8/
├── best.pt               👈 Downloaded separately (link below)
├── main.py    # Main script
├── requirements.txt      # Python dependencies
├── README.md             # Project documentation
└── report.md / .pdf      # Methodology report 
````
---

## 📦 Model Weights

The YOLOv8 model file (`best.pt`) is too large to host directly on GitHub.

📥 [**Click here to download best.pt from Google Drive**]([https://drive.google.com/your-shareable-link-here](https://drive.google.com/file/d/1vJGoLu5lf8Dp4YVuMOod4Qmg_mHdB4nC/view?usp=sharing))

➡️ After downloading, place `best.pt` in the root directory of this project.

---

## 🛠️ Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/Shreya200326/player-tracking-yolo-deepsort.git
cd player-tracking-yolo-deepsort
````

### 2. (Optional) Create a Virtual Environment

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## ▶️ Running the Code

```bash
python main.py
```

* A video window will open showing real-time player detection and tracking.
* Press `q` to exit.

---

## ⚙️ Customization

* The model tracks only class ID `2` (assumed to be "player"). You can adjust this in `main.py`.
* `max_age=300` is used in Deep SORT to allow up to 10 seconds of disappearance tolerance.

---

## 🧰 Requirements

Listed in `requirements.txt`. For reference:

```
ultralytics
opencv-python
deep_sort_realtime
```

Install using:

```bash
pip install -r requirements.txt
```

---

## 📌 Notes

* Ensure your input video is named `15sec_input_720p.mp4` or adjust the path in `main.py`.
* If your model uses different class mappings, update the class ID check accordingly.

---
