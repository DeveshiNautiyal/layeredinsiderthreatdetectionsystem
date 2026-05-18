Layered Insider Threat Detection System
A production-grade, AI-powered insider threat detection system that combines behavioral analytics, meta-learning, and adversarial evasion resilience to identify malicious insider activity in real time.
Live Demo: https://threat-dashboard-integrated.vercel.app
GitHub: https://github.com/DeveshiNautiyal/layeredinsiderthreatdetectionsystem

Table of Contents

Overview
Architecture
Features
Tech Stack
Project Structure
Installation
Usage
API Reference
Dashboard
Model Details
Author


Overview
Insider threats are among the most damaging and difficult-to-detect cybersecurity risks. Unlike external attackers, insiders have legitimate access and deep knowledge of organizational systems, making signature-based detection methods ineffective.
This system addresses that gap using a layered detection pipeline that models normal user behavior, detects anomalies using machine learning, adapts to novel threat patterns through meta-learning, and remains robust against adversarial evasion attempts.
The system is designed for enterprise environments and outputs actionable alerts through a real-time React dashboard deployed on Vercel.

Architecture
The system is built around four detection layers, each targeting a different aspect of insider threat behavior.
Raw User Activity Logs
        |
        v
+-------------------------+
|   Data Pipeline         |
|  (data_pipeline.py)     |
|  - Log ingestion        |
|  - Feature extraction   |
|  - Normalization        |
+-------------------------+
        |
        v
+-------------------------+
|   Layer 1: UEBA         |
|  (baseline_ueba.py)     |
|  - Isolation Forest     |
|  - Statistical baseline |
|  - Behavioral profiling |
+-------------------------+
        |
        v
+-------------------------+
|   Layer 2: Meta-Learning|
|  (meta_detection.py)    |
|  - MAML-style adaptation|
|  - Few-shot detection   |
|  - Novel threat patterns|
+-------------------------+
        |
        v
