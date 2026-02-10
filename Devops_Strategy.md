# DevOps Strategy — Intelligent Academic Planner (EduPlanAI)

## 1. Project Overview

The Intelligent Academic Planner is a multi-platform application consisting of four components:

| # | Component | Technology Stack |
|---|-----------|-----------------|
| 1 | **Backend API** | Node.js, Express.js, MongoDB Atlas, Mongoose |
| 2 | **Frontend Web** | React 19, Vite, Axios, React Router |
| 3 | **Frontend Mobile** | Flutter, Dart |
| 4 | **Main Repository** | Documentation & DevOps configuration |

---

## 2. Source Code Repositories

Each component is maintained in its own Git repository:

| Component | GitHub Repository | Branch Strategy |
|-----------|-------------------|-----------------|
| **Backend API** | [NEHANGRM/Software-Engineering-Project-Backend](https://github.com/NEHANGRM/Software-Engineering-Project-Backend) | `main` (production), feature branches for development |
| **Frontend Web** | [udaykumar223/SWE_WEB](https://github.com/udaykumar223/SWE_WEB) | `main` (production), feature branches for development |
| **Frontend Mobile** | [AdityaSuresh27/Software-Engineering-Project](https://github.com/AdityaSuresh27/Software-Engineering-Project) | `main` (production), feature branches for development |
| **Main (Docs/DevOps)** | [AdityaSuresh27/Software-project-main](https://github.com/AdityaSuresh27/Software-project-main) | `main` |

---

## 3. Deployment Strategy

### 3.1 Backend API

| Aspect | Details |
|--------|---------|
| **Deployment Platform** | Render / Railway (Cloud PaaS) |
| **Database** | MongoDB Atlas (Cloud-hosted cluster) |
| **Runtime** | Node.js |
| **Entry Point** | `index.js` |
| **Port** | 5000 (configurable via `PORT` environment variable) |
| **Environment Variables** | `MONGODB_URI`, `JWT_SECRET`, `GEMINI_API_KEY`, `PORT` |
| **Deployment Trigger** | Push to `main` branch triggers automatic deployment |

### 3.2 Frontend Web

| Aspect | Details |
|--------|---------|
| **Deployment Platform** | Vercel / Netlify (Static hosting with CDN) |
| **Build Tool** | Vite |
| **Build Command** | `npm run build` |
| **Output Directory** | `dist/` |
| **Environment Variables** | `VITE_API_URL` (points to deployed backend URL) |
| **Deployment Trigger** | Push to `main` branch triggers automatic build and deployment |

### 3.3 Frontend Mobile

| Aspect | Details |
|--------|---------|
| **Platform** | Android (APK) / iOS |
| **Build Tool** | Flutter SDK |
| **Build Command** | `flutter build apk --release` |
| **Distribution** | Manual APK distribution / Google Play Store (future) |
| **API Configuration** | Backend URL configured in app's API service layer |

---

## 4. Testing & Pre-Deployment Checks

### 4.1 Backend API

| Test Type | Tool / Library | Command | Description |
|-----------|---------------|---------|-------------|
| **Unit Tests** | Jest | `npm test` | Tests for controllers (auth, events, tasks, attendance) and models |
| **Integration Tests** | Jest + Supertest | `npm test` | API endpoint testing with HTTP assertions |
| **Linting** | ESLint | `npx eslint .` | Code quality and style enforcement |
| **Security Audit** | npm audit | `npm audit` | Checks for known vulnerabilities in dependencies |

### 4.2 Frontend Web

| Test Type | Tool / Library | Command | Description |
|-----------|---------------|---------|-------------|
| **Linting** | ESLint | `npm run lint` | Code quality enforcement for React components |
| **Build Verification** | Vite | `npm run build` | Ensures production build compiles without errors |
| **Dependency Audit** | npm audit | `npm audit` | Checks for known vulnerabilities |

### 4.3 Frontend Mobile

| Test Type | Tool / Library | Command | Description |
|-----------|---------------|---------|-------------|
| **Unit Tests** | Flutter Test | `flutter test` | Widget and logic unit testing |
| **Build Verification** | Flutter SDK | `flutter build apk` | Ensures APK builds successfully |
| **Static Analysis** | Dart Analyzer | `flutter analyze` | Code quality and type checking |

---

## 5. CI/CD Pipeline Strategy

### 5.1 Pipeline Overview

```
Developer Push → GitHub → CI Pipeline → Tests → Build → Deploy
```

### 5.2 CI/CD Tool

**GitHub Actions** is used as the CI/CD platform for all repositories.

### 5.3 Backend CI/CD Workflow

```yaml
# Trigger: Push to main branch
# Steps:
#   1. Checkout code
#   2. Setup Node.js environment
#   3. Install dependencies (npm ci)
#   4. Run linting (eslint)
#   5. Run unit & integration tests (npm test)
#   6. Run security audit (npm audit)
#   7. Deploy to Render/Railway (if all checks pass)
```

### 5.4 Frontend Web CI/CD Workflow

```yaml
# Trigger: Push to main branch
# Steps:
#   1. Checkout code
#   2. Setup Node.js environment
#   3. Install dependencies (npm ci)
#   4. Run linting (npm run lint)
#   5. Build production bundle (npm run build)
#   6. Deploy to Vercel/Netlify (if build succeeds)
```

### 5.5 Frontend Mobile CI/CD Workflow

```yaml
# Trigger: Push to main branch
# Steps:
#   1. Checkout code
#   2. Setup Flutter SDK
#   3. Install dependencies (flutter pub get)
#   4. Run static analysis (flutter analyze)
#   5. Run unit tests (flutter test)
#   6. Build release APK (flutter build apk --release)
#   7. Upload APK artifact
```

---

## 6. Tools, Platforms & Libraries Summary

| Category | Tool / Platform | Purpose |
|----------|----------------|---------|
| **Version Control** | Git + GitHub | Source code management and collaboration |
| **CI/CD** | GitHub Actions | Automated testing and deployment pipelines |
| **Backend Hosting** | Render / Railway | Cloud deployment for Node.js API server |
| **Frontend Hosting** | Vercel / Netlify | Static site hosting with auto-deploy from Git |
| **Database** | MongoDB Atlas | Cloud-hosted NoSQL database |
| **Backend Framework** | Express.js (v5) | REST API framework |
| **Frontend Framework** | React 19 + Vite | Web SPA framework and build tool |
| **Mobile Framework** | Flutter + Dart | Cross-platform mobile app framework |
| **Authentication** | JWT (jsonwebtoken) + bcryptjs | Token-based auth with password hashing |
| **AI Integration** | Google Gemini API (@google/generative-ai) | AI-powered study plan generation |
| **HTTP Client** | Axios | Frontend-to-backend API communication |
| **Testing (Backend)** | Jest + Supertest | Unit and integration testing |
| **Testing (Web)** | ESLint | Linting and static analysis |
| **Testing (Mobile)** | Flutter Test + Dart Analyzer | Unit testing and static analysis |
| **Security** | Helmet.js + npm audit | HTTP header security + vulnerability scanning |
| **API Documentation** | Postman (manual) | API endpoint testing and documentation |

---

## 7. Environment Management

| Environment | Backend URL | Database | Purpose |
|-------------|-------------|----------|---------|
| **Development** | `http://localhost:5000/api` | MongoDB Atlas (shared dev cluster) | Local development and testing |
| **Production** | Deployed URL (Render/Railway) | MongoDB Atlas (production cluster) | Live application serving end users |

---

## 8. Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                        END USERS                                │
└──────────────┬──────────────────────────────┬───────────────────┘
               │                              │
       ┌───────▼────────┐            ┌────────▼────────┐
       │  Web Browser   │            │  Mobile Device  │
       │  (React + Vite)│            │  (Flutter App)  │
       │  Vercel/Netlify│            │  APK Install    │
       └───────┬────────┘            └────────┬────────┘
               │         HTTPS / REST         │
               └──────────────┬───────────────┘
                              │
                   ┌──────────▼──────────┐
                   │   Backend API       │
                   │   (Node.js/Express) │
                   │   Render / Railway  │
                   │   Port: 5000        │
                   └──────────┬──────────┘
                              │
              ┌───────────────┼───────────────┐
              │               │               │
     ┌────────▼─────┐ ┌──────▼──────┐ ┌──────▼──────┐
     │ MongoDB Atlas │ │ JWT Auth    │ │ Gemini API  │
     │ (Database)    │ │ (Security)  │ │ (AI Engine) │
     └──────────────┘ └─────────────┘ └─────────────┘
```
