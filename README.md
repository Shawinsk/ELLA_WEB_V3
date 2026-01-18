# E.L.L.A V2 - Elegant Language & Logic Assistant

![Python](https://img.shields.io/badge/Python-3.14-blue?logo=python)
![React](https://img.shields.io/badge/React-18.2-61DAFB?logo=react)
![Electron](https://img.shields.io/badge/Electron-28-47848F?logo=electron)
![Gemini](https://img.shields.io/badge/Google%20Gemini-Native%20Audio-4285F4?logo=google)
![License](https://img.shields.io/badge/License-MIT-green)

> **"Built by SK"**

**E.L.L.A** (**E**legant **L**anguage & **L**ogic **A**ssistant) is a next-generation multimodal AI desktop agent. It bridges the gap between conversational AI and physical/digital action, allowing you to control your environment, design physical objects, and browse the web using only your voice.

Powered by **Google's Gemini 2.5 Native Audio**, ELLA supports real-time, low-latency voice conversations with interrupt capabilities, making it feel like talking to a real person.

---

## 🌟 Key Features

### 🧠 Advanced AI Core

- **Native Audio Streaming**: Uses Gemini 2.5's native audio capabilities for sub-500ms latency.
- **Interruptible Speech**: You can cut ELLA off mid-sentence, and she will stop listening and process your new input immediately.
- **Multimodal Understanding**: ELLA can see what you see (via webcam) and what's on your screen (via screenshot tools).

### 🧊 Generative 3D CAD (Computer Aided Design)

- **Voice-to-CAD**: Simply say "Make a 3D model of a bolt with a 10mm head" and ELLA generates it instantly.
- **Parametric Editing**: Ask for changes naturally: "Make it taller", "Add a hole in the center".
- **Visual Preview**: View the generated 3D models in an interactive window within the app.
- **Technology**: Built on `build123d` and a custom Python agent for reliable geometric construction.

### 🌐 Autonomous Web Agent

- **Full Browser Control**: ELLA can open a Chromium browser to perform research, take screenshots, or fill forms.
- **Visual Reasoning**: The agent looks at the webpage screenshot to understand where to click and type.
- **Safety**: Runs in a sandboxed Playwright instance.

### 🖨️ 3D Printing Integration

- **Direct Slicing**: ELLA can take the CAD model she just generated, slice it (using OrcaSlicer), and get it ready for printing.
- **Wireless Printing**: Supports Moonraker (Klipper), OctoPrint, and PrusaLink.
- **Status Monitoring**: Ask "How is the print going?" to get real-time progress, temperatures, and time remaining.

### 🏠 Smart Home Control

- **TP-Link Kasa Support**: Native integration with Kasa smart plugs and bulbs.
- **Voice Commands**: "Turn on the living room lights", "Set the bedroom light to blue".
- **Auto-Discovery**: Automatically finds devices on your local network.

### 🖐️ "Minority Report" UI

- **Gesture Control**: Use hand gestures to interact with the UI without touching the mouse or keyboard.
  - **Pinch**: Click/Select.
  - **Open Palm**: Release/Hover.
  - **Fist**: Grab/Drag windows.
- **Face Authentication**: Secure your assistant so it only responds to you. Uses local facial recognition to unlock the interface.

---

## 🛠️ System Architecture

ELLA is built as a hybrid desktop application:

1.  **Frontend (UI)**: Built with **React**, **Vite**, and **Tailwind CSS**. It manages the visual interface, 3D rendering (Three.js), and gesture recognition (MediaPipe).
2.  **Backend (Brain)**: A **Python (FastAPI)** server that handles:
    - Audio I/O (PyAudio/SoundDevice)
    - WebSocket communication with the frontend
    - Gemini API connectivity
    - Agent tools (CAD, Web, Printer, Home)
3.  **Wrapper**: **Electron** serves the React app and provides a native desktop window frame.

---

## 🚀 Installation Guide

### Prerequisites

- **Operating System**: Windows 10/11 or macOS 14+
- **Python**: Version 3.10 or higher (3.14 recommended)
- **Node.js**: Version 18+
- **Webcam**: Required for Vision features
- **Microphone**: Required for Voice features

### Step 1: Clone the Repository

```bash
git clone https://github.com/Shawinsk/ELLA_PROJECT_V2.0.2.git ELLA
cd ELLA
```

### Step 2: Setup Python Backend

It is highly recommended to use Conda or venv.

```bash
# Create environment
conda create -n ella python=3.14 -y
conda activate ella

# Install Audio Dependencies (macOS only)
# brew install portaudio

# Install Python Requirements
pip install -r requirements.txt

# Install Playwright Browsers (for Web Agent)
playwright install chromium
```

### Step 3: Setup React Frontend

```bash
npm install
```

### Step 4: Configure API Key

1.  Get a generic **Gemini API Key** from [Google AI Studio](https://aistudio.google.com/).
2.  Create a `.env` file in the root directory.
3.  Add your key:
    ```env
    GEMINI_API_KEY=your_actual_api_key_here
    ```

### Step 5: Face Authentication (Optional)

1.  Take a clear photo of your face.
2.  Save it as `reference.jpg` in the root (or `backend/`) folder.
3.  ELLA will compare the webcam feed against this image to unlock.

---

## ▶️ How to Run

You can run ELLA with a single command that starts both the backend and frontend.

**Make sure your Conda environment is active!**

```bash
conda activate ella
npm run dev
```

- **Frontend**: Opens at `http://localhost:5173`
- **Backend**: Runs on `http://localhost:8000`

---

## 🎮 Usage Guide

### Voice Interaction

- **Wake Word**: None required (uses VAD - Voice Activity Detection). Just start speaking when the visualizer is active.
- **Stop/Interrupt**: Just speak over her. She will stop talking and listen.

### Common Commands

| Category     | Example Command                                   |
| :----------- | :------------------------------------------------ |
| **General**  | "Hello Ella, what can you do?"                    |
| **CAD**      | "Design a hexagonal box with a lid."              |
| **CAD**      | "Make the walls thicker."                         |
| **Web**      | "Go to Google News and tell me the top headline." |
| **Home**     | "Turn on the office light."                       |
| **Printing** | "Slice this model and send it to the printer."    |

---

## 📂 Project Structure

```plaintext
ELLA_WEB/
├── backend/                   # Python Backend
│   ├── ella.py                # Main Agent Logic & Audio Loop
│   ├── server.py              # FastAPI/Socket.IO Server
│   ├── cad_agent.py           # CAD Generation Logic
│   ├── web_agent.py           # Playwright Browser Logic
│   ├── printer_agent.py       # 3D Printing Logic
│   ├── kasa_agent.py          # Smart Home Logic
│   ├── tools.py               # Gemini Tool Definitions
│   └── authenticator.py       # Face Recognition
├── src/                       # React Frontend
│   ├── components/            # UI Components (Windows, Chat, etc.)
│   ├── assets/                # Images & Icons
│   └── App.jsx                # Main Entry
├── projects/                  # User data (CAD files, logs, etc.)
├── printer_profiles/          # OrcaSlicer profiles
├── settings.json              # App configuration
├── package.json               # Frontend Deps
└── requirements.txt           # Backend Deps
```

---

## 🔒 Privacy & Local Processing

- **Biometrics**: Face data is processed locally using MediaPipe. Your face image is never sent to the cloud.
- **Project Files**: All CAD designs and files are stored locally in the `projects/` folder.
- **Cloud Usage**: Only voice audio and text prompts are sent to Google Gemini for processing. Video frames for "vision" are sent only when necessary for context.

---

## 🤝 Credits

**Built by SK**

- **Core AI**: Google Gemini 2.5
- **3D Kernel**: build123d
- **Vision**: MediaPipe
- **Browser**: Playwright

---

_Created with ❤️ by SK for the Future of AI Interaction._