+-------------------------+
|   Layer 3: Adversarial  |
|  (adversarial_evasion.py|
|  - Evasion detection    |
|  - Drift monitoring     |
|  - Robustness checks    |
+-------------------------+
        |
        v
+-------------------------+
|   Backend API           |
|  (backend_api.py)       |
|  - FastAPI REST layer   |
|  - Alert aggregation    |
|  - Risk scoring         |
+-------------------------+
        |
        v
+-------------------------+
|   React Dashboard       |
|  (react_dashboard.jsx)  |
|  - Real-time alerts     |
|  - Risk visualization   |
|  - User behavior charts |
+-------------------------+
Layer Descriptions
Layer 1 - User and Entity Behavior Analytics (UEBA):
Establishes a behavioral baseline for each user using Isolation Forest and statistical profiling. Flags deviations from normal patterns such as unusual login times, data volume spikes, or access to restricted resources.
Layer 2 - Meta-Learning Detection:
Uses a MAML-inspired (Model-Agnostic Meta-Learning) approach to rapidly adapt to new and previously unseen threat patterns with minimal labeled examples. This makes the system effective even against novel insider threat tactics.
Layer 3 - Adversarial Evasion Resilience:
Monitors for adversarial behavior where an insider deliberately tries to blend in or evade detection by slowly changing their behavior over time (low-and-slow attacks). Detects concept drift and applies robustness checks.
Backend API:
A FastAPI-based REST layer that aggregates signals from all three detection layers, computes a unified risk score per user, and exposes endpoints for the dashboard and external integrations.
React Dashboard:
A live, interactive dashboard deployed at https://threat-dashboard-integrated.vercel.app showing real-time alerts, risk scores, behavioral timelines, and exportable reports.

Features

Multi-layer detection combining rule-based, ML, and meta-learning approaches
Real-time risk scoring per user with alert severity levels (Low, Medium, High, Critical)
Behavioral profiling that adapts to each individual user's normal patterns
Adversarial evasion detection for low-and-slow insider attacks
Few-shot learning to detect novel threats with minimal training data
FastAPI backend with clean REST endpoints
React dashboard with live data, charts, and alert exports
Modular architecture where each layer can be used independently
JSON export of alerts and results for SIEM integration


Tech Stack
Backend:

Python 3.10+
FastAPI
Scikit-learn (Isolation Forest, preprocessing)
NumPy, Pandas
Uvicorn (ASGI server)

Frontend:

React 18
Vite
Recharts (data visualization)
Deployed on Vercel

Machine Learning:

Isolation Forest for anomaly detection
MAML-style meta-learning for few-shot adaptation
Adversarial robustness via behavioral drift monitoring


Project Structure
layeredinsiderthreatdetectionsystem/
|
+-- insider_threat_detection_complete (2)/
|   +-- insider_threat_detection_complete/
|       +-- insider_threat_detection/
|           +-- main.py                  # Entry point, orchestrates all layers
|           +-- backend_api.py           # FastAPI REST API
|           +-- backend_simple.py        # Simplified backend for testing
|           +-- data_pipeline.py         # Data ingestion and feature engineering
|           +-- baseline_ueba.py         # Layer 1: UEBA anomaly detection
|           +-- meta_detection.py        # Layer 2: Meta-learning detection
|           +-- adversarial_evasion.py   # Layer 3: Evasion resilience
|           +-- react_dashboard.jsx      # Frontend dashboard component
|           +-- test_quick.py            # Quick test script
|           +-- requirements.txt         # Python dependencies
|           +-- results.json             # Detection results output
|           +-- alerts_export.json       # Exported alerts
|           +-- runtime.txt              # Runtime configuration
|           +-- data/                    # Input data directory
|           +-- README.md                # This file
|
+-- threat-dashboard-integrated/
    +-- threat-dashboard-integrated/
        +-- src/                         # React source files
        +-- dist/                        # Production build
        +-- .vercel/                     # Vercel deployment config

Installation
Prerequisites

Python 3.10 or higher
Node.js 18 or higher
pip

Backend Setup
bash# Clone the repository
git clone https://github.com/DeveshiNautiyal/layeredinsiderthreatdetectionsystem.git
cd layeredinsiderthreatdetectionsystem

# Navigate to the detection module
cd "insider_threat_detection_complete (2)/insider_threat_detection_complete/insider_threat_detection"

# Create a virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # Mac/Linux

# Install dependencies
pip install -r requirements.txt

# Run the system
python main.py
Frontend Setup
bashcd threat-dashboard-integrated/threat-dashboard-integrated

# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

Usage
Running the Full Detection Pipeline
bashpython main.py
This runs all three detection layers on the data in the data/ folder and outputs results to results.json and alerts_export.json.
Running the API Server
bashuvicorn backend_api:app --reload --port 8000
The API will be available at http://localhost:8000
Quick Test
bashpython test_quick.py
Runs a quick validation of all detection layers with sample data.

API Reference
GET /alerts
Returns all current alerts sorted by severity.
GET /risk-scores
Returns risk scores for all monitored users.
GET /user/{user_id}/behavior
Returns behavioral profile and anomaly history for a specific user.
POST /analyze
Submits new activity logs for real-time analysis.
GET /export
Exports current alerts as a downloadable JSON file.

Dashboard
The live dashboard is deployed at:
https://threat-dashboard-integrated.vercel.app
Features available on the dashboard:

Real-time alert feed with severity indicators
Per-user risk score timeline
Behavioral anomaly charts
Detection layer breakdown showing which layer triggered each alert
Exportable alert reports in JSON format
Filter alerts by severity, user, time range, or detection layer


Model Details
Isolation Forest (Layer 1)

Contamination factor: 0.05 (assumes 5% of activity is anomalous)
Features: login time, session duration, data volume, resource access count, failed attempts
Output: anomaly score per session

Meta-Learning Detector (Layer 2)

Inspired by Model-Agnostic Meta-Learning (MAML)
Adapts to new threat classes with as few as 5 labeled examples
Uses task-specific fine-tuning on behavioral embeddings

Adversarial Evasion Detector (Layer 3)

Monitors for behavioral drift over sliding time windows
Detects gradual evasion strategies that bypass Layer 1
Uses statistical drift tests (KS test, CUSUM) to flag slow behavioral shifts


Author
Deveshi Nautiyal
GitHub: https://github.com/DeveshiNautiyal
Project: https://github.com/DeveshiNautiyal/layeredinsiderthreatdetectionsystem
Live Demo: https://threat-dashboard-integrated.vercel.app
