# TaskFlow — SaaS Task Management System

A full-stack task management web application built as part of my internship assessment. I built this from scratch using React on the frontend and Node.js/Express on the backend, with PostgreSQL (Supabase) as the database. For the UI design and CSS enhancements, I used AI-assisted design tools (Google Stitch + AI) to generate the design system and then integrated it into the React codebase manually.

---

## Tech Stack

### Frontend
| Technology | Purpose |
|---|---|
| React 19 + Vite | Component-based UI framework with fast HMR |
| Tailwind CSS v4 | Utility-first styling with `@theme` design tokens |
| React Router DOM v7 | Client-side routing and auth guards |
| Axios | HTTP client for backend API calls |
| Material Symbols (Google) | Icon library |
| Inter (Google Fonts) | Primary typeface |

### Backend
| Technology | Purpose |
|---|---|
| Node.js + Express | REST API server |
| Sequelize ORM | Database models and migrations |
| PostgreSQL (Supabase) | Production database with SSL |
| JSON Web Tokens (JWT) | Stateless authentication |
| bcrypt | Password hashing |
| dotenv | Environment variable management |
| CORS | Cross-origin request handling |

### Design & AI Tools
- **Google Stitch** — Used to generate the "SaaS Task Management System" UI design system (color tokens, typography, component layouts)
- **AI-assisted CSS** — Tailwind design tokens and component CSS were enhanced and refined using AI tools to match the Stitch design system precisely

---

## Features Implemented

### Authentication
- [x] User registration with email & password
- [x] Secure login with JWT token-based authentication
- [x] Password hashing using bcrypt
- [x] Protected routes (redirects to `/auth` if not logged in)
- [x] Persistent login session via `localStorage`
- [x] Auto-login after registration

### Task Management
- [x] Create new tasks with a title
- [x] View all tasks in a Kanban-style board (Pending / Completed columns)
- [x] Toggle task status between Pending and Completed
- [x] Delete tasks
- [x] Real-time stat cards (Total, Pending, Completed counts)
- [x] Live progress bar showing weekly completion percentage

### UI / UX
- [x] Pixel-perfect implementation of the Stitch "SaaS Task Management System" design
- [x] Responsive layout (mobile-friendly, sidebar hidden on small screens)
- [x] Frosted glass top navigation bar
- [x] Fixed sidebar with navigation links and sign-out
- [x] Quick Create task bar with a floating action button (FAB)
- [x] Team Activity feed and Weekly Goal progress card
- [x] Auth page with Login/Sign up toggle, social buttons (Google, SSO), and side hero panel
- [x] Material Symbols icons throughout the UI
- [x] Smooth hover and transition animations

---

## 🛠️ Setup Steps

### Prerequisites
- Node.js v18+ and npm
- A [Supabase](https://supabase.com) account (free tier works)
- Git

---

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/prductspace_assesment.git
cd prductspace_assesment
```

---

### 2. Backend Setup

```bash
cd backend
npm install
```

Create a `.env` file in the `backend/` folder (see `.env.example` for reference):

```env
PORT=5000
DATABASE_URL=postgresql://postgres:[YOUR-PASSWORD]@db.xxxxxxxxxxxx.supabase.co:5432/postgres
JWT_SECRET=your_super_secret_jwt_key_here
```

> **Note:** Get `DATABASE_URL` from Supabase → Project → Settings → Database → Connection String (URI mode). Make sure to URL-encode special characters in your password (e.g. `@` → `%40`).

Start the backend server:

```bash
node index.js
```

The server runs on `http://localhost:5000`. On startup, Sequelize will automatically sync the database tables.

---

### 3. Frontend Setup

```bash
cd ../frontend
npm install
```

Create a `.env` file in the `frontend/` folder (see `.env.example` for reference):

```env
VITE_API_URL=http://localhost:5000/api
```

Start the development server:

```bash
npm run dev
```

The app runs on `http://localhost:5173`.

---

## 🌐 Deployment

### Backend — Render (recommended)

1. Push your code to GitHub (`.env` is gitignored — never committed)
2. Create a new **Web Service** on [Render](https://render.com)
3. Set **Root Directory** to `backend`
4. Set **Build Command** to `npm install`
5. Set **Start Command** to `node index.js`
6. Add environment variables in the Render dashboard:
   - `DATABASE_URL`
   - `JWT_SECRET`
   - `PORT` (Render sets this automatically)

### Frontend — Vercel (recommended)

1. Create a new project on [Vercel](https://vercel.com)
2. Set **Root Directory** to `frontend`
3. Set **Build Command** to `npm run build`
4. Set **Output Directory** to `dist`
5. Add environment variable in Vercel dashboard:
   - `VITE_API_URL` = `https://your-backend.onrender.com/api`

---

## 📁 Project Structure

```
prductspace_assesment/
├── backend/
│   ├── config/
│   │   └── database.js        # Sequelize + PostgreSQL config
│   ├── controllers/
│   │   ├── authController.js  # Register / Login logic
│   │   └── taskController.js  # CRUD task logic
│   ├── middleware/
│   │   └── auth.js            # JWT verification middleware
│   ├── models/
│   │   ├── User.js            # User model
│   │   └── Task.js            # Task model (Pending/Completed enum)
│   ├── routes/
│   │   ├── auth.js            # /api/auth routes
│   │   └── tasks.js           # /api/tasks routes
│   ├── .env.example
│   ├── .gitignore
│   └── index.js               # Express server entry point
│
└── frontend/
    ├── src/
    │   ├── context/
    │   │   └── AuthContext.jsx  # Global auth state (login/register/logout)
    │   ├── pages/
    │   │   ├── Auth.jsx         # Login + Sign up page
    │   │   └── Dashboard.jsx    # Main task board dashboard
    │   ├── services/
    │   │   └── api.js           # Axios instance with auth headers
    │   ├── index.css            # Tailwind v4 + design tokens
    │   └── main.jsx             # React entry point
    ├── index.html               # Loads Google Fonts + Material Symbols
    ├── vite.config.js
    ├── .env.example
    └── .gitignore
```

---

## 🔑 API Endpoints

| Method | Endpoint | Auth Required | Description |
|---|---|---|---|
| POST | `/api/auth/register` | No | Create a new user account |
| POST | `/api/auth/login` | No | Login and receive JWT token |
| GET | `/api/tasks` | Yes | Get all tasks for logged-in user |
| POST | `/api/tasks` | Yes | Create a new task |
| PUT | `/api/tasks/:id` | Yes | Update task status |
| DELETE | `/api/tasks/:id` | Yes | Delete a task |

---

## 📝 Notes

- The Task status enum in the database uses `'Pending'` and `'Completed'` (capital first letter) — the frontend sends values in this exact casing.
- JWT tokens are stored in `localStorage` and attached to every API request via an Axios interceptor.
- The UI design system was generated using **Google Stitch AI** and manually integrated into React components with Tailwind CSS v4.
