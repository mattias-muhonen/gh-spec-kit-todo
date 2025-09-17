# Tasks: Todo App with User Assignment

**Input**: Design documents from `/specs/001-todo-app-where/`
**Prerequisites**: plan.md (required), research.md, data-model.md, contracts/

## Execution Flow (main)
```
1. Load plan.md from feature directory
   → If not found: ERROR "No implementation plan found"
   → Extract: tech stack, libraries, structure
2. Load optional design documents:
   → data-model.md: Extract entities → model tasks
   → contracts/: Each file → contract test task
   → research.md: Extract decisions → setup tasks
3. Generate tasks by category:
   → Setup: project init, dependencies, linting
   → Tests: contract tests, integration tests
   → Core: models, services, CLI commands
   → Integration: DB, middleware, logging
   → Polish: unit tests, performance, docs
4. Apply task rules:
   → Different files = mark [P] for parallel
   → Same file = sequential (no [P])
   → Tests before implementation (TDD)
5. Number tasks sequentially (T001, T002...)
6. Generate dependency graph
7. Create parallel execution examples
8. Validate task completeness:
   → All contracts have tests?
   → All entities have models?
   → All endpoints implemented?
9. Return: SUCCESS (tasks ready for execution)
```

## Format: `[ID] [P?] Description`
- **[P]**: Can run in parallel (different files, no dependencies)
- Include exact file paths in descriptions

## Path Conventions
- **Web app structure**: `backend/src/`, `frontend/src/`
- All paths relative to repository root

## Phase 3.1: Setup
- [ ] T001 Create backend project structure with directories backend/src/{models,services,api,utils} and backend/tests/{contract,integration,unit}
- [ ] T002 Create frontend project structure with directories frontend/src/{components,pages,services,utils} and frontend/tests
- [ ] T003 Initialize backend Node.js project with TypeScript, Express, Jest dependencies in backend/package.json
- [ ] T004 Initialize frontend React project with TypeScript, Vite, React Testing Library in frontend/package.json
- [ ] T005 [P] Configure ESLint and Prettier for backend in backend/.eslintrc.json and backend/.prettierrc
- [ ] T006 [P] Configure ESLint and Prettier for frontend in frontend/.eslintrc.json and frontend/.prettierrc
- [ ] T007 [P] Create TypeScript configs in backend/tsconfig.json and frontend/tsconfig.json
- [ ] T008 [P] Set up Jest configs in backend/jest.config.js and frontend/jest.config.js
- [ ] T009 Create data storage directory backend/data with .gitkeep file

## Phase 3.2: Tests First (TDD) ⚠️ MUST COMPLETE BEFORE 3.3
**CRITICAL: These tests MUST be written and MUST FAIL before ANY implementation**

### Contract Tests (API Endpoints)
- [ ] T010 [P] Contract test GET /api/tasks in backend/tests/contract/tasks.get.test.ts
- [ ] T011 [P] Contract test POST /api/tasks in backend/tests/contract/tasks.post.test.ts
- [ ] T012 [P] Contract test GET /api/tasks/:id in backend/tests/contract/tasks.getById.test.ts
- [ ] T013 [P] Contract test PUT /api/tasks/:id in backend/tests/contract/tasks.put.test.ts
- [ ] T014 [P] Contract test DELETE /api/tasks/:id in backend/tests/contract/tasks.delete.test.ts
- [ ] T015 [P] Contract test GET /api/users in backend/tests/contract/users.get.test.ts
- [ ] T016 [P] Contract test POST /api/users in backend/tests/contract/users.post.test.ts
- [ ] T017 [P] Contract test GET /api/users/:id in backend/tests/contract/users.getById.test.ts
- [ ] T018 [P] Contract test PUT /api/users/:id in backend/tests/contract/users.put.test.ts
- [ ] T019 [P] Contract test DELETE /api/users/:id in backend/tests/contract/users.delete.test.ts

