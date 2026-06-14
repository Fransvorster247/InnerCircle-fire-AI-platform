# InnerCircle Fire AI Platform

**AI-Powered Fire Safety Compliance Automation System for South Africa**

---

## 🎯 Vision

InnerCircle Fire provides an intelligent, end-to-end fire safety compliance platform that bridges facility managers, fire service suppliers, insurance companies, and regulators. Our AI-driven system automates quote verification, work inspection, SLA tracking, risk assessment, and supplier governance—ensuring South African businesses remain compliant with SANS 10400-T, ASIB, and insurance requirements.

---

## 📋 Core Problem

**The fire compliance fragmentation crisis:**
- Facility managers manually vet supplier quotes against complex SANS standards
- No standardized verification that work was completed correctly
- Compliance certificates expire without warning
- Insurance underwriting lacks real-time risk data
- Suppliers operate without transparent performance metrics
- No single source of truth for fire safety accountability

**InnerCircle Fire solves this** through 5 intelligent AI agents that automate compliance oversight.

---

## 🏗️ System Architecture

### 5-Agent AI Orchestration

```
┌─────────────────────────────────────────┐
│     Master Orchestrator (CrewAI)        │
│  Async task routing + Shared memory     │
└──────────────┬──────────────────────────┘
               │
    ┌──────────┼──────────┬──────────┬──────────┐
    │          │          │          │          │
    ▼          ▼          ▼          ▼          ▼
┌────────┐ ┌────────┐ ┌──────┐ ┌──────┐ ┌────────┐
│  QIE   │ │  WVS   │ │ SLA  │ │ Risk │ │ Supply │
│ Quote  │ │ Work   │ │Comp. │ │Assess│ │Mgmt    │
│Engine  │ │Verif.  │ │Track │ │     │ │       │
└────────┘ └────────┘ └──────┘ └──────┘ └────────┘
    │          │          │          │          │
    └──────────┼──────────┼──────────┼──────────┘
               │
    ┌──────────▼──────────────┐
    │  SANS Standards Engine   │
    │  - Rule evaluation       │
    │  - Vector embeddings     │
    │  - Compliance scoring    │
    └──────────────────────────┘
               │
    ┌──────────▼──────────────┐
    │   PostgreSQL Database    │
    │  + Vector Store (Pinecone)
    └──────────────────────────┘
```

---

## 📖 Documentation

- **[API Specification](./docs/API_SPEC.md)**
- **[System Architecture](./docs/ARCHITECTURE.md)**
- **[SANS Standards Guide](./docs/SANS_STANDARDS_GUIDE.md)**
- **[Deployment Guide](./docs/DEPLOYMENT.md)**

---

## 🚀 Quick Start

### Prerequisites
- Python 3.10+
- PostgreSQL 14+
- OpenAI API key
- Pinecone account (vector DB)

### Installation

```bash
git clone https://github.com/Fransvorster247/InnerCircle-fire-AI-platform.git
cd InnerCircle-fire-AI-platform
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
python scripts/migrate_db.py
uvicorn api.main:app --reload
```

---

## 📊 Technology Stack

- **AI/LLM**: OpenAI GPT-4o, CrewAI
- **Vision**: YOLOv8, OpenCV
- **Backend**: FastAPI, PostgreSQL
- **ORM**: SQLAlchemy
- **Deployment**: Docker, Docker Compose

---

**Status**: Active Development | **Last Updated**: June 2026