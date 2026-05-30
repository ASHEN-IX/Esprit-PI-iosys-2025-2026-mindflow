# Study Partner – AI-Powered Study Assistance Platform

## Overview

Study Partner is an intelligent platform designed to provide personalized study guidance through a multi-agent AI system. This project was developed as part of the **PI-IOT – 4th Year Engineering Program** at **Esprit School of Engineering** (Academic Year 2025–2026).

The platform combines a full-stack web application with advanced AI agents to help students create personalized study plans, receive real-time coaching, and optimize their learning efficiency through intelligent signal processing and progress tracking.

## Features

### 🎯 Core Features
- **Personalized Study Plans**: AI-powered planner agent creates adaptive learning paths
- **Real-time Coaching**: Coach agent provides guidance, motivation, and nudges
- **Progress Evaluation**: Evaluator agent assesses performance and provides feedback
- **Focus Session Tracking**: Signal processing for monitoring learning patterns
- **Multi-Agent Orchestration**: Coordinated AI agents for comprehensive learning support
- **Gamification System**: Ranking system with tier progression (Novice → Legend)
- **Task Management**: Full task lifecycle management with progress tracking
- **Course Ingestion**: Intelligent course material processing and integration

### 🔧 Technical Capabilities
- Microservices architecture with independent scalability
- Kubernetes-ready deployment configuration
- JWT-based authentication with RBAC
- Real-time notifications and analytics
- Multi-language support for course material processing

## Tech Stack

### Frontend
- **React.js** 18+ – UI framework
- **Tailwind CSS** – Styling
- **Vite** – Build tool
- **Vitest** – Testing framework
- **Playwright** – E2E testing

### Backend
- **Node.js 20+** – Runtime
- **Express.js** – Web framework
- **MongoDB 7** – Database with Mongoose ODM
- **JWT** – Authentication (jsonwebtoken + bcryptjs)
- **Docker Compose** – Orchestration

### AI Service
- **Python 3.11+** – Runtime
- **FastAPI** – API framework
- **LLM Integration** – AI agent backbone
- **ML Models** – Fatigue detection, focus analysis
- **Poetry** – Dependency management

## Architecture

### System Overview
```
┌─────────────────────────────────────────────────────────┐
│                    Frontend (React)                      │
│              study-partner-web (Port 3000)               │
└────────────────────┬────────────────────────────────────┘
                     │
┌────────────────────▼────────────────────────────────────┐
│              API Gateway (Express)                       │
│              study-partner-api (Port 3000)               │
├─────────────────────────────────────────────────────────┤
│  ├─ Auth Service (3001)         ✓ JWT & RBAC          │
│  ├─ User Profile Service (3002) ✓ Gamification        │
│  ├─ Study Service (3003)        ✓ Tasks & Plans       │
│  ├─ AI Orchestrator (3004)      ✓ Proxy to Python AI  │
│  ├─ Signal Processing (3005)    ✓ Focus Tracking      │
│  ├─ Analytics Service (3006)    ✓ Event Tracking      │
│  └─ Notification Service (3007) ✓ In-app Alerts      │
└────────────────┬───────────────────────────────────────┘
                 │
┌────────────────▼───────────────────────────────────────┐
│           Python AI Service (FastAPI)                   │
│        study-partner-ai (Port 8000)                    │
├─────────────────────────────────────────────────────────┤
│  ├─ Planner Agent       → Personalized study plans    │
│  ├─ Coach Agent         → Real-time guidance           │
│  ├─ Evaluator Agent     → Progress assessment         │
│  ├─ Scheduler Agent     → Task scheduling             │
│  └─ Signal Processor    → ML-based insights           │
└─────────────────────────────────────────────────────────┘
         │
         ▼
    ┌─────────────┐
    │  MongoDB    │
    │  Database   │
    └─────────────┘
```

### Microservices Details

| Service | Port | Framework | Purpose |
|---------|------|-----------|---------|
| API Gateway | 3000 | Express.js | Request routing, rate limiting |
| Auth Service | 3001 | Express.js | JWT authentication & RBAC |
| User Profile | 3002 | Express.js | Profiles, gamification |
| Study Service | 3003 | Express.js | Tasks, courses, plans |
| AI Orchestrator | 3004 | Express.js | Proxy to Python AI |
| Signal Processing | 3005 | Express.js | Focus session tracking |
| Analytics Service | 3006 | Express.js | Event tracking |
| Notification Service | 3007 | Express.js | In-app notifications |
| Python AI Service | 8000 | FastAPI | ML agents, coaching |

