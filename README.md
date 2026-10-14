#  Hotel Management System

## Structure

- `backend/` - Laravel 12 REST API
- `frontend/` - React 19 + Vite interface
- `render.yaml` - Render Blueprint for both services

## Local start

Backend:

```powershell
cd backend
copy .env.example .env
php artisan key:generate
New-Item -ItemType File -Force database\database.sqlite
php artisan migrate --seed
php artisan serve
```

Frontend in another terminal:

```powershell
cd frontend
copy .env.example .env
npm install
npm run dev
```

Default local-only credentials from `.env.example`:

- Email: `admin@example.com`
- Password: `change-me-now`

Change them before any public deployment.

## Aiven variables

Set these on the Render backend service from the Aiven connection information:

- `DB_HOST`
- `DB_PORT`
- `DB_DATABASE` (often `defaultdb`)
- `DB_USERNAME`
- `DB_PASSWORD`
- `DB_SSL_CA_B64`

Create the CA value in PowerShell after downloading Aiven's `ca.pem`:

```powershell
[Convert]::ToBase64String([IO.File]::ReadAllBytes("ca.pem"))
```

Also provide:

- `APP_KEY` from `php artisan key:generate --show`
- `SUPER_ADMIN_EMAIL`
- `SUPER_ADMIN_PASSWORD`

Do not commit real credentials.

## Vercel frontend deployment

Import this repository into Vercel and keep the project root set to the repository root. The root `vercel.json` installs the frontend dependencies, runs its Vite production build, and publishes `frontend/dist`.

Set `VITE_API_URL` in the Vercel project's environment variables to the public URL of the deployed backend (for example, the Render API URL). Redeploy after changing environment variables.

## Tomorrow's lab modification pattern

The generic entity is currently `Record` with `name`, `description`, and `status`. Rename or replace these pieces for the exam subject:

- `backend/app/Models/Record.php`
- `backend/app/Http/Controllers/Api/RecordController.php`
- the `records` migration
- `frontend/src/services/recordService.js`
- `frontend/src/components/RecordForm.jsx`
- `frontend/src/components/RecordTable.jsx`

Login, Super Admin authorization, API authentication, Render deployment, and Aiven configuration can stay unchanged.
