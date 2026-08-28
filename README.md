# 🎮 Virtual Steering Wheel — OpenCV + MediaPipe

Control any PC or browser-based racing game using your webcam and hand gestures — no external hardware required. 

This project uses computer vision to track hand position and orientation in real time, translating physical hand movements into keyboard inputs (`↑`, `↓`, `←`, `→`).

---

## ⚡ Features

- **Real-time Steering:** Calculates steering angle based on the relative position of both wrists[cite: 1].
- **Adaptive Control Zones:** Features dead-zone filtering and release threshold logic to prevent unwanted jitter[cite: 1].
- **Gesture Acceleration & Braking:**
  - 👊 **Fist:** Triggers Acceleration (`UP` arrow).
  - 🖐 **Open Palm:** Triggers Braking (`DOWN` arrow).
- **Live Visual HUD:** Displays real-time status overlay, custom steering wheel UI, angle indicators, and live FPS counter[cite: 1].
- **Cross-Platform:** Built-in auto-detection for macOS and Windows webcam backends.

---

## 🖐 Controls & Gestures

| Hand Gesture | Action | Triggered Key |
|---|---|---|
| 👊 Both Fists (Level) | Accelerate | `UP` Arrow |
| 👊 Both Fists (Tilt Left) | Accelerate + Steer Left | `UP` + `LEFT` Arrows |
| 👊 Both Fists (Tilt Right) | Accelerate + Steer Right | `UP` + `RIGHT` Arrows |
| 🖐 Both Hands Open (Level) | Brake | `DOWN` Arrow |
| 🖐 Both Hands Open (Tilt Left) | Brake + Steer Left | `DOWN` + `LEFT` Arrows |
| 🖐 Both Hands Open (Tilt Right) | Brake + Steer Right | `DOWN` + `RIGHT` Arrows |
| 👊🖐 Mixed (One Fist, One Open) | Neutral (Throttle Off) | None |
| ❌ Hands Out of Frame | Emergency Cut-off (Release All) | All Keys Released |

> **Note:** Steering logic works continuously regardless of whether you are accelerating or braking.

---

## 🛠️ Requirements

- **Python Version:** Python `3.9` to `3.12` *(Required: MediaPipe legacy solutions API does not support Python 3.13+)*
- **Hardware:** Standard Web Camera

---

## ⚙️ Quick Start

### 1. Clone the Repository
```bash
git clone [https://github.com/your-username/virtual-steering-wheel.git](https://github.com/your-username/virtual-steering-wheel.git)
cd virtual-steering-wheel
2. Install DependenciesBashpip install -r requirements.txt
3. Run the ApplicationBashpython main.py
(Press Q or ESC while focused on the webcam window to safely exit)  🔧 ConfigurationYou can customize control sensitivity at the top of main.py[cite: 1, 2]:PythonCAMERA_INDEX       = 0     # 0 = Default webcam, 1/2 = External camera[cite: 1, 2]
DEAD_ZONE_DEG      = 12    # Degrees of central tilt to ignore (prevents wheel drift)[cite: 1, 2]
FLIP_CAMERA        = True  # True mirrors camera for selfie view[cite: 1, 2]
GRACE_FRAMES       = 8     # Frames to wait before releasing keys when hands disappear[cite: 1, 2]
OPEN_FINGER_THRESH = 3     # Min extended fingers required to register an open hand[cite: 1, 2]
❓ TroubleshootingAttributeError: module 'mediapipe' has no attribute 'solutions'You are using Python 3.13+. Switch your virtual environment/interpreter to Python 3.10 or 3.11.[ERROR] Cannot open camera[cite: 1, 2]Change CAMERA_INDEX = 0 to 1 or 2 in main.py[cite: 1, 2].macOS Users: Ensure Terminal or VS Code has camera permissions under System Settings > Privacy & Security > Camera[cite: 1, 2].Steering is Inverted:Set FLIP_CAMERA = False in main.py.  🎮 Game CompatibilityWorks out-of-the-box with any racing game supporting standard arrow key controls:  TrackMania  Browser Games (Hill Climb Racing, Chrome Dino, etc.)  Arcade Emulators / TORCS