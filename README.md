# Sports Management System

A full-stack sports management application for organizing leagues,
tournaments, teams, players, matches, venues, staff, contracts, transfers, and
statistics.

The project is split into:

- [`backend/`](./backend) - Express REST API with MySQL
- [`frontend/`](./frontend) - React web application

## Features

- User and administrator authentication with JWT
- Role-based access control for protected pages and API operations
- League and tournament management
- Team and coach management
- Player profiles, contracts, statistics, and transfers
- Venue and referee management
- Match scheduling, results, lineups, and match events
- League tables, dashboards, reports, and performance statistics
- BCNF-oriented MySQL schema with relationships and triggers

## Technology

### Backend

- Node.js
- Express 5
- MySQL
- `mysql2`
- JSON Web Tokens
- `bcrypt`

### Frontend

- React 19
- Create React App
- React Router
- Axios
- Tailwind CSS
- Recharts
- Lucide React

## Requirements

- Node.js 18 or newer
- npm
- MySQL 8 or a compatible MySQL server

## Project setup

### 1. Clone the repository

```bash
git clone https://github.com/syedhassan92/Sports-Management-System.git
cd Sports-Management-System
```

### 2. Configure and initialize the database

Create a `.env` file in `backend/`:

```env
PORT=5000
FRONTEND_URL=http://localhost:3000

DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=
DB_NAME=sports_management_db

JWT_SECRET=replace-with-a-long-random-secret
JWT_EXPIRE=24h
```

Run the complete database setup script:

```bash
mysql -u root -p < backend/database/complete-setup.sql
```

The script creates the database, tables, relationships, triggers, and sample
records. It drops and recreates `sports_management_db`, so do not run it
against a database containing data you need to preserve.

### 3. Install backend dependencies and start the API

```bash
cd backend
npm install
npm run dev
```

The API runs at `http://localhost:5000` by default. Its health endpoint is:

```text
http://localhost:5000/api/health
```

### 4. Install frontend dependencies and start the web app

Open a second terminal from the repository root:

```bash
cd frontend
npm install
npm start
```

The frontend runs at `http://localhost:3000`.

The frontend API client currently uses `http://localhost:5000/api`. If the
backend runs elsewhere, update the `baseURL` in
[`frontend/src/services/apiService.js`](./frontend/src/services/apiService.js).

## Local demo accounts

The database setup script creates sample accounts:

| Account | Login identifier | Password | Role |
| --- | --- | --- | --- |
| Admin | `admin@sports.com` | `admin123` | Admin |
| User | `user` | `user123` | User |

These credentials are for local development only. Change or remove them before
deploying the application.

## Useful commands

### Backend

```bash
cd backend
npm run dev       # Start with automatic restarts
npm start         # Start normally
```

### Frontend

```bash
cd frontend
npm start         # Development server
npm run build     # Production build
npm test          # React test runner
```

## Documentation

- [Backend README](./backend/README.md) - API, authentication, database, and
  troubleshooting details
- [Frontend README](./frontend/README.md) - screens, routing, API client, and
  frontend development details

## Repository structure

```text
.
├── backend/
│   ├── config/            # Database connection
│   ├── database/          # SQL schema and seed scripts
│   ├── middleware/        # JWT and authorization middleware
│   ├── routes/            # API route modules
│   ├── server.js          # API entry point
│   └── README.md
├── frontend/
│   ├── public/            # Static assets
│   ├── src/
│   │   ├── components/    # Shared UI and layout
│   │   ├── context/       # Authentication and app state
│   │   ├── pages/         # User and admin screens
│   │   └── services/      # API and mock data services
│   └── README.md
└── README.md
```

## Security notes

- Never commit `.env` files, passwords, or production JWT secrets.
- Replace the sample credentials before deployment.
- Use a strong, unique `JWT_SECRET` in every deployed environment.
- Do not expose the MySQL server publicly unless it is properly secured.
