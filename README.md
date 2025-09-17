This has been created with https://github.com/github/spec-kit/tree/main

to demonstrate what kind of specs it creates. Initial prompt was "todo app where tasks can be assigned to uses"
- set up for Claude
- /specify was the todo command
- /plan and /task

Below are the ouputs messages of the three steps
---

⏺ ✅ Specification created successfully!

  Branch: 001-todo-app-whereSpec file: /Users/mattias.muhonen/work/s
  pec-kit-todo/todo-assigns/specs/001-todo-app-where/spec.md

  The specification has been written with the core requirements for
  a todo app with user assignment capabilities. Several areas are
  marked with [NEEDS CLARIFICATION] for important decisions about:
  - User management and authentication model
  - Task visibility and permission rules
  - Handling of removed/deactivated users
  - Persistence and multi-user support details

  The spec is ready for the next phase where these clarifications
  can be addressed during planning.

  ---

  ⏺ ✅ Implementation Plan Complete

  Branch: 001-todo-app-where
  Status: Ready for task generation (/tasks command)

  Generated Artifacts:

  1. plan.md - Complete implementation plan with all phases defined
  2. research.md - Technical decisions and resolved clarifications
  3. data-model.md - Entity definitions and storage schema
  4. contracts/openapi.yaml - Full REST API specification
  5. quickstart.md - User guide and test scenarios
  6. CLAUDE.md - AI assistant context file

  Key Decisions Made:

  - Architecture: Web application with React frontend + Node.js
  backend
  - Storage: JSON file-based (simple, migratable)
  - User Model: Simple registry without authentication
  - Assignment Rules: Soft assignments with orphan handling
  - Testing: TDD approach with Jest and React Testing Library

  Phase Completion:

  ✅ Phase 0: Research complete - All clarifications resolved
  ✅ Phase 1: Design complete - Data models, API contracts, and
  quickstart created
  ✅ Phase 2: Task planning described (40-45 tasks estimated)

  The plan is now ready for the /tasks command to generate the
  detailed task list.

---

