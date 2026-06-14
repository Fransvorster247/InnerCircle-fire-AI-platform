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

### 5 AI Agents

| Agent | Purpose | Key Technology | Output |
|-------|---------|-----------------|--------|
| **QIE** (Quote Intelligence Engine) | Parse supplier quotes; cross-ref SANS standards; benchmark pricing | GPT-4o, embeddings, rule engine | Quote compliance report, pricing flags |
| **WVS** (Work Verification System) | Validate photo/test uploads; computer vision inspection; quality scoring | YOLOv8, EXIF validation, IoT integration | Work completion certificate, quality score |
| **SLA** (SLA & Compliance Dashboard) | Track certificate expiry; supplier performance; escalation alerts | Time-series DB, scoring algorithm | Compliance dashboard, supplier scorecards |
| **Risk** (Risk Assessment Engine) | 5-dimensional risk scoring; insurance readiness grading; remediation prioritization | Risk matrix, weighting algorithm | Risk score (1-100), insurance grade (A-F) |
| **Supply** (Supplier Marketplace) | Match suppliers by specialty/location/performance; SLA template generation | Multi-dimensional matching, NLP | Supplier recommendations, SLA templates |

---

## 📂 Project Structure

```
innercircle-fire-platform/
├── config/                    # Configuration layer (Pydantic settings, SANS standards)
├── database/                  # SQLAlchemy ORM models + Alembic migrations
├── agents/                    # 5 CrewAI agents + orchestrator
│   ├── orchestrator.py        # Master task router
│   ├── qie_agent/             # Quote Intelligence Engine
│   ├── wvs_agent/             # Work Verification System
│   ├── sla_agent/             # SLA & Compliance Dashboard
│   ├── risk_agent/            # Risk Assessment Engine
│   └── supply_agent/          # Supplier Marketplace
├── standards/                 # SANS standards engine
├── api/                       # FastAPI REST API
├── ml_models/                 # YOLOv8, embeddings, model caching
├── external_apis/             # OpenAI, IoT, Stripe integrations
├── tests/                     # Comprehensive test suite
├── scripts/                   # DB migrations, data seeding
└── docs/                      # API spec, architecture, deployment
```

---

## 🚀 Quick Start

### Prerequisites
- Python 3.10+
- PostgreSQL 14+
- OpenAI API key (GPT-4o)
- Pinecone or Weaviate account (vector DB)

### Installation

```bash
# Clone repository
git clone https://github.com/Fransvorster247/InnerCircle-fire-AI-platform.git
cd InnerCircle-fire-AI-platform

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Copy environment template
cp .env.example .env
# Edit .env with your API keys, DB credentials, etc.

# Run database migrations
python scripts/migrate_db.py

# Seed SANS standards data
python scripts/seed_standards.py

# Start API server
uvicorn api.main:app --reload --host 0.0.0.0 --port 8000
```

### Docker Compose

```bash
docker-compose up -d
```

---

## 📡 API Endpoints (Core)

### Quote Analysis (QIE)
```
POST /api/quotes/analyze
{
  "supplier_id": "SUP-001",
  "building_id": "BLD-001",
  "quote_file": <PDF>,
  "quote_amount": 45000
}
Response:
{
  "quote_id": "QT-001",
  "compliance_flags": [...],
  "scope_gaps": [...],
  "pricing_benchmark": {...},
  "recommendation": "APPROVED_WITH_NOTES"
}
```

### Work Verification (WVS)
```
POST /api/verification/submit
{
  "work_order_id": "WO-001",
  "photos": [<image>],
  "test_results": {...},
  "completion_certificate": <PDF>
}
Response:
{
  "verification_id": "VER-001",
  "quality_score": 94.5,
  "cv_findings": {...},
  "status": "APPROVED"
}
```

### SLA Dashboard (SLA)
```
GET /api/sla/dashboard?building_id=BLD-001
Response:
{
  "certificates": [...],
  "expiry_alerts": [...],
  "supplier_scorecards": [...],
  "escalations": [...]
}
```

