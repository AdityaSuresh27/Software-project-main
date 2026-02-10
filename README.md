# 🎓 ClassFlow — Intelligent Academic Planner

> A multi-platform academic planner that helps students organize coursework, track attendance, manage timetables, and generate AI-powered study plans — all in one place.

---

## 📌 What is ClassFlow?

ClassFlow is a full-stack academic planning application built as part of a Software Engineering course project. It addresses a common student pain point: **juggling multiple tools** for calendars, to-do lists, attendance tracking, and study scheduling.

Instead of switching between apps, students get a **single unified platform** available on both **web and mobile**, backed by a shared API server that keeps everything in sync.

### The Core Idea

Students often struggle with:
- Tracking class attendance and understanding where they stand percentage-wise
- Managing assignments, exams, and deadlines across multiple courses
- Creating effective study schedules that avoid burnout
- Visualizing their daily/weekly academic workload

EduPlanAI solves this by combining **task management**, **event scheduling**, **timetable management**, **attendance tracking**, and **AI-driven study plan generation** into one cohesive application.

---

## ✨ Key Features

| Feature | Description |
|---|---|
| **🔐 Authentication** | Secure user registration and login with JWT-based token authentication and bcrypt password hashing |
| **📅 Calendar & Events** | Create, view, edit, and delete academic events with priority levels, categories, and reminders |
| **📝 Task Management** | Track assignments, projects, and to-dos with status updates and deadlines |
| **🕐 Timetable** | Build a weekly class schedule with course names, instructors, rooms, and time slots |
| **📊 Attendance Tracking** | Mark daily attendance per course and view statistics (present/absent/late/excused percentages) |
| **🏷️ Categories** | Organize events and tasks into custom categories for better filtering |
| **🤖 AI Study Planner** | Uses **Google Gemini AI** to generate personalized study schedules based on your existing commitments |
| **📈 Analytics** | Daily workload analysis, overcommitment detection, procrastination analysis, and burnout risk assessment |
| **🎙️ Voice Notes** | Record and attach voice notes to events (mobile app) |
| **🌙 Dark Mode** | Full dark/light theme support across both platforms |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                          END USERS                              │
└──────────────┬──────────────────────────────┬───────────────────┘
               │                              │
       ┌───────▼────────┐            ┌────────▼────────┐
       │  Web Browser   │            │  Mobile Device  │
       │  (React + Vite)│            │  (Flutter App)  │
       └───────┬────────┘            └────────┬────────┘
               │         HTTPS / REST         │
               └──────────────┬───────────────┘
                              │
                   ┌──────────▼──────────┐
                   │   Backend API       │
                   │  Node.js / Express  │
                   └──────────┬──────────┘
                              │
              ┌───────────────┼───────────────┐
              │               │               │
     ┌────────▼─────┐ ┌──────▼──────┐ ┌──────▼──────┐
     │ MongoDB Atlas │ │ JWT Auth    │ │ Gemini API  │
     │ (Database)    │ │ (Security)  │ │ (AI Engine) │
     └──────────────┘ └─────────────┘ └─────────────┘
