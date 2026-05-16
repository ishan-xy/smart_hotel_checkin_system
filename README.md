# Smart Hotel Check-In System

A real-time computer vision based hotel check-in and smart room access system using face recognition, QR-based digital keys, and access control.

## UI Preview

👉 https://checkin.gamchngr.xyz  
[ ishanx.tech expired 💔🥀🥀]

> This is **only a UI preview**.  
> The full system is designed for **local deployment**

---
## Working Demo


https://github.com/user-attachments/assets/84b73a69-400f-4dbb-9e54-b749404ff9cc

---

## Smart Lock System
<img width="1280" height="762" alt="image" src="https://github.com/user-attachments/assets/c49fec4c-b509-4c80-9733-5990f657122b" />

---

## System Architecture Diagram
<img width="1920" height="1080" alt="SYSTEM ARCHITECTURE AND FLOW" src="https://github.com/user-attachments/assets/30eff8a6-219f-4fb9-87f2-955bd91f80b0" />

---
## Features

* Face recognition based guest identification
* Automatic room assignment after check-in
* Secure QR-based temporary room keys
* Real-time camera streaming using WebRTC
* Event-driven architecture using ZMQ
* Smart lock integration with access verification
* Expiring encrypted QR access tokens

## Tech Stack

Python, FastAPI, OpenCV, dlib, MongoDB, WebRTC, ZeroMQ


## Flow

The system assumes the hotel already has the guest’s booking and face data.

At the kiosk:

* Camera recognizes the guest
* Booking details are fetched automatically
* Guest checks in through the dashboard
* Room gets assigned automatically
* A signed and encrypted temporary QR key is generated and emailed

At the room:

* Guest scans the QR code at the door
* System verifies signature + expiry
* Door unlocks only if the token is valid
  
## Setup

### 1. Install `uv`
---

### 2. Install dependencies

```bash
uv sync
```

---

### 3. Add required models

Place trained models inside:

```
models/
```

> These are **not included** because GitHub does not allow large files.

---

### 4. Environment variables

Create `.env`:

```env
MONGODB_URL=...
SMTP_USERNAME=...
SMTP_PASSWORD=...
CHECKIN_SECRET=...
```

---

## Run Services

Run each service in separate terminals:

```bash
uv run services/camera/serve_camera.py
```

```bash
python3 -m http.server 5500 -d services/ui
```

```bash
uv run services/stream_receiver/camera_recv.py
```

```bash
uv run python -m services.face_recognition.cv
```

```bash
uv run services/bridge/zmq_ws_bridge.py
```

```bash
uv run uvicorn services.api.app.main:app --reload --app-dir .
```

---