### Risk Assessment (Risk)
```
GET /api/risk/assessment?building_id=BLD-001
Response:
{
  "risk_score": 68,
  "insurance_grade": "B+",
  "dimensions": {
    "building_characteristics": 75,
    "occupancy_risk": 65,
    "system_integrity": 70,
    "maintenance_status": 60,
    "compliance_history": 72
  },
  "remediation_priority": [...]
}
```

### Supplier Matching (Supply)
```
GET /api/suppliers/match?specialty=SPRINKLERS&location=GAUTENG&budget=50000
Response:
{
  "matches": [...],
  "sla_template": {...}
}
```

---

## 🔐 Security & Compliance

- **Authentication**: JWT tokens for API access
- **Data Encryption**: AES-256 for sensitive data at rest
- **Audit Logging**: All compliance actions logged with timestamps
- **GDPR/POPIA**: Data retention policies, consent management
- **Compliance Validation**: SANS 10400-T, ASIB, insurance alignment

---

## 📊 Technology Stack

| Layer | Technology |
|-------|-----------|
| **AI/LLM** | OpenAI GPT-4o, LangChain, CrewAI |
| **Vision** | YOLOv8, OpenCV, Pillow |
| **Backend** | FastAPI, Uvicorn, Async Python |
| **Database** | PostgreSQL (relational), Pinecone (vector) |
| **ORM** | SQLAlchemy |
| **Configuration** | Pydantic, Python-dotenv |
| **Testing** | Pytest, Pytest-asyncio |
| **Deployment** | Docker, Docker Compose |
| **CI/CD** | GitHub Actions (coming soon) |

---

## 📖 Documentation

- **[API Specification](./docs/API_SPEC.md)** — OpenAPI/Swagger endpoints
- **[Database Schema](./docs/DATABASE_SCHEMA.md)** — Entity relationships
- **[System Architecture](./docs/ARCHITECTURE.md)** — Detailed design
- **[SANS Standards Guide](./docs/SANS_STANDARDS_GUIDE.md)** — Regulatory mapping
- **[Deployment Guide](./docs/DEPLOYMENT.md)** — Production setup
- **[Troubleshooting](./docs/TROUBLESHOOTING.md)** — Common issues

---

## 🧪 Testing

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=. --cov-report=html

# Run specific test file
pytest tests/test_qie_agent.py -v

# Run tests matching pattern
pytest -k "quote" -v
```

---

## 🤝 Contributing

1. Create feature branch: `git checkout -b feature/your-feature`
2. Commit changes: `git commit -m "Add your feature"`
3. Push to branch: `git push origin feature/your-feature`
4. Open Pull Request

---

## 📋 Roadmap

**Phase 1 (MVP - Q3 2026)**
- ✅ QIE Agent (quote parsing, SANS matching)
- ✅ SLA Dashboard (certificate tracking)
- ✅ Core API & database

**Phase 2 (Q4 2026)**
- WVS Agent (computer vision, photo verification)
- Risk Assessment Engine
- Supplier Marketplace

**Phase 3 (Q1 2027)**
- Insurance partnership APIs
- Advanced analytics & reporting
- Mobile app

---

## 👥 Team

- **Founder/CEO**: Frans Vorster (Business Strategy, Regulatory)
- **CTO**: [Engineering Lead] (AI/ML, Architecture)
- **Product Lead**: [Product Manager] (UX, Feature prioritization)

---

## 📞 Support

- **Email**: support@innercirclefire.co.za
- **Issues**: [GitHub Issues](https://github.com/Fransvorster247/InnerCircle-fire-AI-platform/issues)
- **Documentation**: [Wiki](https://github.com/Fransvorster247/InnerCircle-fire-AI-platform/wiki)

---

## 📄 License

Proprietary - InnerCircle Fire (Pty) Ltd. All rights reserved.

---

## 🙏 Acknowledgments

- SABS (South African Bureau of Standards) - SANS 10400-T guidance
- ASIB (Association of Sprinkler Installation Bodies) - Technical standards
- SA Fire Industry Council - Market insights

---

**Last Updated**: June 2026  
**Status**: Active Development
