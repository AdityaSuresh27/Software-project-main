# API Endpoint Testing Document

## Overview
This document outlines the integration tests performed on the Academic Planner Backend API. The tests verify the functionality of all major endpoints, ensuring correct behavior for success and error scenarios.

**Testing Framework**: Jest + Supertest
**Database**: MongoDB (Local Test Database)
**Test Count**: 28 Tests
**Status**: ✅ All Passed

## Test Coverage

### 1. Authentication (`/api/auth`)
| Test Case | Method | Endpoint | Expected Result | Status |
|-----------|--------|----------|-----------------|--------|
| Register new user | POST | `/register` | 201 Created, Returns Token | ✅ Passed |
| prevent duplicate email | POST | `/register` | 400 Bad Request, Error Message | ✅ Passed |
| Login valid user | POST | `/login` | 200 OK, Returns Token | ✅ Passed |
| Login invalid password | POST | `/login` | 400 Bad Request, "Invalid credentials" | ✅ Passed |

### 2. Tasks (`/api/tasks`)
| Test Case | Method | Endpoint | Expected Result | Status |
|-----------|--------|----------|-----------------|--------|
| Create new task | POST | `/` | 201 Created, Returns Task | ✅ Passed |
| Validate missing title | POST | `/` | 500/400 Error | ✅ Passed |
| Get all tasks | GET | `/` | 200 OK, List of Tasks | ✅ Passed |
| Update task | PUT | `/:id` | 200 OK, Updated Task | ✅ Passed |
| Delete task | DELETE | `/:id` | 200 OK, "Task deleted" | ✅ Passed |

### 3. Events (`/api/events`)
| Test Case | Method | Endpoint | Expected Result | Status |
|-----------|--------|----------|-----------------|--------|
| Create event | POST | `/` | 201 Created | ✅ Passed |
| Get events | GET | `/` | 200 OK | ✅ Passed |
| Update event | PUT | `/:id` | 200 OK | ✅ Passed |
| Delete event | DELETE | `/:id` | 200 OK | ✅ Passed |

### 4. Timetable (`/api/timetable`)
| Test Case | Method | Endpoint | Expected Result | Status |
|-----------|--------|----------|-----------------|--------|
| Create entry | POST | `/` | 201 Created | ✅ Passed |
| Get entries | GET | `/` | 200 OK | ✅ Passed |
| Update entry | PUT | `/:id` | 200 OK | ✅ Passed |
| Delete entry | DELETE | `/:id` | 200 OK | ✅ Passed |

### 5. Attendance (`/api/attendance`)
| Test Case | Method | Endpoint | Expected Result | Status |
|-----------|--------|----------|-----------------|--------|
| Mark attendance | POST | `/` | 200 OK (Upsert) | ✅ Passed |
| Update attendance | POST | `/` | 200 OK (Updates existing) | ✅ Passed |
| Get attendance | GET | `/` | 200 OK | ✅ Passed |
| Get stats | GET | `/stats` | 200 OK, Correct Aggregation | ✅ Passed |
| Delete record | DELETE | `/:id` | 200 OK | ✅ Passed |

### 6. Categories (`/api/categories`)
| Test Case | Method | Endpoint | Expected Result | Status |
|-----------|--------|----------|-----------------|--------|
| Create category | POST | `/` | 201 Created | ✅ Passed |
| Get categories | GET | `/` | 200 OK | ✅ Passed |
| Update category | PUT | `/:id` | 200 OK | ✅ Passed |
| Delete category | DELETE | `/:id` | 200 OK | ✅ Passed |

### 7. AI Features (`/api/ai`)
| Test Case | Method | Endpoint | Expected Result | Status |
|-----------|--------|----------|-----------------|--------|
| Analyze Daily Workload | GET | `/daily` | 200 OK, Correct Minutes Calc | ✅ Passed |
| Generate Study Plan | POST | `/generate-plan` | 200 OK, Mocks Gemini API | ✅ Passed |

## How to Run Tests
To execute the test suite, run the following command in the terminal:

```bash
npm run test:integration
```

**Note**: Ensure your local MongoDB instance is running. The tests use a separate database `eduplanai_test` which is cleared before each test.
