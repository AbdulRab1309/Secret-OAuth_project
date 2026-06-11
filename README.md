# Secret-OAuth_project

A small Node.js/Express application demonstrating local authentication and Google OAuth2, storing user secrets in PostgreSQL.

## Features
- Local username/password authentication (Passport Local)
- Google OAuth2 sign-in (passport-google-oauth2)
- Session management with `express-session`
- Store and display per-user "secrets" from a PostgreSQL database

## Tech stack
- Node.js (ES modules)
- Express
- Passport (local + Google)
- PostgreSQL
- EJS templates

## Prerequisites
- Node.js 16+ and npm
- PostgreSQL server
- A Google OAuth client (Client ID / Client Secret) for OAuth sign-in

## Setup
1. Clone the repository and install dependencies:

```bash
git clone <repo-url>
cd Secret-OAuth_project
npm install
```

2. Create a `.env` file in the project root with these variables (do NOT commit this file):

```env
GOOGLE_CLIENT_ID=""
GOOGLE_CLIENT_SECRET=""
SESSION_SECRET="a-long-random-secret"
PG_USER="postgres"
PG_HOST="localhost"
PG_DATABASE="secrets"
PG_PASSWORD="your_db_password"
PG_PORT="5432"
```

3. Create the PostgreSQL database and table (example):

```sql
CREATE DATABASE secrets;
\c secrets

CREATE TABLE users (
	id SERIAL PRIMARY KEY,
	email TEXT UNIQUE,
	password TEXT,
	secret TEXT
);
```

4. Start the app:

```bash
# start with node
node index.js

# or with nodemon (if installed globally)
nodemon index.js
```

The app listens on port `3000` by default. Open `http://localhost:3000`.

## Notes & Tips
- Keep `.env` out of version control — add it to `.gitignore` (this repo already includes one).
- If you see Git line-ending warnings on Windows, there is a `.gitattributes` in the repo to enforce LF in the repository.
- To change your PostgreSQL user password, run:

```sql
ALTER USER postgres WITH PASSWORD 'NewSecurePassword';
```

## Security
- Use strong, unique values for `SESSION_SECRET` and your database password.
- When deploying, set environment variables on the host (do not store secrets in the repository).

## Contributing
- Feel free to open issues or pull requests. Ensure secrets are not included in commits.

## License
This project is provided as-is. Add a license file if you plan to publish it.
