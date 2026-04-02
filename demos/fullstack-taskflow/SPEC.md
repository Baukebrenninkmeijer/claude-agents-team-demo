# TaskFlow - A Full-Stack Task Manager

## Overview

A clean, modern task management app built from scratch by a team of AI agents working in parallel. The app lets users create, organize, and track tasks with tags, priorities, and due dates.

## Tech Stack

- **Backend**: FastAPI (Python) + SQLite via SQLAlchemy
- **Frontend**: React + Vite + Tailwind CSS
- **Tests**: pytest (backend) + Vitest (frontend)

## Features

### Core (MVP)
- Create, read, update, delete tasks
- Each task has: title, description, priority (low/medium/high), due date, completed status
- Filter tasks by status (all / active / completed)
- Sort by priority or due date

### Nice to Have
- Tags/labels on tasks
- Search by title
- Dark mode toggle

## API Endpoints

```
GET    /api/tasks          - List all tasks (supports ?status=active|completed&sort=priority|due_date)
POST   /api/tasks          - Create a task
GET    /api/tasks/{id}     - Get a single task
PUT    /api/tasks/{id}     - Update a task
DELETE /api/tasks/{id}     - Delete a task
```

### Task Schema

```json
{
  "id": 1,
  "title": "Buy groceries",
  "description": "Milk, eggs, bread",
  "priority": "medium",
  "due_date": "2026-04-05",
  "completed": false,
  "tags": ["shopping"],
  "created_at": "2026-04-01T10:00:00Z"
}
```

## Project Structure

```
team-demo/
├── backend/
│   ├── app/
│   │   ├── main.py          # FastAPI app + CORS
│   │   ├── models.py        # SQLAlchemy models
│   │   ├── schemas.py       # Pydantic schemas
│   │   ├── database.py      # DB connection + session
│   │   └── routers/
│   │       └── tasks.py     # Task CRUD endpoints
│   ├── tests/
│   │   └── test_tasks.py    # API tests
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   ├── components/
│   │   │   ├── TaskList.jsx
│   │   │   ├── TaskItem.jsx
│   │   │   ├── TaskForm.jsx
│   │   │   └── FilterBar.jsx
│   │   ├── hooks/
│   │   │   └── useTasks.js
│   │   └── api/
│   │       └── tasks.js
│   ├── index.html
│   ├── package.json
│   ├── vite.config.js
│   └── tailwind.config.js
├── SPEC.md
└── README.md
```

## Design Notes

- Backend serves on port 8000, frontend on port 5173
- CORS configured to allow frontend origin
- SQLite DB stored at `backend/taskflow.db`
- Frontend uses fetch (no axios) to keep deps minimal
- Tailwind for styling - clean, modern look with good spacing
- Responsive layout that works on desktop
