# 🎮 Virtual Steering Wheel — OpenCV + MediaPipe

Control any PC or browser-based racing game using your webcam and hand gestures. No external hardware required.

This project uses computer vision to track hand position and orientation in real time, translating physical hand movements into keyboard inputs (`↑`, `↓`, `←`, `→`).

---

## ⚡ Features

* **Real-time Steering:** Calculates steering angle based on the relative position of both wrists.
* **Adaptive Control Zones:** Features dead-zone filtering and release threshold logic to prevent unwanted jitter.
* **Gesture Acceleration & Braking:**
  * 👊 **Fist:** Triggers Acceleration (`UP` arrow).
  * 🖐 **Open Palm:** Triggers Braking (`DOWN` arrow).
* **Live Visual HUD:** Displays real-time status overlay, custom steering wheel UI, angle indicators, and live FPS counter.
* **Cross-Platform:** Built-in auto-detection for macOS and Windows webcam backends.

---

## 🖐 Controls & Gestures

| Hand Gesture | Action | Triggered Key |
| :--- | :--- | :--- |
| 👊 Both Fists (Level) | Accelerate | `UP` Arrow |
| 👊 Both Fists (Tilt Left) | Accelerate + Steer Left | `UP` + `LEFT` Arrows |
| 👊 Both Fists (Tilt Right) | Accelerate + Steer Right | `UP` + `RIGHT` Arrows |
| 🖐 Both Hands Open (Level) | Brake | `DOWN` Arrow |
| 🖐 Both Hands Open (Tilt Left) | Brake + Steer Left | `DOWN` + `LEFT` Arrows |
| 🖐 Both Hands Open (Tilt Right) | Brake + Steer Right | `DOWN` + `RIGHT` Arrows |
| 👊🖐 Mixed (One Fist, One Open) | Neutral (Throttle Off) | None |
| ❌ Hands Out of Frame | Emergency Cut-off | All Keys Released |

> **Note:** Steering logic works continuously regardless of whether you are accelerating or braking.

---

## 🛠️ Requirements

* **Python Version:** `3.9` to `3.12` *(MediaPipe legacy solutions do not support Python 3.13+)*
* **Hardware:** Standard Web Camera

---

## ⚙️ Quick Start

**1. Clone the Repository**
```bash
git clone https://github.com/your-username/virtual-steering-wheel.git
cd virtual-steering-wheel
2. Install Dependencies

Bash
pip install -r requirements.txt
3. Run the Application

Bash
python main.py
(Press Q or ESC while focused on the webcam window to safely exit)

🔧 Configuration
You can customize control sensitivity at the top of main.py:

Python
CAMERA_INDEX       = 0     # 0 = Default webcam, 1/2 = External camera
DEAD_ZONE_DEG      = 12    # Degrees of central tilt to ignore (prevents wheel drift)
FLIP_CAMERA        = True  # True mirrors camera for selfie view
GRACE_FRAMES       = 8     # Frames to wait before releasing keys when hands disappear
OPEN_FINGER_THRESH = 3     # Min extended fingers required to register an open hand
❓ Troubleshooting
AttributeError: module 'mediapipe' has no attribute 'solutions'

Switch your Python environment to 3.10 or 3.11. Python 3.13+ is not supported by legacy MediaPipe.

[ERROR] Cannot open camera

Change CAMERA_INDEX = 0 to 1 or 2 in main.py.

macOS Users: Ensure Terminal or VS Code has camera permissions under System Settings > Privacy & Security > Camera.

Steering is Inverted

Set FLIP_CAMERA = False in main.py.
