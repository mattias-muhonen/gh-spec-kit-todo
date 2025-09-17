# Quickstart Guide

**Feature**: Todo App with User Assignment
**Date**: 2025-09-17

## Prerequisites

- Node.js 20.x or later
- npm or yarn package manager
- Git

## Quick Setup

### 1. Clone and Install

```bash
# Clone the repository
git clone <repository-url>
cd todo-assigns

# Install backend dependencies
cd backend
npm install

# Install frontend dependencies
cd ../frontend
npm install
```

### 2. Start Development Servers

```bash
# Terminal 1: Start backend server
cd backend
npm run dev
# Server runs on http://localhost:3000

# Terminal 2: Start frontend dev server
cd frontend
npm run dev
# UI runs on http://localhost:5173
```

### 3. Verify Installation

Open your browser to http://localhost:5173 and you should see the Todo App interface.

## Feature Walkthrough

### Creating Your First User

1. Click "Manage Users" in the navigation
2. Click "Add User"
3. Enter a name (e.g., "Alice Smith")
4. Click "Save"

### Creating a Task

1. Click "Add Task" on the main page
2. Enter task title: "Complete project documentation"
3. Optional: Add a description
4. Select "Alice Smith" from the assignee dropdown
5. Click "Create Task"

### Viewing Assigned Tasks

1. Use the filter dropdown at the top of the task list
2. Select "Alice Smith" to see only her tasks
3. Select "Unassigned" to see tasks without assignees
4. Select "All" to see everything

### Reassigning a Task

1. Click on a task to open edit mode
2. Change the assignee dropdown to a different user
3. Or select "Unassigned" to remove assignment
4. Click "Save Changes"

### Completing a Task

1. Click the checkbox next to any task
2. Task moves to completed state
3. Filter by "Completed" to see finished tasks

## API Testing

### Using curl

```bash
# Create a user
curl -X POST http://localhost:3000/api/users \
  -H "Content-Type: application/json" \
  -d '{"name": "Bob Johnson", "email": "bob@example.com"}'

# Create a task (replace USER_ID with actual ID from previous response)
curl -X POST http://localhost:3000/api/tasks \
  -H "Content-Type: application/json" \
  -d '{"title": "Review code changes", "assignedTo": "USER_ID"}'

# Get all tasks
curl http://localhost:3000/api/tasks

# Get tasks assigned to specific user
curl http://localhost:3000/api/tasks?assignedTo=USER_ID

# Update task to mark complete (replace TASK_ID)
curl -X PUT http://localhost:3000/api/tasks/TASK_ID \
  -H "Content-Type: application/json" \
  -d '{"completed": true}'
```

### Using the API Documentation

1. Navigate to http://localhost:3000/api-docs
2. Interactive Swagger UI for testing all endpoints
3. Try out each operation with example data

## Running Tests

```bash
# Run backend tests
cd backend
npm test

# Run frontend tests
cd frontend
npm test

# Run all tests with coverage
npm run test:coverage
```

## Test Scenarios

### Scenario 1: Task Assignment Flow
1. Create 2 users: "Alice" and "Bob"
2. Create task "Write tests" assigned to Alice
3. Verify task appears in Alice's filtered view
4. Reassign task to Bob
5. Verify task moves to Bob's filtered view
6. Unassign task
7. Verify task appears in "Unassigned" filter

### Scenario 2: User Deletion Handling
1. Create user "Charlie"
2. Create 3 tasks assigned to Charlie
3. Delete Charlie from user management
4. Verify all 3 tasks now show as "Unassigned"
5. Verify tasks are not deleted

### Scenario 3: Bulk Operations
1. Create 5 tasks with mixed assignments
2. Mark 3 as complete
3. Filter by "Completed" status
4. Verify only 3 completed tasks show
5. Filter by "Active" status
6. Verify only 2 active tasks show

## Data Storage

- Tasks stored in: `backend/data/tasks.json`
- Users stored in: `backend/data/users.json`
- Files auto-created on first run
- Human-readable JSON format for debugging

## Troubleshooting

### Port Already in Use
```bash
# Change backend port
PORT=3001 npm run dev

# Update frontend proxy in vite.config.ts
```

### Data Not Persisting
- Check `backend/data/` directory exists
- Verify write permissions on data files
- Check console for file system errors

### User Not Found Errors
- Ensure users are created before assignment
- Check user ID format matches (UUIDs)
- Verify user is active (not deleted)

## Next Steps

1. **Add Authentication**: Implement user login to track who makes changes
2. **Add Categories**: Group tasks by project or category
3. **Add Due Dates**: Time-based task management
4. **Add Comments**: Collaboration features on tasks
5. **Add Notifications**: Email when assigned a task

## Environment Variables

### Backend (.env)
```
PORT=3000
NODE_ENV=development
DATA_PATH=./data
```

### Frontend (.env)
```
VITE_API_URL=http://localhost:3000/api
```