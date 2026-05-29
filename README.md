<div align="center">

# 🏙️ UrbanFix AI

**Plateforme intelligente de détection et de rénovation des espaces urbains**

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-009688?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Next.js](https://img.shields.io/badge/Next.js-14+-000000?style=flat-square&logo=next.js&logoColor=white)](https://nextjs.org/)
[![YOLOv8](https://img.shields.io/badge/YOLOv8-Detection-FF6B35?style=flat-square)](https://github.com/ultralytics/ultralytics)
[![SDXL](https://img.shields.io/badge/SDXL-LoRA-8B5CF6?style=flat-square)](https://arxiv.org/abs/2307.01952)
[![License](https://img.shields.io/badge/Licence-MIT-green?style=flat-square)](LICENSE)

> Projet de Fin d'Études · ENET'COM Sfax · Ingénierie des Données et Systèmes Décisionnels

[Démo](#pipeline-de-démo) · [Installation](#installation) · [Documentation API](#documentation) · [Architecture](#architecture)

</div>

---

## 🎯 À propos du projet

**UrbanFix AI** transforme une simple photographie d'un espace urbain dégradé en un **dossier d'aide à la décision complet**, le tout en moins de 4 minutes.

Conçu pour les municipalités tunisiennes et les citoyens, le système automatise l'ensemble du pipeline : détection des anomalies, génération de scénarios de rénovation visuels, estimation budgétaire en dinars tunisiens (TND), narration audio et production de rapports PDF professionnels.

### Problème résolu

Les collectivités locales tunisiennes s'appuient encore sur des inspections manuelles coûteuses, des rapports papier et des études de faisabilité s'étirant sur plusieurs mois. UrbanFix AI réduit ce cycle à quelques minutes, avec une interface accessible aux techniciens comme aux citoyens.

---

## ✨ Fonctionnalités

| Fonctionnalité | Technologie | Description |
|---|---|---|
| 🔍 **Détection automatique** | YOLOv8 | Identification des dégradations urbaines sur photo |
| 🎨 **Scénarios de rénovation** | SDXL + LoRA `tnrenovation` | Génération d'images photoréalistes avant/après |
| 💰 **Estimation budgétaire** | Llama 3.3 70B (Groq) | Chiffrage en dinars tunisiens par type de travaux |
| 🔊 **Narration audio** | Bark TTS | Synthèse vocale du rapport de diagnostic |
| 🎬 **Vidéo avant/après** | Pipeline vidéo | Comparaison animée de l'espace rénové |
| 📄 **Rapport PDF** | ReportLab | Dossier structuré et professionnel |
| 📡 **Suivi en temps réel** | WebSocket + FastAPI | Progression du pipeline étape par étape |

---

## 🏗️ Architecture

```
UrbanFix AI
├── backend/              # API FastAPI + services IA
│   ├── app/
│   │   ├── api/          # Endpoints REST & WebSocket
│   │   ├── services/     # YOLOv8, SDXL, Llama, Bark, PDF
│   │   └── models/       # Schémas Pydantic & ORM
│   ├── tests/            # Tests unitaires et d'intégration
│   ├── requirements.txt
│   └── API_DOCUMENTATION.md
├── frontend/             # Application Next.js 14
│   ├── app/              # App Router (pages & layouts)
│   ├── components/       # Composants réutilisables
│   └── public/
├── docs/                 # Documentation LoRA, guides techniques
│   └── SDXL_LORA_TRAINING.md
├── scripts/              # Scripts de lancement & démo (PowerShell)
│   ├── run_backend.ps1
│   ├── run_frontend.ps1
│   └── seed_demo_data.py
└── datasets/             # Données locales (non commitées, voir .gitignore)
```

> **Note :** Les dossiers `data/`, `uploads/`, `outputs/`, `temp/`, `runs/` et les poids de modèles sont exclus du dépôt Git (données volumineuses et artefacts locaux).

---

## ⚙️ Prérequis

- **OS :** Windows 10/11 avec PowerShell 5.1+
- **Python :** 3.10 ou supérieur
- **Node.js :** 18+ et npm
- **Git**
- **GPU NVIDIA** *(optionnel, recommandé pour l'inférence SDXL et YOLOv8)*

---

## 🚀 Installation

### 1. Cloner le dépôt

```bash
git clone https://github.com/<votre-username>/urbanfix-ai.git
cd urbanfix-ai
```

### 2. Backend (FastAPI)

```powershell
cd backend
python -m venv venv
.\venv\Scripts\activate
pip install -r requirements.txt
```

Créer le fichier `.env` dans `backend/` :

```env
APP_NAME=UrbanFix AI
VERSION=1.0.0
DEBUG=True
DATABASE_URL=sqlite:///./urbanfix.db
SECRET_KEY=your-secret-key-here

# Clés API externes
GROQ_API_KEY=your_groq_api_key
HUGGINGFACE_TOKEN=your_hf_token
```

> 🔑 Obtenez votre clé Groq sur [console.groq.com](https://console.groq.com) et votre token HuggingFace sur [huggingface.co/settings/tokens](https://huggingface.co/settings/tokens).

### 3. Frontend (Next.js)

```powershell
cd frontend
npm install
```

Créer le fichier `frontend/.env.local` :

```env
NEXT_PUBLIC_API_BASE_URL=http://localhost:8000/api/v1
```

---

## ▶️ Lancement en local

```powershell
# Terminal 1 — Backend
.\scripts\run_backend.ps1

# Terminal 2 — Frontend
.\scripts\run_frontend.ps1
```

| Service | URL |
|---|---|
| Interface utilisateur | http://localhost:3000 |
| API REST | http://localhost:8000 |
| Swagger UI | http://localhost:8000/docs |
| ReDoc | http://localhost:8000/redoc |

---

## 🎬 Pipeline de démo

Alimenter la base avec des données de démonstration :

```powershell
python .\scripts\seed_demo_data.py
```

Déclencher un traitement complet sur un signalement de démo :

```powershell
python .\scripts\seed_demo_data.py --run-process
```

---

## 🧪 Tests

```powershell
# Tests backend
cd backend
pytest -q

# Build de vérification frontend
cd frontend
npm run build

# Health check rapide
curl http://localhost:8000/health
```

---

## 📚 Documentation

| Ressource | Lien |
|---|---|
| Documentation API | [backend/API_DOCUMENTATION.md](backend/API_DOCUMENTATION.md) |
| Services backend | [backend/SERVICES_README.md](backend/SERVICES_README.md) |
| Guide fine-tuning LoRA SDXL | [docs/SDXL_LORA_TRAINING.md](docs/SDXL_LORA_TRAINING.md) |
| Checklist démo | [DEMO_CHECKLIST.md](DEMO_CHECKLIST.md) |
| Fix WinError 32 | [WINDOWS_WINERROR32_FIX.md](WINDOWS_WINERROR32_FIX.md) |

---

## 🤖 Modèle LoRA — `tnrenovation`

Le projet inclut un modèle LoRA fine-tuné sur SDXL, entraîné sur un dataset de 199 images d'espaces urbains tunisiens collectées via l'API Unsplash. Le trigger token `tnrenovation` oriente la génération vers les codes esthétiques de la rénovation urbaine locale.

Guide complet : [docs/SDXL_LORA_TRAINING.md](docs/SDXL_LORA_TRAINING.md)

---

## 👤 Auteur

Projet réalisé dans le cadre d'un **Projet de Fin d'année (PFA)** à l'**École Nationale d'Électronique et des Télécommunications de Sfax (ENET'COM)**, filière Ingénierie des Données et Systèmes Décisionnels.

---

## 📄 Licence

Ce projet est distribué sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.
