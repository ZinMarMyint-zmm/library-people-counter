# Library People Counter

A Python application that uses YOLOv8 object detection to count people entering a university library. It runs on macOS, Windows, and Raspberry Pi, and includes a Tkinter desktop GUI for operating the system and viewing counts.

Built during my Python Developer internship at Southeast Bangkok University.

> **Note:** Footage from the library is not included in this repository for privacy reasons.

## Features

- Person detection using YOLOv8 (Ultralytics)
- Entry counting: counts people entering the library
- Cross-platform: macOS, Windows, and Raspberry Pi
- Works with different cameras (built-in webcam, USB webcam, Raspberry Pi camera)
- Tkinter desktop GUI for operating the system and viewing counts

## Supported Platforms

| Platform | Camera | Environment |
|----------|--------|-------------|
| MacBook | Built-in camera | macOS |
| Windows PC | USB webcam | Windows |
| Raspberry Pi 5 | Raspberry Pi camera | Raspberry Pi Desktop (Raspberry Pi OS) |

## How It Works

```
Camera (built-in / USB / Raspberry Pi camera)
    ↓
Frame capture
    ↓
YOLOv8 person detection
    ↓
Entry counting logic
    ↓
Tkinter GUI (live count display)
```

1. Frames are captured from the camera.
2. YOLOv8 detects people in each frame.
3. The counting logic virtual line crossing counts people entering the library. 
4. The GUI shows the current count and controls.

## Tech Stack

- **Language:** Python
- **Detection:** YOLOv8 (Ultralytics)
- **Video processing:** OpenCV and Picamera2 on Raspberry Pi
- **GUI:** Tkinter

## Getting Started

### Prerequisites

- Python 3.12
- A camera supported on your platform (see table above)

### Installation

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
python -m venv .venv
```

Activate the virtual environment:

```bash
# macOS / Raspberry Pi
source .venv/bin/activate

# Windows (PowerShell)
.venv\Scripts\Activate.ps1
```

Install dependencies:

```bash
pip install -r requirements.txt
```

The YOLOv11n.pt weights are downloaded automatically by Ultralytics on first run.

### Platform Notes

- **macOS:** Allow camera access for Terminal / your IDE in System Settings → Privacy & Security → Camera.
- **Windows:** Plug in the USB webcam before starting. If the wrong camera opens, change the camera index in the config.
- **Raspberry Pi:** Enable the Picamera2 and make sure it is detected.
### Run

```bash
python main.py
```

[Edit the command to match your entry file.]

## Real-World Testing

The system was tested in the actual library environment.

| Scenario | Result |
|----------|--------|
| 1-3 people, clearly separated | Counted reliably |
| Overlapping people (e.g., 4 people close together) | Reduced accuracy; e.g., 3 of 4 counted |

These are observations from informal testing in the library, not results from a formal benchmark.

## Limitations

- **Occlusion:** When people overlap in the camera view, the detector can merge them, which causes undercounting.
- Accuracy depends on camera angle, lighting, and distance.
- Not evaluated on a large labeled dataset.

## Future Improvements

- Add object tracking (e.g., ByteTrack or DeepSORT) to follow individuals across frames and reduce missed counts
- Mount the camera overhead to reduce occlusion
- Tune confidence and NMS thresholds for crowded scenes
- Measure and compare FPS across macOS, Windows, and Raspberry Pi
- Evaluate on a labeled dataset and report precision/recall
- Add exit counting and current-occupancy estimation
- Export counts with timestamps for analytics

## Project Structure

```
.
├── main.py              # Application entry point
├── detector.py          # YOLOv8 detection logic
├── gui.py               # Tkinter GUI
└── requirements.txt
```

## Privacy

This project processes video of people. Raw footage and images of identifiable individuals are not stored in this repository. If you deploy a similar system, follow your organization's privacy policy and local regulations.

## Author

**Zin Mar Myint**
[GitHub](https://github.com/ZinMarMyint-zmm) · [LinkedIn](www.linkedin.com/in/zin-mar-myint)
