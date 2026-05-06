# TeamFlow — Team Task Manager

A production-grade full-stack task management application with role-based access control, built for team collaboration.

🌐 **Live Demo**: [Add your Railway URL here]  
📁 **GitHub**: [Add your repo URL here]

---

## ✨ Features

- 🔐 **Authentication** — Secure JWT-based signup & login with bcrypt password hashing
- 📁 **Project Management** — Create, update, and delete projects; invite team members
- ✅ **Task Tracking** — Kanban board (Todo / In Progress / Done) with priorities & due dates
- 👥 **Role-Based Access Control** — Admins manage everything; Members update their assigned tasks
- 📊 **Dashboard** — Stats overview, overdue alerts, my tasks, and recent projects
- 🎨 **Premium UI** — Dark mode with glassmorphism, smooth animations, responsive design

---

## 🏗️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 18 + Vite |
| Styling | Vanilla CSS (custom design system) |
| Backend | Node.js + Express |
| Database | PostgreSQL |
| ORM | Prisma |
| Auth | JWT + bcrypt |
| Deployment | Railway |

---

## 🚀 Local Setup

### Prerequisites
- Node.js >= 18
- PostgreSQL (local or cloud)

### Backend
```bash
cd backend
cp .env.example .env
# Edit .env with your DATABASE_URL and JWT_SECRET

npm install
npx prisma db push      # Create tables
npm run dev             # Start on port 5000
```

### Frontend
```bash
cd frontend
cp .env.example .env
# Set VITE_API_URL=http://localhost:5000/api

npm install
npm run dev             # Start on port 5173
```

---

## 🌐 Railway Deployment

### 1. Backend Service
1. Create new project on [railway.app](https://railway.app)
2. Add **PostgreSQL** plugin — copy the `DATABASE_URL`
3. Create a new service → Deploy from GitHub → select `/backend` folder
4. Add environment variables:
   ```
   DATABASE_URL=<from PostgreSQL plugin>
   JWT_SECRET=<random 32+ char string>
   FRONTEND_URL=<your frontend Railway URL>
   PORT=5000
   ```
5. After deploy, run migration: In Railway shell → `npx prisma db push`

### 2. Frontend Service
1. Create another service → Deploy from GitHub → select `/frontend` folder
2. Add environment variable:
   ```
   VITE_API_URL=<your backend Railway URL>/api
   ```
3. Deploy — Railway auto-runs `npm run build` then `npm start`

---

## 📡 API Reference

### Auth
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| POST | `/api/auth/signup` | Public | Register |
| POST | `/api/auth/login` | Public | Login |
| GET | `/api/auth/me` | ✅ | Get current user |

### Projects
| Method | Endpoint | Role | Description |
|---|---|---|---|
| GET | `/api/projects` | Auth | List my projects |
| POST | `/api/projects` | Auth | Create project |
| GET | `/api/projects/:id` | Member | Project details |
| PUT | `/api/projects/:id` | Admin | Update project |
| DELETE | `/api/projects/:id` | Admin | Delete project |
| POST | `/api/projects/:id/members` | Admin | Invite member |
| DELETE | `/api/projects/:id/members/:userId` | Admin | Remove member |
| PUT | `/api/projects/:id/members/:userId/role` | Admin | Change role |

### Tasks
| Method | Endpoint | Role | Description |
|---|---|---|---|
| GET | `/api/projects/:id/tasks` | Member | List tasks |
| POST | `/api/projects/:id/tasks` | Admin | Create task |
| PUT | `/api/projects/:id/tasks/:taskId` | Admin/Assignee | Update task |
| DELETE | `/api/projects/:id/tasks/:taskId` | Admin | Delete task |

### Dashboard
| Method | Endpoint | Auth | Description |
|---|---|---|---|
| GET | `/api/dashboard` | ✅ | Aggregated stats |

---

## 🔒 Role-Based Access Control

| Action | Admin | Member |
|---|---|---|
| View project & tasks | ✅ | ✅ |
| Create/delete tasks | ✅ | ❌ |
| Assign tasks | ✅ | ❌ |
| Update task status | ✅ | ✅ (own only) |
| Invite/remove members | ✅ | ❌ |
| Change member roles | ✅ | ❌ |
| Delete project | ✅ | ❌ |

---

## 🎬 Demo Video Script (2-5 min)

1. **Landing page** (0:15) — Show the hero, features, and CTA
2. **Signup** (0:30) — Create a new account
3. **Create project** (0:30) — Add a project with description
4. **Create tasks** (1:00) — Add 3-4 tasks with different priorities/due dates to show the Kanban board
5. **Invite member** (0:30) — Invite a second user email via Settings
6. **Member login** (0:30) — Login as the second user, show restricted access
7. **Update task status** (0:30) — Member updates their own task
8. **Dashboard** (0:30) — Show stats, overdue tasks, my tasks

---

## 📁 Project Structure

```
team-task-manager/
├── backend/
│   ├── prisma/schema.prisma
│   ├── src/
│   │   ├── middleware/   (auth.js, projectRole.js)
│   │   ├── routes/       (auth, projects, tasks, dashboard)
│   │   ├── controllers/  (auth, projects, tasks, dashboard)
│   │   └── index.js
│   └── package.json
├── frontend/
│   ├── src/
│   │   ├── api/client.js
│   │   ├── context/AuthContext.jsx
│   │   ├── components/   (AppShell, KanbanBoard, TaskCard, Modal)
│   │   ├── pages/        (Landing, Login, Signup, Dashboard, Projects, ProjectDetail, ProjectSettings)
│   │   └── App.jsx
│   └── package.json
└── README.md
```

---

## 👤 Author

Built with ❤️ for placement submission.
