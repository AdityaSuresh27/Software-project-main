# Unit Testing Documentation

## Overview
This document details the unit tests implemented for the Academic Planner Backend. Unlike the integration tests, these tests focus on isolating the controller logic by mocking the database layer (Mongoose models) and external services (Google Gemini API).

**Testing Framework**: Jest + Supertest (Mocked Models)
**Test Count**: 58 Tests
**Status**: ✅ All Passed

## Test Strategy
- **Controllers Tested**: `TaskController`, `EventController`, `CategoryController`, `AIController`, `AuthController`, `AttendanceController`, `TimetableController`.
- **Middleware Tested**: `AuthMiddleware`.
- **Mocking**:
  - `Mongoose Models`: All database operations (`find`, `save`, `findByIdAndUpdate`, etc.) are mocked using `jest.mock`.
  - `Auth Middleware`: Authentication is bypassed by mocking the middleware to inject a test user (`mockUserId`).
  - `External Services`: Google Generative AI is mocked to prevent real API calls and ensure deterministic results.
- **Request Simulation**: `supertest` is used to simulate HTTP requests to the express app, verifying the controller's response structure and status codes.

## Test Coverage

### 1. Auth Controller (`tests/authController.test.js`)
| Function | Scenario | Expected Result | Status |
|----------|----------|-----------------|--------|
| `register` | Register new user | 201 Created, Returns token & user | ✅ Passed |
| `register` | Email already exists | 400 Bad Request | ✅ Passed |
| `login` | Correct credentials | 200 OK, Returns token & user | ✅ Passed |
| `login` | Wrong password | 400 Bad Request, Invalid credentials | ✅ Passed |
| `login` | User not found | 400 Bad Request, User not found | ✅ Passed |
| `getMe` | Valid user ID | 200 OK, Returns user without password | ✅ Passed |
| `getMe` | Database Error | 500 Internal Server Error | ✅ Passed |

### 2. Auth Middleware (`tests/authMiddleware.test.js`)
| Function | Scenario | Expected Result | Status |
|----------|----------|-----------------|--------|
| `authMiddleware` | Valid Bearer token | Calls `next()`, sets `req.user` | ✅ Passed |
| `authMiddleware` | No Authorization header | 401 Access Denied | ✅ Passed |
| `authMiddleware` | Invalid/expired token | 400 Invalid Token | ✅ Passed |

### 3. Task Controller (`tests/unit/taskController.unit.test.js`)
| Function | Scenario | Expected Result | Status |
|----------|----------|-----------------|--------|
| `getTasks` | Fetch all tasks | 200 OK, Returns tasks array | ✅ Passed |
| `getTasks` | Database Error | 500 Internal Server Error | ✅ Passed |
| `createTask` | Create valid task | 201 Created, Validates data | ✅ Passed |
| `createTask` | Save Error | 500 Internal Server Error | ✅ Passed |
| `updateTask` | Update existing task | 200 OK, Returns updated task | ✅ Passed |
| `deleteTask` | Delete existing task | 200 OK, Confirmation message | ✅ Passed |

### 4. Event Controller (`tests/unit/eventController.unit.test.js`)
| Function | Scenario | Expected Result | Status |
|----------|----------|-----------------|--------|
| `createEvent` | Standard fields | 201 Created | ✅ Passed |
| `createEvent` | Field Aliasing (e.g. `startDate` -> `startTime`) | 201 Created, Maps fields correctly | ✅ Passed |
| `createEvent` | Missing `startTime` | 400 Bad Request | ✅ Passed |
| `getEvents` | Fetch all events | 200 OK | ✅ Passed |
| `updateEvent` | Update success | 200 OK | ✅ Passed |
| `updateEvent` | Not Found | 404 Not Found | ✅ Passed |
| `deleteEvent` | Delete success | 200 OK | ✅ Passed |

### 5. Attendance Controller (`tests/attendanceController.test.js`)
| Function | Scenario | Expected Result | Status |
|----------|----------|-----------------|--------|
| `getAttendance` | Fetch all records | 200 OK, Returns records array | ✅ Passed |
| `getAttendance` | Database Error | 500 Internal Server Error | ✅ Passed |
| `markAttendance` | New record (upsert insert) | 200 OK, Creates record | ✅ Passed |
| `markAttendance` | Existing record (upsert update) | 200 OK, Updates record | ✅ Passed |
| `markAttendance` | Database Error | 500 Internal Server Error | ✅ Passed |
| `deleteAttendance` | Delete existing record | 200 OK, Confirmation message | ✅ Passed |
| `deleteAttendance` | Record not found | 404 Not Found | ✅ Passed |
| `deleteAttendance` | Database Error | 500 Internal Server Error | ✅ Passed |
| `getAttendanceStats` | Multiple courses | 200 OK, Grouped stats by course | ✅ Passed |
| `getAttendanceStats` | Cancelled records excluded | 200 OK, Correct totals | ✅ Passed |
| `getAttendanceStats` | No records | 200 OK, Empty object | ✅ Passed |
| `getAttendanceStats` | Database Error | 500 Internal Server Error | ✅ Passed |

### 6. Category Controller (`tests/unit/categoryController.unit.test.js`)
| Function | Scenario | Expected Result | Status |
|----------|----------|-----------------|--------|
| `getCategories` | Fetch categories | 200 OK | ✅ Passed |
| `createCategory` | Create new | 201 Created | ✅ Passed |
| `updateCategory` | Update success | 200 OK | ✅ Passed |
| `updateCategory` | Not Found | 404 Not Found | ✅ Passed |
| `deleteCategory` | Delete success | 200 OK | ✅ Passed |

### 7. Timetable Controller (`tests/timetableController.test.js`)
| Function | Scenario | Expected Result | Status |
|----------|----------|-----------------|--------|
| `getTimetable` | Fetch all entries | 200 OK, Returns entries array | ✅ Passed |
| `getTimetable` | Database Error | 500 Internal Server Error | ✅ Passed |
| `createTimetableEntry` | Create valid entry | 201 Created | ✅ Passed |
| `createTimetableEntry` | Save Error | 500 Internal Server Error | ✅ Passed |
| `updateTimetableEntry` | Update existing entry | 200 OK, Returns updated entry | ✅ Passed |
| `updateTimetableEntry` | Entry not found | 404 Not Found | ✅ Passed |
| `updateTimetableEntry` | Database Error | 500 Internal Server Error | ✅ Passed |
| `deleteTimetableEntry` | Delete existing entry | 200 OK, Confirmation message | ✅ Passed |
| `deleteTimetableEntry` | Entry not found | 404 Not Found | ✅ Passed |
| `deleteTimetableEntry` | Database Error | 500 Internal Server Error | ✅ Passed |

### 8. AI Controller (`tests/unit/aiController.unit.test.js`)
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
