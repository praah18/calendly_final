# Calendly Clone (Schedly)

## Overview
Schedly is a full-stack scheduling platform inspired by Calendly. It lets a default admin user create event types, define weekly availability, and share public booking links. Invitees can pick a date, choose a time slot, and book instantly while the system prevents double-booking.

## Features
- Create, edit, delete event types with duration and URL slug
- Weekly availability management with timezone support
- Public booking page with calendar, slots, and booking form
- Double-booking prevention
- Booking confirmation page
- Meetings dashboard with upcoming, past, and cancel actions

## Screenshots
- Event Types page: `TODO`
- Availability page: `TODO`
- Booking page: `TODO`
- Meetings page: `TODO`

## Tech Stack
- Frontend: Next.js (React), Luxon
- Backend: Node.js, Express, PostgreSQL, Luxon, Zod
- Database: PostgreSQL

## API Documentation
Base URL: `http://localhost:4000`

Event Types
- `GET /api/event-types`
- `POST /api/event-types`
  - body: `{ "name": "Coffee Chat", "durationMinutes": 30, "slug": "coffee-chat" }`
- `PUT /api/event-types/:id`
- `DELETE /api/event-types/:id`

Availability
- `GET /api/availability`
- `PUT /api/availability`
  - body:
  ```json
  {
    "timezone": "America/New_York",
    "days": [
      { "dayOfWeek": 1, "ranges": [{ "start": "09:00", "end": "17:00" }] }
    ]
  }
  ```

Public Booking
- `GET /api/public/event-types/:slug`
- `GET /api/public/availability/:slug?date=YYYY-MM-DD`
- `POST /api/public/bookings/:slug`
  - body: `{ "name": "Jamie", "email": "jamie@example.com", "start": "2026-03-20T09:00:00-04:00" }`
- `GET /api/public/bookings/id/:id`

Meetings
- `GET /api/meetings?status=upcoming|past`
- `POST /api/meetings/:id/cancel`

## Setup

1. Install Node.js (v18 or newer).
2. Create a PostgreSQL database named `calendly_clone`.
3. Import the schema and seed data:
   - `psql -d calendly_clone -f database/schema.sql`
   - `psql -d calendly_clone -f database/seed.sql`
4. Backend setup:
   - `cd backend`
   - Create `.env` using `backend/.env.example`
   - `npm install`
   - `npm run dev`
5. Frontend setup:
   - `cd frontend`
   - Create `.env` using `frontend/.env.example`
   - `npm install`
   - `npm run dev`
6. Open `http://localhost:3000` to use the app.

## Deployment

Frontend (Vercel)
1. Push this repo to GitHub.
2. In Vercel, import the repo.
3. Set `Root Directory` to `frontend`.
4. Add environment variable `NEXT_PUBLIC_API_URL` to your backend URL.
5. Deploy.

Backend (Render or Railway)
1. Create a new Web Service.
2. Set `Root Directory` to `backend`.
3. Build command: `npm install`.
4. Start command: `npm run start`.
5. Add environment variables from `backend/.env.example`.

Database (Supabase)
1. Create a new project.
2. Go to SQL Editor.
3. Run `database/schema.sql` and then `database/seed.sql`.
4. Copy the Supabase connection string into `DATABASE_URL` in your backend.

## Notes
- This project assumes a default logged-in admin user with `id=1`.
- Availability is stored per day and used to generate slots for public booking.
- Bookings use UTC timestamps in the database to avoid timezone conflicts.
- Email notifications use SMTP. Add SMTP settings in `backend/.env` to enable confirmation and cancellation emails.

## Important Rules
- No login system. Admin pages assume a default user.
- UI focuses on Calendly-like layout and clarity.
- Double booking prevention happens in the backend.
# calendly_final