```

---

## 🔗 Repository Links

This project is split into **four repositories**, each handling a specific part of the system:

| Component | Repository | Description |
|---|---|---|
| 📄 **Main (Docs & DevOps)** | [AdityaSuresh27/Software-project-main](https://github.com/AdityaSuresh27/Software-project-main) | Documentation, diagrams, DevOps strategy, and testing plans |
| ⚙️ **Backend API** | [NEHANGRM/Software-Engineering-Project-Backend](https://github.com/NEHANGRM/Software-Engineering-Project-Backend) | Node.js REST API with MongoDB and Gemini AI integration |
| 🌐 **Frontend Web** | [udaykumar223/SWE_WEB](https://github.com/udaykumar223/SWE_WEB) | React 19 web application with responsive UI |
| 📱 **Frontend Mobile** | [AdityaSuresh27/Software-Engineering-Project](https://github.com/AdityaSuresh27/Software-Engineering-Project) | Flutter cross-platform mobile application |

---

## 🛠️ Tech Stack

### Backend
| Technology | Purpose |
|---|---|
| **Node.js** | Server runtime |
| **Express.js v5** | REST API framework |
| **MongoDB Atlas** | Cloud NoSQL database |
| **Mongoose** | MongoDB ODM for schema modeling |
| **JWT (jsonwebtoken)** | Token-based authentication |
| **bcryptjs** | Password hashing |
| **Helmet.js** | HTTP security headers |
| **Google Generative AI** | Gemini-powered study plan generation |
| **Jest + Supertest** | Unit and integration testing |

### Frontend Web
| Technology | Purpose |
|---|---|
| **React 19** | UI component framework |
| **Vite 7** | Build tool and dev server |
| **React Router v7** | Client-side routing |
| **Axios** | HTTP client for API calls |
| **Framer Motion** | Animations and transitions |
| **React Hook Form** | Form handling and validation |
| **React Calendar** | Calendar component |
| **React Toastify** | Toast notifications |
| **React Icons** | Icon library |
| **Vitest** | Unit testing framework |

### Frontend Mobile
| Technology | Purpose |
|---|---|
| **Flutter 3** | Cross-platform mobile framework |
| **Dart** | Programming language |
| **Provider** | State management |
| **Table Calendar** | Calendar widget |
| **SharedPreferences** | Local storage for auth tokens |
| **Google Fonts** | Typography |
| **AudioPlayers** | Voice note playback |
| **Flutter Local Notifications** | Reminder notifications |

---

## 📦 Modules

### 1. Authentication Module
- User registration with email and password
- Secure login with JWT token generation
- Password hashing with bcrypt (salt rounds: 10)
- Auth middleware protecting all private routes
- User profile retrieval (`/api/auth/me`)

### 2. Events Module
- Full CRUD operations for academic events
- Support for multiple event types (exam, assignment, lecture, etc.)
- Priority levels (low, medium, high)
- Start/end time scheduling with reminders
- Field aliasing for cross-platform compatibility

### 3. Task Management Module
- Create, read, update, and delete tasks
- Per-user task isolation (users only see their own tasks)

### 4. Timetable Module
- Build weekly class schedules
- Fields: course name, code, instructor, room, days of week, start/end times
- Semester start/end date support
- Excluded dates handling (holidays, breaks)
- Color-coded entries for visual clarity

### 5. Attendance Tracking Module
- Mark attendance per course per day (present, absent, late, excused, cancelled)
- Upsert logic prevents duplicate records for the same course+date
- Attendance statistics grouped by course
- Cancelled classes excluded from totals
- Visual percentage indicators on the frontend

### 6. Categories Module
- Create custom categories to organize events and tasks
- Per-user category management with CRUD operations

### 7. AI-Powered Analytics Module
- **Daily Workload Analysis** — aggregates events to show how loaded each day is
- **Overcommitment Detection** — flags days where you have too many commitments
- **Procrastination Analysis** — identifies patterns of task delay
- **Burnout Risk Assessment** — evaluates schedule density to warn about potential burnout
- **AI Study Plan Generator** — uses Google Gemini to create personalized study schedules based on your existing timetable, events, and preferences

---

## 🚀 Getting Started

### Prerequisites
- **Node.js** (v18 or higher)
- **npm** (v9 or higher)
- **Flutter SDK** (v3.0+) — for mobile development
- **MongoDB Atlas** account — for the database
- **Google Gemini API Key** — for AI features

### Backend Setup
```bash
git clone https://github.com/NEHANGRM/Software-Engineering-Project-Backend.git
cd Software-Engineering-Project-Backend
npm install
```

Start the server:
```bash
npm run dev
```

### Frontend Web Setup
```bash
git clone https://github.com/udaykumar223/SWE_WEB.git
cd SWE_WEB
npm install
```

Start the dev server:
```bash
npm run dev
```

### Frontend Mobile Setup
```bash
git clone https://github.com/AdityaSuresh27/Software-Engineering-Project.git
cd Software-Engineering-Project
flutter pub get
flutter run
```

---

## 🧪 Testing

| Component | Framework | Command |
|---|---|---|
| Backend | Jest + Supertest | `npm test` |
| Frontend Web | Vitest + React Testing Library | `npm test` |
| Frontend Mobile | Flutter Test | `flutter test` |


## 📁 Project Structure

```
EduPlanAI/
├── Main/Software-project-main/       # Documentation & DevOps
│   ├── README.md                     # This file
│   ├── Devops_Strategy.md            # CI/CD and deployment strategy
│   ├── Backend_Testings.md           # Backend test documentation
│   ├── FrontendWeb_Testings.md       # Frontend web test documentation
│   └── Diagrams/                     # Architecture and flow diagrams
│
├── Backend-Mobile/Software-Engineering-Project-Backend/
│   ├── index.js                      # Express server entry point
│   ├── controllers/                  # Route handler logic
│   ├── models/                       # Mongoose schemas
│   ├── routes/                       # API route definitions
│   ├── middleware/                    # Auth middleware
│   └── tests/                        # Jest unit tests
│
├── SWE_WEB/                          # React web application
│   ├── src/pages/                    # Page components
│   ├── src/components/               # Reusable UI components
│   ├── src/services/                 # API service layer
│   └── src/context/                  # React context providers
│
└── Frontend-Mobile/Software-Engineering-Project/
    └── lib/
        ├── frontend/                 # Flutter UI screens
        ├── backend/                  # API service layer
        └── main.dart                 # App entry point
```

---

## 🤝 Team

This project was developed as part of a **Software Engineering** course to demonstrate full-stack development, DevOps practices, and collaborative software design.

Teammates:

-- Aditya Suresh - Frontend/Backend Engineer - https://github.com/AdityaSuresh27
-- Nehan GRM - Devops Engineer - https://github.com/NEHANGRM
-- Uday Kumar - Frontend Engineer - https://github.com/udaykumar223
-- Shruthilaya AV - Backend Engineer - https://github.com/ShruthilayaAV
-- Tejeshwara Reddy Dareddy - Testing Engineer - https://github.com/TejeswaraReddy-Dareddy


## 📄 License

[MIT](https://choosealicense.com/licenses/mit/)