## Contributors

This project was developed by students of **Esprit School of Engineering** as part of the PIDEV program.

## Academic Context

**Institution**: Esprit School of Engineering – Tunisia  
**Program**: PIDEV – 3rd Year Engineering  
**Academic Year**: 2025–2026  
**Course Type**: Integrated Project (Projet Intégrateur)

## Getting Started

### Prerequisites

- Node.js 18+
- Python 3.11+
- Docker and Docker Compose
- MongoDB 7+ (or use Docker image)
- npm or pnpm

### Installation & Setup

#### 1. Clone the repository
```bash
git clone <repository-url>
cd study-partner
```

#### 2. Setup Backend Services

```bash
# Install shared dependencies
cd study-partner-api/shared
npm install
cd ..

# Install all service dependencies
npm install

# Setup environment
cp .env.example .env

# Start all services with Docker Compose
docker-compose up -d
```

#### 3. Setup Frontend

```bash
cd study-partner-web

# Install dependencies
npm install

# Setup environment
cp .env.example .env

# Start development server
npm run dev
```

The frontend will be available at `http://localhost:3000`

#### 4. Setup Python AI Service

```bash
cd study-partner-ai

# Install dependencies
poetry install

# Run the service
poetry run python services/api/main.py
```

The AI service will be available at `http://localhost:8000`

### Development Commands

**Backend Services**
```bash
cd study-partner-api

# Run all services
docker-compose up

# Run specific service
docker-compose up api-gateway

# View logs
docker-compose logs -f

# Run tests
npm test
```

**Frontend**
```bash
cd study-partner-web

# Development server
npm run dev

# Build for production
npm run build

# Run tests
npm run test

# Run E2E tests
npm run test:e2e
```

**AI Service**
```bash
cd study-partner-ai

# Run tests
poetry run pytest

# Run with uvicorn
poetry run uvicorn services.api.main:app --reload --port 8000
```

## Deployment

### Docker & Kubernetes

- **Docker Compose**: Use for local development (`docker-compose.yml` and `docker-compose.prod.yml`)
- **Kubernetes**: Production deployment files available in `deploy/k8s/`

### Hosting Options

The application can be deployed to:
- **GitHub Pages**: Frontend static builds
- **Vercel**: Frontend deployment
- **Render**: Backend services
- **Railway**: Microservices
- **DigitalOcean**: Full stack deployment (via GitHub Education)

## Testing

### Backend API Tests
```bash
cd study-partner-api
npm test
npm run test:coverage
```

### Frontend Tests
```bash
cd study-partner-web
npm run test
npm run test:e2e
```

### AI Service Tests
```bash
cd study-partner-ai
poetry run pytest
poetry run pytest --cov
```

## Project Structure

```
study-partner/
├── study-partner-web/           # React frontend
│   ├── src/                     # Source code
│   ├── e2e/                     # Playwright tests
│   └── package.json
├── study-partner-api/           # Node.js microservices
│   ├── services/                # Individual services
│   ├── shared/                  # Shared utilities
│   └── package.json
├── study-partner-ai/            # Python AI service
│   ├── agents/                  # AI agents (Planner, Coach, etc.)
│   ├── services/                # AI services
│   └── pyproject.toml
├── deploy/                      # Deployment configs
│   └── k8s/                     # Kubernetes manifests
└── README.md
```

## Key Technologies & Tools

### Frontend Stack
- React 18+, Vite, Tailwind CSS, Vitest, Playwright

### Backend Stack
- Node.js 20+, Express.js, MongoDB, Mongoose, JWT, Winston

### AI Stack
- Python 3.11+, FastAPI, LLM integrations, scikit-learn

### DevOps
- Docker, Docker Compose, Kubernetes, GitHub Actions

## Acknowledgments

We acknowledge:
- **Esprit School of Engineering** for providing the educational framework and mentorship
- Our instructors and project supervisors
- The open-source community for the frameworks and libraries used
- Our peers and team members who contributed to this project

## License

This project is developed for educational purposes as part of the Esprit School of Engineering curriculum.

---

**Developed at Esprit School of Engineering – Tunisia**  
**PI-IOT – 4IOSYS | 2025–2026**
