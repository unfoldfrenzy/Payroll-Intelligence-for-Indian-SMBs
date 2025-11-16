# SMB Payroll Benchmark — Auto-Updating Comparison Page

Overview
- React frontend fetches canonical benchmark data from a backend API and renders an interactive comparison table targeting Indian SMB buyers.
- Backend collects data from multiple sources on a schedule (scrapers/adapters), normalizes it into a canonical schema, and exposes GET /api/benchmarks and POST /api/leads (for lead capture).
- Auto-update implemented via GitHub Actions or a scheduler (serverless cron). Each data update includes evidence links and timestamps.

Key components
- frontend/: React app
- server/: Node/Express API to serve benchmark JSON and accept leads
- scripts/: scrapers/adapters which fetch and normalize data from vendor websites, G2/Capterra, Play Store, etc.
- .github/workflows/sync-benchmarks.yml: optional GitHub Actions scheduled job to refresh benchmark data and commit to repo.

Running locally (MVP)
- Backend:
  - NODE_ENV=development
  - npm install
  - npm run start (starts Express on port 4000)
- Frontend:
  - cd frontend
  - npm install
  - npm run start (starts React dev server on port 3000)
- The frontend expects GET http://localhost:4000/api/benchmarks and POST http://localhost:4000/api/leads

Notes
- Scraping third-party sites may violate terms of service. Prefer vendor-supplied data or official APIs.
- Add a human-review step for large automatic updates.