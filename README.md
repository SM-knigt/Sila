# 🤟 Sila — Real-Time Arabic Sign Language Translator

<p align="center">
  <img src="logo-sila.png" alt="Sila logo" width="140" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/HTML5-orange?logo=html5&logoColor=white" />
  <img src="https://img.shields.io/badge/CSS3-blue?logo=css3&logoColor=white" />
  <img src="https://img.shields.io/badge/JavaScript-yellow?logo=javascript&logoColor=black" />
  <img src="https://img.shields.io/badge/PWA-563D7C?logo=pwa&logoColor=white" />
  <img src="https://img.shields.io/badge/FastAPI-005571?logo=fastapi&logoColor=white" />
  <img src="https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/ONNX%20Runtime-inference-blue" />
  <img src="https://img.shields.io/badge/Status-Active-success" />
</p>

---

## ✨ What is Sila?

**Sila (صِلة)** means *connection* in Arabic — and that's exactly what this project does.

Point your camera at an Arabic Sign Language letter, and Sila translates it to text and speech **in real time**, right in your browser. No app install needed. No powerful GPU required. Just your camera and a browser.

Built as a **Progressive Web App** with a **FastAPI** inference backend and a lightning-fast **ONNX** model, Sila is designed to be accessible, open, and ready to deploy anywhere.

---

## 🚀 Features

### 🖥️ Front-End (PWA)
- 📱 **Fully responsive** — works on mobile, tablet, and desktop
- ⚡ **Service Worker** for offline support and faster loads
- 📲 **Installable** via Web App Manifest — works like a native app
- 🎥 **Live camera feed** directly in the browser

### ⚙️ Back-End (FastAPI)
- 🔌 Clean REST API with a single `/predict` endpoint
- 🔒 CORS-enabled for safe cross-origin browser requests
- 📦 Accepts Base64 or file uploads, returns instant predictions

### 🧠 Model (ONNX Runtime)
- 🏎️ Model loaded **once at startup** — near-zero latency per request
- 🖥️ CPU-first inference via **ONNX Runtime** — no GPU needed
- 🔢 Trained on **32 Arabic Sign Language letter classes**

---

## 📊 Dataset

The model was trained on the **Sila Dataset** — 32 categories covering the full Arabic Sign Language alphabet.

🔗 [View on Mendeley Data](https://data.mendeley.com/datasets/y7pckrw6z2/1)

---

## 🗂️ Project Structure

```
.
├── index.html          # Main app entry point
├── welcome.html        # Landing / onboarding page
├── styles.css          # App styles
├── script.js           # Camera capture & API integration
├── sw.js               # Service Worker (offline support)
├── manifest.json       # PWA manifest
├── logo-sila.png       # App logo
├── backend.py          # FastAPI inference server
├── model.onnx          # 👈 Place your ONNX model here
├── requirements.txt    # Python dependencies
└── README.md
```

> ⚠️ Make sure `MODEL_PATH` in `backend.py` matches your model file location (default: `"model.onnx"`).

---

## ⚡ Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/your-username/sila.git
cd sila
```

### 2. Run the Front-End

```bash
python -m http.server 5500
# Open → http://localhost:5500/
```

### 3. Run the Back-End

```bash
# Python 3.10+
pip install -r requirements.txt
uvicorn backend:app --host 0.0.0.0 --port 8000 --reload
```

That's it! Open your browser, allow camera access, and start signing. 🤟

---

## 🔗 Front-End ↔ Back-End Integration

In `script.js`, each captured frame is:

1. 📸 Converted to Base64 (PNG/JPEG)
2. 📡 Sent to `/predict` via POST request
3. 🏷️ Returned `label` displayed in the UI in real time

> 🔒 **Note:** Browsers require **HTTPS or localhost** to access the camera. Keep this in mind when deploying.

---

## 🧠 Model Notes

- Place `model.onnx` at the project root (or update `MODEL_PATH` in `backend.py`)
- Expected input format: `1 × 3 × 224 × 224` (normalized to `[0, 1]` — match your training pipeline)
- Inference flow:
  1. Load session once on startup: `onnxruntime.InferenceSession(MODEL_PATH)`
  2. Preprocess image: Resize → CenterCrop → Normalize → CHW
  3. Run `session.run(...)` → return top predicted class

---

## 📦 Deployment

| Component | Recommended Setup |
|-----------|------------------|
| 🌐 Front-End (PWA) | Nginx, Vercel, or Netlify (HTTPS required) |
| ⚙️ Back-End (FastAPI) | Uvicorn/Gunicorn behind Nginx reverse proxy |
| 🔐 SSL | Let's Encrypt (Certbot or acme.sh) |
| 🔒 CORS | Lock `allow_origins` to your production domain |

---

## 🧯 Troubleshooting

| Problem | Solution |
|---------|----------|
| 📷 Camera not working | Use HTTPS or localhost; check browser permissions |
| 🚫 CORS blocked | Add your frontend domain to `allow_origins` in `backend.py` |
| 🐢 Slow first prediction | Normal — model loads at startup. Keep the server warm |
| ❌ ONNX Runtime errors | Run `pip install onnxruntime` and verify your Python environment |

---

## 🤝 Contributing

Pull requests are welcome! If you have ideas for improving the UI, adding text-to-speech, or supporting more sign languages — open an issue and let's talk.

---

## 💙 Credits

Built with care for accessibility and inclusion.

- [FastAPI](https://fastapi.tiangolo.com/) — blazing fast Python API framework
- [ONNX Runtime](https://onnxruntime.ai/) — efficient cross-platform ML inference
- [PWA community](https://web.dev/progressive-web-apps/) — for making the web feel native

---

<p align="center">
  Made with 🤟 for the Arabic Sign Language community
</p>
