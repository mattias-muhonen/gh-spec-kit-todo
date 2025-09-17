# Research & Technical Decisions

**Feature**: Todo App with User Assignment
**Date**: 2025-09-17
**Status**: Complete

## Key Decisions from Specification Analysis

### 1. User Management Model
**Decision**: Simple user registry without authentication
**Rationale**:
- Spec has multiple NEEDS CLARIFICATION about authentication
- Starting simple allows focus on core assignment functionality
- Can add authentication layer later without major refactoring
**Alternatives considered**:
- Full authentication system - too complex for initial implementation
- External auth provider (OAuth) - adds unnecessary complexity initially

### 2. Data Storage
**Decision**: JSON file-based storage
**Rationale**:
- Simple to implement and debug
- No database setup required for development
- Easy to migrate to database later
- Sufficient for initial scale (1000 tasks, 50 users)
**Alternatives considered**:
- SQLite - adds dependency without clear benefit at this scale
- PostgreSQL - overengineered for initial requirements
- In-memory only - doesn't meet persistence requirement

### 3. Task Assignment Rules
**Decision**: Soft assignments with orphan handling
**Rationale**:
- Tasks remain when assigned user is removed
- Assignment becomes "unassigned" automatically
- Preserves data integrity without complex cascades
**Alternatives considered**:
- Hard delete of tasks - data loss risk
- Prevent user deletion with assignments - poor UX
- Transfer to default user - adds complexity

### 4. API Design
**Decision**: RESTful API with standard CRUD operations
**Rationale**:
- Well understood pattern
- Easy to test and document
- Stateless design as per constraints
**Endpoints planned**:
- Tasks: GET, POST, PUT, DELETE /api/tasks
- Users: GET, POST, PUT, DELETE /api/users
- Filtering: GET /api/tasks?assignedTo={userId}

### 5. Frontend Architecture
**Decision**: React with TypeScript and component-based structure
**Rationale**:
- Type safety reduces bugs
- Component reusability for task lists/forms
- Modern tooling with Vite for fast development
**Component structure**:
- TaskList - displays filtered tasks
- TaskForm - create/edit tasks with assignment
- UserSelector - dropdown for user assignment
- FilterBar - filter tasks by assignee

### 6. Testing Strategy
**Decision**: Jest + React Testing Library
**Rationale**:
- Industry standard for React apps
- Good TypeScript support
- Supports both unit and integration tests
**Test categories**:
- API contract tests (request/response validation)
- Component unit tests (isolated behavior)
- Integration tests (user flows)

## Resolved Clarifications

### From FR-002: User Creation During Assignment
**Resolution**: Users must exist before assignment. No inline user creation.
**Reason**: Keeps UI simple and prevents accidental user duplication.

### From FR-007: User Management
**Resolution**: Basic CRUD for users with name and ID. No roles or permissions initially.
**Reason**: Minimal viable approach, can extend later.

### From FR-008: Orphaned Tasks
**Resolution**: Tasks become unassigned when user is deleted. Show as "Unassigned" in UI.
**Reason**: Preserves task data while handling user removal gracefully.

### From FR-010: Multi-User Support
**Resolution**: Multi-user without authentication. Users identified by selection, not login.
**Reason**: Simplifies initial implementation while supporting core requirement.

### From FR-011: Persistence Model
**Resolution**: Server-side JSON files, auto-save on changes.
**Reason**: Simple, reliable, meets persistence requirement.

### From FR-012: Task Visibility
**Resolution**: All users can see all tasks. Filter view by assignee.
**Reason**: Collaborative approach appropriate for small teams.

## Technology Stack Summary

### Backend
- **Runtime**: Node.js 20.x
- **Language**: TypeScript 5.x
- **Framework**: Express.js
- **Storage**: Node.js fs module with JSON files
- **Validation**: Joi or Zod for request validation

### Frontend
- **Framework**: React 18.x
- **Language**: TypeScript 5.x
- **Build Tool**: Vite
- **Styling**: CSS Modules or Tailwind CSS
- **State**: React Context or Zustand (simple state management)
- **HTTP Client**: Fetch API or Axios

### Development Tools
- **Testing**: Jest, React Testing Library
- **Linting**: ESLint with TypeScript rules
- **Formatting**: Prettier
- **Git Hooks**: Husky for pre-commit checks

## Next Steps (Phase 1)
1. Define data models for Task and User entities
2. Create OpenAPI specification for REST endpoints
3. Generate contract tests from API spec
4. Create quickstart guide for local development
5. Set up project structure with frontend/backend separation