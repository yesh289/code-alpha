# CodeAlpha_ProjectManagementTool

A full-stack collaborative project management tool (Task 3 — CodeAlpha Full Stack Development Internship).
Built with **React + Vite** (frontend), **Node.js + Express + MongoDB** (backend), and **Socket.io** for
real-time updates.

## Features
- User registration & login (JWT authentication, hashed passwords)
- Create projects, invite members by email
- Kanban-style task board: To Do / In Progress / Done
- Task creation, editing, assigning, moving between columns, deleting
- Comments on tasks
- **Real-time updates** across all connected users on a project board (new tasks, moved tasks,
  deleted tasks, and new comments all sync live via WebSockets — this is the bonus feature from
  the task brief)

## Tech Stack
| Layer     | Tech |
|-----------|------|
| Frontend  | React 18, React Router, Axios, Socket.io-client, Vite |
| Backend   | Node.js, Express.js, Mongoose (MongoDB), JWT, bcrypt.js, Socket.io |
| Database  | MongoDB |

## Project Structure
```
CodeAlpha_ProjectManagementTool/
├── backend/
│   ├── config/db.js
│   ├── models/        (User, Project, Task, Comment)
│   ├── middleware/auth.js
│   ├── routes/         (auth, projects, tasks, comments)
│   └── server.js
└── frontend/
    └── src/
        ├── api/axios.js
        ├── context/AuthContext.jsx
        ├── pages/       (Login, Register, Dashboard, ProjectBoard)
        └── components/  (Navbar, ProjectCard, TaskCard, TaskModal)
```

## Setup & Run Locally

### Prerequisites
- Node.js 18+
- MongoDB running locally, or a free MongoDB Atlas connection string

### 1. Backend
```bash
cd backend
cp .env.example .env      # then edit MONGO_URI / JWT_SECRET if needed
npm install
npm run dev                # starts on http://localhost:5000
```

### 2. Frontend
```bash
cd frontend
cp .env.example .env
npm install
npm run dev                # starts on http://localhost:5173
```

Open http://localhost:5173, register a user, create a project, and start adding tasks.
Open the same project in a second browser tab (or invite + log in as a second user) to see the
real-time sync in action.

## API Overview
| Method | Endpoint                          | Description                    |
|--------|------------------------------------|---------------------------------|
| POST   | /api/auth/register                | Register a new user            |
| POST   | /api/auth/login                   | Log in, get JWT                |
| GET    | /api/auth/me                       | Current user (protected)       |
| GET    | /api/projects                     | List my projects                |
| POST   | /api/projects                     | Create a project                |
| GET    | /api/projects/:id                 | Project details + its tasks    |
| POST   | /api/projects/:id/members         | Invite a member by email       |
| DELETE | /api/projects/:id                 | Delete a project (owner only)  |
| POST   | /api/tasks                        | Create a task                   |
| PUT    | /api/tasks/:id                    | Update/move a task              |
| DELETE | /api/tasks/:id                    | Delete a task                   |
| GET    | /api/comments/task/:taskId        | List comments on a task        |
| POST   | /api/comments                     | Add a comment on a task        |

All endpoints except register/login require an `Authorization: Bearer <token>` header.

## Notes for Submission
- Push this whole folder to a GitHub repo named `CodeAlpha_ProjectManagementTool`.
- Record a short screen-capture walking through: register/login, creating a project, adding
  tasks, moving them across columns, commenting, and (ideally) two browser windows side by side
  showing the real-time sync — that's the most impressive part to show in the video.
- Post it on LinkedIn tagging @CodeAlpha with the GitHub link, per the internship instructions.