### Integration Tests (User Scenarios)
- [ ] T020 [P] Integration test: Task assignment flow in backend/tests/integration/taskAssignment.test.ts
- [ ] T021 [P] Integration test: User deletion handling in backend/tests/integration/userDeletion.test.ts
- [ ] T022 [P] Integration test: Bulk task operations in backend/tests/integration/bulkOperations.test.ts
- [ ] T023 [P] Frontend component test: TaskList in frontend/tests/components/TaskList.test.tsx
- [ ] T024 [P] Frontend component test: TaskForm in frontend/tests/components/TaskForm.test.tsx
- [ ] T025 [P] Frontend component test: UserSelector in frontend/tests/components/UserSelector.test.tsx

## Phase 3.3: Core Implementation (ONLY after tests are failing)

### Data Models
- [ ] T026 [P] Create Task model with validation in backend/src/models/Task.ts
- [ ] T027 [P] Create User model with validation in backend/src/models/User.ts
- [ ] T028 [P] Create TypeScript interfaces for DTOs in backend/src/types/index.ts

### Storage Layer
- [ ] T029 [P] Implement JSON file storage service in backend/src/services/StorageService.ts
- [ ] T030 Create task storage operations in backend/src/services/TaskStorage.ts
- [ ] T031 Create user storage operations in backend/src/services/UserStorage.ts

### Business Logic Services
- [ ] T032 Implement TaskService with CRUD operations in backend/src/services/TaskService.ts
- [ ] T033 Implement UserService with CRUD operations in backend/src/services/UserService.ts
- [ ] T034 Add task assignment logic to TaskService in backend/src/services/TaskService.ts
- [ ] T035 Add orphan task handling when user deleted in backend/src/services/UserService.ts

### API Endpoints
- [ ] T036 Create Express app setup and middleware in backend/src/app.ts
- [ ] T037 Implement GET /api/tasks endpoint in backend/src/api/tasks.ts
- [ ] T038 Implement POST /api/tasks endpoint in backend/src/api/tasks.ts
- [ ] T039 Implement GET /api/tasks/:id endpoint in backend/src/api/tasks.ts
- [ ] T040 Implement PUT /api/tasks/:id endpoint in backend/src/api/tasks.ts
- [ ] T041 Implement DELETE /api/tasks/:id endpoint in backend/src/api/tasks.ts
- [ ] T042 Implement GET /api/users endpoint in backend/src/api/users.ts
- [ ] T043 Implement POST /api/users endpoint in backend/src/api/users.ts
- [ ] T044 Implement GET /api/users/:id endpoint in backend/src/api/users.ts
- [ ] T045 Implement PUT /api/users/:id endpoint in backend/src/api/users.ts
- [ ] T046 Implement DELETE /api/users/:id endpoint in backend/src/api/users.ts

### Frontend Components
- [ ] T047 [P] Create TaskList component in frontend/src/components/TaskList.tsx
- [ ] T048 [P] Create TaskForm component in frontend/src/components/TaskForm.tsx
- [ ] T049 [P] Create TaskItem component in frontend/src/components/TaskItem.tsx
- [ ] T050 [P] Create UserSelector component in frontend/src/components/UserSelector.tsx
- [ ] T051 [P] Create FilterBar component in frontend/src/components/FilterBar.tsx
- [ ] T052 [P] Create UserManagement component in frontend/src/components/UserManagement.tsx

### Frontend Services
- [ ] T053 [P] Create API client service in frontend/src/services/api.ts
- [ ] T054 [P] Create task API methods in frontend/src/services/taskService.ts
- [ ] T055 [P] Create user API methods in frontend/src/services/userService.ts

### Frontend Pages
- [ ] T056 Create main App component with routing in frontend/src/App.tsx
- [ ] T057 Create TasksPage with task list and filters in frontend/src/pages/TasksPage.tsx
- [ ] T058 Create UsersPage for user management in frontend/src/pages/UsersPage.tsx

## Phase 3.4: Integration
- [ ] T059 Add request validation middleware in backend/src/middleware/validation.ts
- [ ] T060 Add error handling middleware in backend/src/middleware/errorHandler.ts
- [ ] T061 Add CORS configuration in backend/src/middleware/cors.ts
- [ ] T062 Set up Vite proxy for API in frontend/vite.config.ts
- [ ] T063 Add loading states and error handling to frontend components
- [ ] T064 Implement real-time UI updates after API operations

