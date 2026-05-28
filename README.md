# 💪 AI Bicep Curl Counter

A real-time bicep curl counter powered by computer vision and voice commands. The system uses **YOLO pose estimation** to track arm angles and count repetitions automatically, while accepting voice commands to control workout modes.

---

## 🎥 Demo

> *Coming soon — add a screen recording or GIF of the project in action.*

---

## ✨ Features

- 🦾 **Real-time pose estimation** using YOLOv11
- 🎙️ **Voice command control** — hands-free mode switching
- 🔢 **Automatic rep counting** for both arms independently
- 🤝 **Combine mode** — counts reps when both arms move together
- 🔊 **Text-to-speech feedback** — announces each rep count out loud
- 📷 **Live webcam feed** with keypoint and angle overlay

---

## 🗂️ Project Structure

```
├── code.ipynb          # Main notebook
├── yolo11n-pose.pt     # YOLO pose model weights
└── README.md
```

---

## ⚙️ Requirements

- Python 3.8+
- Webcam
- Microphone
- Windows OS *(for voice output via SAPI)*

---

## 📦 Installation

```bash
pip install ultralytics opencv-python cvzone SpeechRecognition pyaudio pyttsx3 pywin32
```

> **Note:** If `pyaudio` fails to install, download the matching `.whl` from [here](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pyaudio) and install it manually.

---

## 🚀 Usage

1. Clone the repository
   ```bash
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```

2. Open `code.ipynb` in Jupyter Notebook or VS Code

3. Run all cells

4. Use voice commands to control the session:

| Command       | Action                                      |
|---------------|---------------------------------------------|
| `"normal"`    | Start counting each arm independently       |
| `"combine"`   | Start counting both arms together           |
| `"stop"`      | End the session                             |

---

## 🧠 How It Works

1. **Pose Detection** — YOLOv11 detects 17 body keypoints from the webcam feed each frame.
2. **Angle Calculation** — The elbow angle is computed using the shoulder, elbow, and wrist coordinates via the arctangent formula.
3. **Rep Logic** — A rep is counted when the arm goes from fully extended (angle > 150°) to curled (angle < 90°) and back.
4. **Voice Control** — A background thread continuously listens for commands using Google Speech Recognition.
5. **Audio Feedback** — Each completed rep is announced out loud using Windows SAPI (via `win32com`).

---

## 🎙️ Voice Architecture

```
Microphone → SpeechRecognition → Command Parser
                                        │
                              ┌─────────┴──────────┐
                           "normal"             "combine"
                              │                     │
                         Independent           Synchronized
                         arm counting          arm counting
```

---

## 🐛 Known Issues

- Voice recognition requires an active internet connection (uses Google Speech API)
- `pyttsx3` has threading issues on some systems — replaced with `win32com` SAPI for reliability
- Colab is **not supported** due to webcam and microphone limitations

---

## 🛠️ Tech Stack

| Library              | Purpose                        |
|----------------------|--------------------------------|
| `ultralytics`        | YOLOv11 pose estimation        |
| `opencv-python`      | Webcam capture & frame display |
| `cvzone`             | On-screen text overlay         |
| `SpeechRecognition`  | Voice command input            |
| `win32com` (SAPI)    | Text-to-speech output          |
| `threading`          | Concurrent voice I/O           |

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

