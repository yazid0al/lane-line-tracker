# lane-line-tracker
Real-time road lane line detection using classical computer vision — Canny edge detection, ROI masking, and the Hough Transform with OpenCV.

# 🛣️ Lane Line Tracker

Real-time road lane line detection using classical computer vision — no deep learning required.

![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=flat-square&logo=python&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-4.8+-5C3EE8?style=flat-square&logo=opencv&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat-square&logo=jupyter&logoColor=white)


---

![Lane detection demo](output/demo.gif)

## 📋 Overview

This project processes dashcam-style driving footage frame by frame and overlays the detected left and right lane lines in real time. It relies entirely on classical image-processing techniques — no trained model or GPU needed — making it lightweight, interpretable, and easy to tune.

## ✨ Features

- 🖤 **Grayscale + Gaussian blur** to suppress noise before edge detection
- ⚡ **Canny edge detection** to isolate strong intensity gradients
- 🔺 **Region-of-interest (ROI) masking** to focus only on the road area in front of the camera
- 📐 **Probabilistic Hough Transform** to detect straight line segments from edges
- 📊 **Slope-based averaging & extrapolation** to merge noisy segments into two clean lane lines
- 🎬 **Video overlay & export** — annotated frames are written to a new output video

## 🔍 How It Works

| Step | Stage | Purpose |
|---|---|---|
| 1 | Grayscale + Blur | Reduce noise before edge detection |
| 2 | Canny Edge Detection | Find edges in the frame |
| 3 | ROI Mask | Keep only the road-facing trapezoid region |
| 4 | Hough Transform | Detect straight line segments from edges |
| 5 | Average / Extrapolate | Merge left and right segments into two clean lines |
| 6 | Overlay | Draw the final lane lines back onto the original frame |

```
Frame → Grayscale → Blur → Canny → ROI Mask → HoughLinesP → Average Slope/Intercept → Overlay → Output
```

## 📂 Project Structure

```
lane-line-tracker/
├── notebooks/
│   └── lane_detection.ipynb
├── output/
│   └── demo.gif
├── requirements.txt            
└── README.md
```

## 🚀 Getting Started

### Prerequisites

- Python 3.9+
- A driving video file (dashcam footage, `.mp4`)

### Installation

```bash
git clone https://github.com/yazid0al/lane-line-tracker.git
cd lane-line-tracker
pip install -r requirements.txt
```

### Usage

1. Place your input video somewhere accessible (e.g. `sample_videos/road.mp4`).
2. Open `notebooks/lane_detection.ipynb` in Jupyter:
   
   ```bash
   jupyter notebook notebooks/lane_detection.ipynb
   ```
4. Update the `VIDEO_PATH` variable in the **Run** cell to point to your video.
5. Run all cells. A live preview window will display the annotated video, and the result is saved to `output/output.mp4`.
6. Press `q` at any time to stop processing early.

## ⚙️ Tuning

The pipeline is sensitive to camera angle, resolution, and lighting. Key parameters to adjust in `process_frame`:

- **ROI trapezoid** — the four vertices defining the road region (currently expressed as fractions of frame width/height)
- **Canny thresholds** — `cv2.Canny(blur, 50, 150)`
- **Hough parameters** — `rho`, `theta`, `threshold`, `minLineLength`, `maxLineGap` in `cv2.HoughLinesP`

## 🧑‍💻 Author
**Yazid Alasidi**
