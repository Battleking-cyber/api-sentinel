<div align="center">

<img src="https://img.shields.io/badge/Python-3.11+-blue?style=for-the-badge&logo=python&logoColor=white"/>
<img src="https://img.shields.io/badge/FastAPI-0.111+-009688?style=for-the-badge&logo=fastapi&logoColor=white"/>
<img src="https://img.shields.io/badge/scikit--learn-ML-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white"/>
<img src="https://img.shields.io/badge/React-18-61DAFB?style=for-the-badge&logo=react&logoColor=black"/>
<img src="https://img.shields.io/badge/Kali_Linux-Tested-557C94?style=for-the-badge&logo=kalilinux&logoColor=white"/>
<img src="https://img.shields.io/badge/OWASP-Top_10-000000?style=for-the-badge&logo=owasp&logoColor=white"/>

# 🛡️ API Sentinel
### AI-Powered API Vulnerability Detection System

> Automatically scan REST APIs for OWASP Top 10 vulnerabilities using payload fuzzing  
> and Machine Learning anomaly detection — with a real-time React dashboard.

**[Features](#-features) • [Demo](#-demo) • [Installation](#-installation) • [Usage](#-usage) • [Architecture](#-architecture) • [ML Module](#-ai--ml-module)**

</div>

---

## 🎯 What Is This?

**API Sentinel** is a full-stack automated security tool that:

1. **Scans** any REST API endpoint with 80+ attack payloads
2. **Detects** vulnerabilities — SQL Injection, XSS, SSRF, Command Injection, Path Traversal, Broken Auth
3. **Predicts** malicious patterns using Random Forest + Isolation Forest ML models
4. **Reports** everything in a real-time React dashboard with risk scores and charts

Built as a placement/capstone project for **M.E. Cybersecurity at MSIS Manipal**.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔍 **API Scanner** | GET/POST fuzzing, header analysis, parameter injection |
| 💉 **SQLi Detection** | Error-based, union-based, time-delay (blind) |
| 🖥️ **XSS Detection** | Reflected payload detection in HTML responses |
| 🔁 **SSRF Detection** | Internal URL + AWS metadata endpoint testing |
| 💣 **Command Injection** | OS output + time-delay detection |
| 📂 **Path Traversal** | File content leakage detection |
| 🔐 **Broken Auth** | Default credential brute-force testing |
| 🤖 **AI/ML Engine** | Random Forest + Decision Tree + Isolation Forest |
| 📊 **React Dashboard** | Real-time risk scores, charts, AI anomaly alerts |
| 🗄️ **Scan Logging** | SQLite stores every request/response for retraining |
| 🔒 **Header Audit** | CSP, HSTS, X-Frame-Options, CORS checks |
| ⚡ **Rate Limit Test** | Detects missing rate limiting on endpoints |

---

## 🖥️ Demo

```
Scan ID: a3f9b12c   Target: http://127.0.0.1:9000

  [CRITICAL] sqli             → SQL Injection — DB error leaked: 'sql syntax'
  [CRITICAL] broken_auth      → Broken Authentication — default credentials accepted
  [CRITICAL] cmdi             → Command Injection — OS output detected: 'root:x:'
  [HIGH    ] xss              → XSS — payload reflected unescaped in response
  [HIGH    ] ssrf             → SSRF — server fetched internal/metadata URL
  [HIGH    ] path_traversal   → Path Traversal — file content exposed: 'root:x:'

Risk Score : 100.0 / 100 — CRITICAL
Requests   : 465
Findings   : 210
AI flagged : 89 requests as suspicious
```

---

## 📁 Project Structure

```
api-sentinel/
├── scanner/
│   ├── __init__.py
│   ├── scanner.py          # Core scanner engine
│   └── payloads.py         # 80+ attack payloads (SQLi, XSS, SSRF, etc.)
├── ml/
│   ├── __init__.py
│   └── detector.py         # Random Forest + Decision Tree + Isolation Forest
├── api/
│   ├── __init__.py
│   └── main.py             # FastAPI backend — 10+ REST endpoints
├── tests/
│   └── vuln_target.py      # Intentionally vulnerable practice API ⚠️
├── dashboard/
│   └── src/
│       └── App.jsx         # React dashboard
├── data/                   # Auto-created: SQLite DB + trained ML models
├── run_scan.py             # CLI scanner with rich terminal output
├── requirements.txt
└── README.md
```

---

## ⚙️ Installation

### Prerequisites
- Python 3.11 or higher
- Node.js 18+ (for React dashboard)
- Git

---

### 🐉 Kali Linux

```bash
# 1. Clone the repository
git clone https://github.com/Battleking-cyber/api-sentinel.git
cd api-sentinel

# 2. Create virtual environment
python3 -m venv venv
source venv/bin/activate

# 3. Install Python dependencies
pip install -r requirements.txt

# 4. Install React dashboard dependencies
cd dashboard && npm install && cd ..
```

---

### 🪟 Windows 10 / 11

```cmd
# 1. Clone the repository
git clone https://github.com/Battleking-cyber/api-sentinel.git
cd api-sentinel

# 2. Create virtual environment
python -m venv venv
venv\Scripts\activate

# 3. Install Python dependencies
pip install -r requirements.txt

# 4. Install React dashboard
cd dashboard && npm install && cd ..
```

> **Tip:** If `pip install` fails on Kali with "externally managed" error, use:
> ```bash
> pip install -r requirements.txt --break-system-packages
> ```

---

## 🚀 Usage

### Step 1 — Start the vulnerable practice target (Terminal 1)

```bash
source venv/bin/activate        # Linux
# venv\Scripts\activate         # Windows

python tests/vuln_target.py
# ⚠️  Running at http://127.0.0.1:9000  —  LOCAL TESTING ONLY
```

### Step 2 — Run the CLI scanner (Terminal 2)

```bash
source venv/bin/activate

# Basic scan
python run_scan.py

# Scan custom target
python run_scan.py --target http://127.0.0.1:9000

# Train ML models + scan
python run_scan.py --target http://127.0.0.1:9000 --train-ml

# Save report to file
python run_scan.py --target http://127.0.0.1:9000 --output report.json
```

### Step 3 — Start the FastAPI backend (Terminal 3)

```bash
source venv/bin/activate
cd api && python main.py

# API running at: http://localhost:8000
# Swagger docs:   http://localhost:8000/docs
```

### Step 4 — Start the React dashboard (Terminal 4)

```bash
cd dashboard && npm start
# Dashboard at: http://localhost:3000
```

---

## 🌐 REST API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/scan/start` | Start a new vulnerability scan |
| `GET`  | `/api/scan/status/{scan_id}` | Check scan progress |
| `GET`  | `/api/results/{scan_id}` | All results for a scan |
| `GET`  | `/api/results/{scan_id}/findings` | Only vulnerable results |
| `GET`  | `/api/stats/{scan_id}` | Vulnerability stats by type and severity |
| `GET`  | `/api/sessions` | List all past scan sessions |
| `POST` | `/api/train` | Train ML models on scan data |
| `POST` | `/api/predict/{scan_id}` | Run AI predictions on a scan |
| `GET`  | `/api/headers-check?url=` | Security header audit |
| `GET`  | `/api/rate-limit-check?url=` | Rate limiting test |
| `GET`  | `/api/health` | Health check |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────┐
│                   React Dashboard                    │
│         Risk Score · Charts · AI Alerts · Logs       │
└──────────────────────┬──────────────────────────────┘
                       │ REST API
┌──────────────────────▼──────────────────────────────┐
│                  FastAPI Backend                     │
│          Scan sessions · Results · Predict           │
└──────┬───────────────┬────────────────┬─────────────┘
       │               │                │
┌──────▼──────┐ ┌──────▼──────┐ ┌──────▼──────┐
│ API Scanner │ │  ML Module  │ │  SQLite DB  │
│  80+ payloads│ │  RF + IF    │ │ Scan logs   │
│  6 vuln types│ │  DT models  │ │ ML features │
└─────────────┘ └─────────────┘ └─────────────┘
```

---

## 🤖 AI / ML Module

Three models work in combination:

| Model | Type | Purpose | Accuracy |
|-------|------|---------|---------|
| **Random Forest** | Supervised | Classify requests as safe/vulnerable | 100% |
| **Decision Tree** | Supervised | Explainable vulnerability rules | 100% |
| **Isolation Forest** | Unsupervised | Detect anomalous request patterns | — |

### Features engineered per request (15+)

- HTTP status code, response time, response length
- Payload length, special character presence (`'`, `<`, `>`, `;`, `|`, `../`)
- Payload type encoding (SQLi=0, XSS=1, CMDi=2, SSRF=3 ...)
- Response body signals: DB error present, script tag, /etc/passwd content, AWS metadata
- Slow response flag (>4s → blind injection indicator)

### Train the models

```bash
# Train on collected scan data
python run_scan.py --train-ml

# Or via API
curl -X POST http://localhost:8000/api/train
```

---

## 🔍 Vulnerabilities Detected

| Vulnerability | Detection Method | Severity |
|---|---|---|
| SQL Injection | DB error signatures + time delay | 🔴 Critical |
| Broken Authentication | Default credential testing | 🔴 Critical |
| Command Injection | OS output + time delay | 🔴 Critical |
| XSS | Reflected payload in HTML response | 🟠 High |
| SSRF | Internal URL + AWS metadata response | 🟠 High |
| Path Traversal | File content leakage (/etc/passwd) | 🟠 High |
| Weak JWT | alg:none + weak secret brute-force | 🟠 High |
| Missing Security Headers | CSP, HSTS, X-Frame-Options, CORS | 🟡 Medium |
| No Rate Limiting | 25+ requests without 429 response | 🟡 Medium |

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Scanner | Python 3.11, `requests`, `httpx` |
| ML / AI | `scikit-learn`, `pandas`, `numpy`, `joblib` |
| Backend | `FastAPI`, `uvicorn`, `SQLite` |
| Dashboard | `React 18`, `Recharts` |
| CLI | `rich` (colored tables + progress bars) |
| Database | SQLite (auto-created in `data/`) |

---

## ⚠️ Legal & Ethical Use

> **This tool is for educational and authorized security testing only.**

- ✅ Only scan APIs you **own** or have **explicit written permission** to test
- ✅ Use `tests/vuln_target.py` for safe local practice
- ❌ Never use against production systems without authorization
- ❌ Never deploy `vuln_target.py` on a public server

Unauthorized scanning of systems you do not own is illegal under the Computer Fraud and Abuse Act (CFAA) and equivalent laws worldwide.

---

## 👤 Author

**Pankaj Arage**
- 🎓 M.E. Cybersecurity — Manipal School of Information Sciences (MSIS), Manipal
- 💼 [LinkedIn](https://linkedin.com/in/pankaj-arage-28b17721b)
- 🐙 [GitHub](https://github.com/Battleking-cyber)
- 📧 pankajarage50@gmail.com

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<div align="center">
⭐ Star this repo if it helped you! &nbsp;|&nbsp; 🍴 Fork it for your own security projects
</div>
