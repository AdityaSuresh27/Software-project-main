# Unit Testing Documentation

## Overview
This document details the unit tests implemented for the Academic Planner Backend. Unlike the integration tests, these tests focus on isolating the controller logic by mocking the database layer (Mongoose models) and external services (Google Gemini API).

**Testing Framework**: Jest + Supertest (Mocked Models)
**Test Count**: 26 Tests
**Status**: ✅ All Passed

## Test Strategy
- **Controllers Tested**: `TaskController`, `EventController`, `CategoryController`, `AIController`.
- **Mocking**:
  - `Mongoose Models`: All database operations (`find`, `save`, `findByIdAndUpdate`, etc.) are mocked using `jest.mock`.
  - `Auth Middleware`: Authentication is bypassed by mocking the middleware to inject a test user (`mockUserId`).
  - `External Services`: Google Generative AI is mocked to prevent real API calls and ensure deterministic results.
- **Request Simulation**: `supertest` is used to simulate HTTP requests to the express app, verifying the controller's response structure and status codes.

## Test Coverage

### 1. Task Controller (`tests/unit/taskController.unit.test.js`)
| Function | Scenario | Expected Result | Status |
|----------|----------|-----------------|--------|
| `getTasks` | Fetch all tasks | 200 OK, Returns tasks array | ✅ Passed |
| `getTasks` | Database Error | 500 Internal Server Error | ✅ Passed |
| `createTask` | Create valid task | 201 Created, Validates data | ✅ Passed |
| `createTask` | Save Error | 500 Internal Server Error | ✅ Passed |
| `updateTask` | Update existing task | 200 OK, Returns updated task | ✅ Passed |
| `deleteTask` | Delete existing task | 200 OK, Confirmation message | ✅ Passed |

### 2. Event Controller (`tests/unit/eventController.unit.test.js`)
| Function | Scenario | Expected Result | Status |
|----------|----------|-----------------|--------|
| `createEvent` | Standard fields | 201 Created | ✅ Passed |
| `createEvent` | Field Aliasing (e.g. `startDate` -> `startTime`) | 201 Created, Maps fields correctly | ✅ Passed |
| `createEvent` | Missing `startTime` | 400 Bad Request | ✅ Passed |
| `getEvents` | Fetch all events | 200 OK | ✅ Passed |
| `updateEvent` | Update success | 200 OK | ✅ Passed |
| `updateEvent` | Not Found | 404 Not Found | ✅ Passed |
| `deleteEvent` | Delete success | 200 OK | ✅ Passed |

### 3. Category Controller (`tests/unit/categoryController.unit.test.js`)
| Function | Scenario | Expected Result | Status |
|----------|----------|-----------------|--------|
| `getCategories` | Fetch categories | 200 OK | ✅ Passed |
| `createCategory` | Create new | 201 Created | ✅ Passed |
| `updateCategory` | Update success | 200 OK | ✅ Passed |
| `updateCategory` | Not Found | 404 Not Found | ✅ Passed |
| `deleteCategory` | Delete success | 200 OK | ✅ Passed |

### 4. AI Controller (`tests/unit/aiController.unit.test.js`)
| Function | Scenario | Expected Result | Status |
|----------|----------|-----------------|--------|
| `getDailyWorkload` | Calculate minutes | 200 OK, Correct Totals | ✅ Passed |
| `getDailyWorkload` | No events | 200 OK, 0 minutes | ✅ Passed |
| `generateStudyPlan` | Generate Plan | 200 OK, Returns Mocked AI Response | ✅ Passed |
| `generateStudyPlan` | Missing API Key | 500 Error | ✅ Passed |
| `generateStudyPlan` | AI Service Error | 500 Error | ✅ Passed |
| `checkOvercommitment` | Workload > 8h | 200 OK, Returns Warning | ✅ Passed |
| `analyzeProcrastination` | Missed Deadlines | 200 OK, Returns Score | ✅ Passed |

## How to Run Unit Tests
To execute the unit test suite, run the following command:

```bash
npm run test:unit
```
