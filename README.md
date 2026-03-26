## Smart Traffic Monitoring System
Minimal scaffold for a Raspberry Pi + OpenCV based traffic monitor with a FastAPI backend and lightweight User/Admin web panels
This project uses computer vision to detect and count vehicles using a webcam feed. It includes a FastAPI backend and a simple frontend UI to display live traffic counts.

### Features:

- Real-time object detection using Haarcascade
- Live count display
- FastAPI backend with REST endpoints
- Web interface for monitoring

### Quick start (dev, desktop)
1) Install Python 3.10+ and pip.
2) Create env and install deps:
'''
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```
3) Place a Haar cascade model (e.g., `haarcascade_car.xml`) in `models/`. Update `MODEL_PATH` in `.env` or keep the default path.
4) Run the server:
```
uvicorn server.main:app --reload
```
5) Open `web/user.html` for viewer, `web/admin.html` for admin. By default they call `http://localhost:8000`.

### Raspberry Pi notes
- Replace `CAMERA_SOURCE` with your camera index or RTSP/HTTP stream.
- Ensure `opencv-python` or `opencv-python-headless` is installed; on Pi you may prefer `opencv-python-headless`.
- Use a systemd service or pm2 to keep the FastAPI process alive; add a watchdog to restart if health checks fail.

### API (partial)
- `GET /api/health` – uptime, last frame, worker status.
- `GET /api/detections` – latest counts and objects.
- `POST /api/reload_model` – `{ "model_path": "models/haarcascade_car.xml" }`.
- `POST /api/config` – `{ "min_size": 35 }` to adjust detection thresholds.

### Next steps
- Replace Haar cascade with a modern detector; keep the `DetectionEngine` interface.
- Add persistence (Timescale/Influx) for historical trends.
- Harden stream ingestion (WebRTC/RTSP proxy) and add authentication.


How to Run

6) Install dependencies:
   pip install -r requirements.txt
7)  Run the server:
   python -m server.main
8) Open browser:
   http://127.0.0.1:3000

Note:
Detection accuracy may vary due to limitations of Haarcascade model.
