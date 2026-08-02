<div align="center">

# 🎮 Riot Games Project

**End-to-end machine learning platform for League of Legends analytics**

FastAPI backend • React frontend • Riot API integration • MLflow experiment tracking

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-TypeScript-61DAFB?logo=react&logoColor=white)
![MLflow](https://img.shields.io/badge/MLflow-Experiment%20Tracking-0194E2?logo=mlflow&logoColor=white)
![Status](https://img.shields.io/badge/status-active-success)

![System Architecture](architecture.svg)

</div>

---

## 👥 Team

| Name | 
|------|
| Khalil Ayeb |
| Melek Bouabid |

## 🎯 Objective

Build and evaluate machine-learning models using Riot API match data to predict:

- 🏆 Match outcomes
- 🎖️ Player rank tier
- 🕵️ Smurf anomalies
- 📈 Rank progression

...while identifying which gameplay features most influence these predictions.

📄 See [`data/processed/README.md`](data/processed/README.md) for the full feature dataset schema.

---

## 📌 Progress Summary — *Feb 27, 2026*

### ✅ Achievements
- Trained and integrated **4 core prediction modules**:
  - Rank Tier Classification
  - Progression Regression
  - Smurf Anomaly Detection
  - Match Outcome Prediction (multiple variants)
- Built a production-style API layer with FastAPI (`/api/v1`)
- Connected frontend pages to live backend endpoints
- Added Riot API resilience: cache + retry/backoff + health status mapping
- Added UI/UX improvements: skeleton loading, retry cooldown, status badges, cache age & timestamps

---

## 📊 MLflow

**Current Setup**
- MLflow tracks experiments, metrics, artifacts, and model runs
- Local tracking data lives under `mlruns/`, artifacts under `mlartifacts/`
- Setup and comparison scripts in `scripts/3_model_training/`

**Run the MLflow UI**
```bash
mlflow ui --port 5000
```
Open → `http://127.0.0.1:5000`

**Key Scripts**

| Script | Purpose |
|---|---|
| `mlflow_setup.py` | Initialize experiments |
| `train_all_models.py` | Train models with tracking |
| `mlflow_model_comparison.py` | Compare runs |

---

## 🧠 Model Choice

| Model | Purpose |
|---|---|
| **Rank Tier Classifier** | Predicts rank tier from player performance features |
| **Progression Regressor** | Predicts win-rate / skill progression tendency |
| **Smurf Detector** | Anomaly-based detection of suspiciously high-skill behavior |
| **Match Outcome Predictor** | `early`, `full`, `strict`, and `cascade` variants |

**Why this choice?**
- Covers classification + regression + anomaly detection for complete player analysis
- Enables both offline evaluation and live API inference
- Match outcome variants support different feature availability windows

---

## ⚙️ FastAPI Setup

**Environment**
- Python dependencies: `requirements.txt`
- Settings source: environment variables in `.env`
- Main app entry: `api/main.py`
- Config object: `api/core/settings.py`

**Start the Backend**
```bash
.venv\Scripts\python.exe -m uvicorn api.main:app --host 127.0.0.1 --port 8001
```

| | |
|---|---|
| Base URL | `http://127.0.0.1:8001` |
| Prefix | `/api/v1` |
| Docs | `/docs` |
| OpenAPI JSON | `/openapi.json` |

---

## 🔌 Endpoints

**Health**
- `GET /api/v1/health`
- `GET /api/v1/health/riot`

**Match Outcome**
- `GET /api/v1/match-outcome/models`
- `POST /api/v1/match-outcome/predict/early`
- `POST /api/v1/match-outcome/predict/full`
- `POST /api/v1/match-outcome/predict/cascade`
- `POST /api/v1/match-outcome/predict/strict`

**Other ML Endpoints**
- `POST /api/v1/rank/predict`
- `POST /api/v1/progression/predict`
- `POST /api/v1/smurf/predict`
- `POST /api/v1/summoner/predict`

**Riot Resilience**
- ✅ Response cache for summoner prediction endpoint
- 🔁 Retry with exponential backoff for transient Riot failures
- 🩺 Health mapping for key states (active / expired / rate-limited / unreachable)

---

## 🧪 Swagger Testing

1. Start the backend server
2. Open `http://127.0.0.1:8001/docs`
3. Expand an endpoint (e.g. `POST /api/v1/rank/predict`)
4. Click **Try it out**
5. Paste a valid JSON payload
6. Click **Execute** and inspect the response + status code

**Quick Checks**
- `GET /api/v1/health`
- `GET /api/v1/match-outcome/models`
- `POST /api/v1/summoner/predict` *(requires a valid Riot API key)*

---

## 💻 Frontend

**Stack:** React + TypeScript + Vite · React Router · Recharts

**Start the Frontend**
```bash
cd "frontend/hextech-insights (1)"
npm install
npm run dev
```
Open → `http://127.0.0.1:5173`

**Recent Improvements**
- Removed duplicate summoner search UI in Live Analytics flow
- Added model-card navigation from Model Dashboard to Predictions page
- Added a compare-players page with side-by-side metrics
- Added "Why This Prediction" explainability cards
- Added loading skeletons, retry cooldown, empty states, Riot status badge, and update timestamps

---

## 🔗 Frontend ↔ Backend Integration

- Frontend API client centralized in `frontend/hextech-insights (1)/services/api.ts`
- Uses `VITE_API_BASE_URL` (default: `http://127.0.0.1:8001/api/v1`)
- Predictions and profile flows are linked to backend endpoints and typed responses

**Data Flow**
```
User action (frontend) → FastAPI endpoint → Model/service loads → Prediction payload
       → Frontend renders metrics, charts, explanations, and status indicators
```

---

## 🚀 Next Priority

- [ ] Replace expired Riot dev key with an active key to fully validate the live summoner pipeline end-to-end
- [ ] Add Docker Compose for one-command startup (backend + frontend + MLflow)

---

<div align="center">

Made with ❤️ for League of Legends analytics

</div>
