# Data Model

**Feature**: Todo App with User Assignment
**Date**: 2025-09-17

## Entities

### Task
Represents a todo item that can be assigned to users.

**Fields**:
- `id`: string (UUID) - Unique identifier
- `title`: string (required, 1-200 chars) - Task title
- `description`: string (optional, 0-2000 chars) - Detailed description
- `completed`: boolean - Completion status (default: false)
- `assignedTo`: string | null - User ID of assignee (nullable)
- `createdAt`: ISO 8601 datetime - Creation timestamp
- `updatedAt`: ISO 8601 datetime - Last modification timestamp
- `completedAt`: ISO 8601 datetime | null - Completion timestamp

**Validation Rules**:
- Title cannot be empty or whitespace only
- Title must be between 1 and 200 characters
- Description must be 2000 characters or less
- Cannot assign to non-existent user ID
- CompletedAt must be null when completed is false
- CompletedAt must have value when completed is true

**State Transitions**:
- Created → In Progress (when assigned)
- Created → Completed (can complete unassigned tasks)
- In Progress → Completed (mark done)
- Completed → In Progress (reopen task)
- Any state → Unassigned (remove assignment)

### User
Represents a person who can be assigned tasks.

**Fields**:
- `id`: string (UUID) - Unique identifier
- `name`: string (required, 1-100 chars) - Display name
- `email`: string (optional) - Email address for future notifications
- `createdAt`: ISO 8601 datetime - Creation timestamp
- `active`: boolean - Whether user is active (default: true)

**Validation Rules**:
- Name cannot be empty or whitespace only
- Name must be between 1 and 100 characters
- Email must be valid format if provided
- Name must be unique in the system

**Business Rules**:
- Inactive users cannot be assigned new tasks
- Existing assignments remain when user becomes inactive
- Deleting a user sets all their tasks to unassigned

## Relationships

### Task → User (Many-to-One)
- A task can be assigned to zero or one user
- A user can have zero or many tasks assigned
- Relationship is optional (tasks can be unassigned)
- Orphaned tasks (assigned to deleted user) become unassigned

## Storage Schema

### JSON File Structure

**tasks.json**:
```json
{
  "tasks": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440001",
      "title": "Implement user authentication",
      "description": "Add login and registration functionality",
      "completed": false,
      "assignedTo": "550e8400-e29b-41d4-a716-446655440002",
      "createdAt": "2025-01-17T10:30:00Z",
      "updatedAt": "2025-01-17T14:45:00Z",
      "completedAt": null
    }
  ]
}
```

**users.json**:
```json
{
  "users": [
    {
      "id": "550e8400-e29b-41d4-a716-446655440002",
      "name": "John Doe",
      "email": "john@example.com",
      "createdAt": "2025-01-15T09:00:00Z",
      "active": true
    }
  ]
}
```

## API Data Transfer Objects (DTOs)

### CreateTaskDTO
```typescript
{
  title: string;
  description?: string;
  assignedTo?: string; // User ID
}
```

### UpdateTaskDTO
```typescript
{
  title?: string;
  description?: string;
  completed?: boolean;
  assignedTo?: string | null; // User ID or null to unassign
}
```

### TaskResponseDTO
```typescript
{
  id: string;
  title: string;
  description: string;
  completed: boolean;
  assignedTo: string | null;
  assignedUser?: { // Populated from User entity
    id: string;
    name: string;
  };
  createdAt: string;
  updatedAt: string;
  completedAt: string | null;
}
```

### CreateUserDTO
```typescript
{
  name: string;
  email?: string;
}
```

### UpdateUserDTO
```typescript
{
  name?: string;
  email?: string;
  active?: boolean;
}
```

### UserResponseDTO
```typescript
{
  id: string;
  name: string;
  email: string | null;
  active: boolean;
  createdAt: string;
  taskCount?: number; // Number of assigned tasks
}
```

## Query Patterns

### Filter Tasks by Assignee
- Parameter: `assignedTo` (user ID or "unassigned")
- Returns: Array of tasks matching filter

### Get User with Task Count
- Joins tasks to count assignments
- Returns user data with `taskCount` field

### Get Task with User Details
- Populates `assignedUser` field with user name
- Handles deleted users gracefully (shows as unassigned)

## Migration Considerations

### Future Database Migration
- UUID IDs compatible with most databases
- JSON structure maps easily to document or relational DB
- Timestamps in ISO 8601 format for compatibility
- Relationships designed for foreign key constraints

### Scaling Considerations
- Index on `assignedTo` field for filtering performance
- Index on `completed` field for status queries
- Consider pagination for large task lists
- May need to add task categories/projects later