# Contributing to API Sentinel

Thank you for your interest in contributing! Here's how to get started.

## 🚀 Getting Started

1. Fork the repository
2. Clone your fork:
   ```bash
   git clone https://github.com/YOUR-USERNAME/api-sentinel.git
   cd api-sentinel
   ```
3. Create a virtual environment and install dependencies:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt
   ```
4. Create a new branch for your feature:
   ```bash
   git checkout -b feature/your-feature-name
   ```

## 🛠️ Ways to Contribute

- **Add new payloads** — Add attack payloads to `scanner/payloads.py`
- **Add new vulnerability checks** — Extend `scanner/scanner.py`
- **Improve ML models** — Improve feature engineering in `ml/detector.py`
- **Fix bugs** — Check the Issues tab
- **Improve docs** — Fix typos, add examples

## 📋 Pull Request Process

1. Make your changes
2. Test against the vuln target: `python run_scan.py --target http://127.0.0.1:9000`
3. Commit with a clear message: `git commit -m "Add: SSRF bypass via URL encoding"`
4. Push and open a Pull Request

## ⚠️ Security Note

Only add payloads for **known, documented vulnerabilities**.  
Never add payloads designed to harm real systems or users.
