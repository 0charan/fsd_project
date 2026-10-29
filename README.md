# CampusPulse – simple College Activity & Event Portal

## Run
```
npm install
npm start          # http://localhost:3000
```
(`npm run reset` deletes data.json so demo data is re-seeded.)

## Demo logins
| Role | Email | Password |
|---|---|---|
| Student | rahul@college.edu | student123 |
| Organizer | org@college.edu | org123 |
| Admin | admin@college.edu | admin123 |

## Demo flow
Student registers (Quiz Championship is full -> waitlist) -> pass with QR appears in My Activity ->
log in as organizer -> enter pass code in Check in (second scan is rejected) -> Manage -> Award points ->
student profile/leaderboard update -> certificate with verify QR. Admin edits point rules; changes show in the audit log.

## Structure
- `server.js` Express API, JWT-style signed tokens, scrypt password hashing, role middleware, rate-limited login, audit log
- `data.json` auto-created JSON database (users, events, regs, rules, audit)
- `public/` frontend (vanilla JS, hash routing, no build step)

## Scaled-down vs the full spec
Left out: teams, volunteers, brackets, stalls, approvals workflow, notifications, CSV export.
Storage is a JSON file instead of MongoDB so nothing else needs installing; the data shapes map directly to Mongo collections.
Set `SECRET` env var in production.

## MongoDB Atlas
1. Atlas -> Database Access -> add a user (username + password).
2. Atlas -> Network Access -> add YOUR IP (or `0.0.0.0/0` for a demo / hosted app).
3. Atlas -> Connect -> Drivers -> copy the `mongodb+srv://...` string.
4. `cp .env.example .env`, paste the string into `MONGODB_URI` (replace `<password>`), set `SECRET`.
5. `npm install && npm start` - you should see "Connected to MongoDB Atlas".
Without `MONGODB_URI` it falls back to `data.json`. App data is stored in database `campusportal`, collection `state`.