## Phase 3.5: Polish
- [ ] T065 [P] Add unit tests for Task model validation in backend/tests/unit/models/Task.test.ts
- [ ] T066 [P] Add unit tests for User model validation in backend/tests/unit/models/User.test.ts
- [ ] T067 [P] Add unit tests for StorageService in backend/tests/unit/services/StorageService.test.ts
- [ ] T068 Create API documentation with Swagger UI in backend/src/api/swagger.ts
- [ ] T069 Create README.md with setup and usage instructions
- [ ] T070 Add environment variable configuration in backend/.env.example and frontend/.env.example
- [ ] T071 Performance optimization: Add response caching for GET requests
- [ ] T072 Add input sanitization for XSS prevention
- [ ] T073 Run full test suite and ensure 80% coverage
- [ ] T074 Manual testing following quickstart.md scenarios

## Dependencies
- Setup (T001-T009) must complete first
- All tests (T010-T025) before any implementation (T026-T058)
- Models (T026-T028) before services (T029-T035)
- Services before API endpoints (T036-T046)
- Backend implementation before frontend can be fully tested
- Integration (T059-T064) after core implementation
- Polish (T065-T074) last

## Parallel Execution Examples

### Batch 1: Project Setup (T005-T008)
```bash
# Launch all config tasks together:
Task: "Configure ESLint and Prettier for backend"
Task: "Configure ESLint and Prettier for frontend"
Task: "Create TypeScript configs"
Task: "Set up Jest configs"
```

### Batch 2: Contract Tests (T010-T019)
```bash
# Launch all API contract tests together:
Task: "Contract test GET /api/tasks"
Task: "Contract test POST /api/tasks"
Task: "Contract test GET /api/tasks/:id"
Task: "Contract test PUT /api/tasks/:id"
Task: "Contract test DELETE /api/tasks/:id"
Task: "Contract test GET /api/users"
Task: "Contract test POST /api/users"
Task: "Contract test GET /api/users/:id"
Task: "Contract test PUT /api/users/:id"
Task: "Contract test DELETE /api/users/:id"
```

### Batch 3: Integration Tests (T020-T025)
```bash
# Launch all integration tests together:
Task: "Integration test: Task assignment flow"
Task: "Integration test: User deletion handling"
Task: "Integration test: Bulk task operations"
Task: "Frontend component test: TaskList"
Task: "Frontend component test: TaskForm"
Task: "Frontend component test: UserSelector"
```

### Batch 4: Models and Types (T026-T029)
```bash
# Launch model creation together:
Task: "Create Task model with validation"
Task: "Create User model with validation"
Task: "Create TypeScript interfaces for DTOs"
Task: "Implement JSON file storage service"
```

### Batch 5: Frontend Components (T047-T052)
```bash
# Launch all UI components together:
Task: "Create TaskList component"
Task: "Create TaskForm component"
Task: "Create TaskItem component"
Task: "Create UserSelector component"
Task: "Create FilterBar component"
Task: "Create UserManagement component"
```

### Batch 6: Frontend Services (T053-T055)
```bash
# Launch API client services together:
Task: "Create API client service"
Task: "Create task API methods"
Task: "Create user API methods"
```

### Batch 7: Unit Tests (T065-T067)
```bash
# Launch unit tests together:
Task: "Unit tests for Task model validation"
Task: "Unit tests for User model validation"
Task: "Unit tests for StorageService"
```

## Notes
- [P] tasks can run in parallel as they modify different files
- Sequential tasks modify the same file or have dependencies
- Verify all tests fail before implementing features (TDD)
- Commit after completing each task or batch
- Run test suite after each implementation phase

## Validation Checklist
*GATE: Checked before execution*

- [x] All API endpoints from contracts have tests (T010-T019)
- [x] All entities from data model have tasks (T026-T027)
- [x] All user scenarios have integration tests (T020-T025)
- [x] All tests come before implementation
- [x] Parallel tasks are truly independent (different files)
- [x] Each task specifies exact file path
- [x] No [P] task modifies same file as another [P] task
- [x] Total tasks: 74 (comprehensive coverage)