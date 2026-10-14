# Sports Management System Backend

This directory contains the Express API and MySQL database integration for the
Sports Management System.

## Stack

- Node.js
- Express 5
- MySQL, accessed through `mysql2`
- JSON Web Tokens (JWT) for authentication
- `bcrypt` for password hashing
- `nodemon` for development

## Requirements

- Node.js 18 or newer
- npm
- MySQL 8 or a compatible MySQL server

## Installation

From this directory, install the dependencies:

```bash
npm install
```

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

`DB_HOST`, `DB_USER`, `DB_NAME`, and `DB_PORT` have defaults in the application,
but setting them explicitly is recommended. Do not commit `.env` or real
credentials.

## Database setup

The complete setup script creates the `sports_management_db` database, all
tables, triggers, relationships, and sample records:

```text
database/complete-setup.sql
```

Run it with MySQL:

```bash
mysql -u root -p < database/complete-setup.sql
```

The script drops and recreates `sports_management_db`, so do not run it against
a database containing data you need to keep.

The schema includes users and admins, leagues, tournaments, teams, coaches,
referees, players, contracts, venues, matches, statistics, and transfers.

## Running the API

Development mode (restarts when files change):

```bash
npm run dev
```

Normal start:

```bash
npm start
```

The server listens on `http://localhost:5000` by default. Check that it is
running with:

```text
GET http://localhost:5000/api/health
```

## API route groups

All routes are prefixed with `http://localhost:5000/api`.

| Prefix | Purpose |
| --- | --- |
| `/auth` | User and admin login and registration |
| `/teams` | Team management and team relationships |
| `/leagues` | League management |
| `/tournaments` | Tournament management, teams, and brackets |
| `/players` | Player management, statistics, matches, and transfers |
| `/coaches` | Coach management |
| `/referees` | Referee management |
| `/venues` | Venue management |
| `/matches` | Match scheduling, results, lineups, and events |
| `/transfers` | Player transfer records |
| `/stats` | Dashboard, league, tournament, team, and player statistics |
| `/player-contracts` | Player contract management |

Management requests use the following header:

```text
Authorization: Bearer <jwt-token>
```

## Seed accounts

The sample SQL data includes these local-development accounts:

| Account | Login identifier | Password | Role |
| --- | --- | --- | --- |
| Admin | `admin@sports.com` | `admin123` | Admin |
| User | `user` | `user123` | User |

These credentials should be changed or removed before using the application
outside a local environment.

## Project structure

```text
backend/
├── config/
│   └── database.js       # MySQL connection pool
├── database/
│   ├── complete-setup.sql
│   ├── schema-bcnf.sql
│   └── seed-bcnf.sql
├── middleware/
│   └── auth.js            # JWT and admin authorization
├── routes/                # Express route modules
├── scripts/
│   └── resetDatabase.js
├── server.js              # Express application entry point
└── package.json
```

## Troubleshooting

- Verify that MySQL is running and `.env` matches the local installation if
  the API reports a database connection failure.
- Set `FRONTEND_URL` to the React development-server URL if CORS rejects the
  frontend.
- Change `PORT` or stop the process using port `5000` if the port is occupied.
