# Claude Code Context

## Project: Todo App with User Assignment

### Tech Stack
- **Backend**: Node.js 20.x, TypeScript 5.x, Express.js
- **Frontend**: React 18.x, TypeScript 5.x, Vite
- **Storage**: JSON file-based (backend/data/)
- **Testing**: Jest, React Testing Library
- **API**: RESTful, OpenAPI 3.0 spec

### Project Structure
```
backend/
├── src/
│   ├── models/      # Task and User models
│   ├── services/    # Business logic
│   ├── api/         # Express routes
│   └── utils/       # Helpers
└── data/           # JSON storage

frontend/
├── src/
│   ├── components/  # React components
│   ├── pages/       # Page components
│   └── services/    # API clients
└── tests/
```

### Key Features
1. Task CRUD with user assignment
2. User management (create, update, delete)
3. Filter tasks by assignee
4. Reassign or unassign tasks
5. Mark tasks complete/incomplete

### API Endpoints
- `GET/POST /api/tasks` - Task management
- `GET/PUT/DELETE /api/tasks/:id` - Single task ops
- `GET/POST /api/users` - User management
- `GET/PUT/DELETE /api/users/:id` - Single user ops

### Development Commands
```bash
# Backend
cd backend && npm run dev    # Start server (port 3000)
cd backend && npm test        # Run tests

# Frontend
cd frontend && npm run dev    # Start UI (port 5173)
cd frontend && npm test       # Run tests
```

### Current Status
- Phase 0: Research ✅
- Phase 1: Design ✅
- Phase 2: Ready for task generation
- Implementation: Pending

### Data Models
- **Task**: id, title, description, completed, assignedTo, timestamps
- **User**: id, name, email, active, createdAt

### Testing Strategy
- Contract tests for API endpoints
- Component unit tests
- Integration tests for user flows
- TDD approach (tests first)

### Recent Changes
1. Created OpenAPI specification
2. Defined data models
3. Established project structure