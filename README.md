# ATS Pro v2 — AI-Powered Resume & Hiring Platform

Full-stack web app with **two distinct user flows**, built with Flask + SQLite + Claude AI + 3D Glassmorphism UI.

---

## Two Flows, One Platform

### Flow 1 — Job Seekers (No Account Needed) → `/check`
Upload a resume and instantly get:
- Overall ATS score (0–100) with sub-scores: Content, Format, Language, Keywords
- Role-specific scoring — pick from 8 preset roles or type any custom role
- Language & grammar issues flagged with severity + exact fixes
- Before/after rewrite suggestions for weak bullet points
- Stronger word choice replacements
- Missing ATS keywords to add
- Formatting tips for better ATS pass rates
- Numbered priority action plan

**No login. No account. Free. Results in ~10 seconds.**

### Flow 2 — Companies & Recruiters (Account Required) → `/company`
Full hiring dashboard:
- **Analyze Resume** — ATS score + AI Hire / Maybe / Reject recommendation with reasoning
- **Green & Red Flags** — automatically spotted by AI
- **Skill Gap Analysis** — matched, missing, bonus skills
- **Interview Questions** — AI-generated per candidate profile
- **Compare & Decide** — select 2–5 candidates, get ranked leaderboard + interview/reject/shortlist lists
- **Candidate Pipeline** — New → Shortlisted → Interviewing → Offered / Rejected
- **Analytics** — 8 Chart.js charts: score bands, role breakdown, hire decisions, trend, skill gaps, pipeline status, company match, avg by role
- **Job Roles Manager** — 8 built-in roles + add custom roles

---

## Quick Start (Local)

```bash
cd ats_pro
python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

# Optional — add your Anthropic key (app works in demo mode without it)
cp .env.example .env
# Edit .env: ANTHROPIC_API_KEY=sk-ant-your-key-here

python app.py
# Open http://localhost:5000
```

**Demo company login:** `demo@company.com` / `demo1234`

---

## Deploy to Internet

### Railway (Recommended — free, ~2 min setup)
1. Push code to a GitHub repo
2. [railway.app](https://railway.app) → New Project → Deploy from GitHub
3. Add env var: `ANTHROPIC_API_KEY=sk-ant-...`
4. Done — `Procfile` handles everything

### Render (Free tier)
- Build command: `pip install -r requirements.txt`
- Start command: `gunicorn app:app --bind 0.0.0.0:$PORT --workers 2 --timeout 120`
- Add env var: `ANTHROPIC_API_KEY`

### Ubuntu VPS
```bash
# Install nginx + app
sudo apt install python3-venv nginx certbot python3-certbot-nginx -y
git clone <repo> /var/www/ats_pro && cd /var/www/ats_pro
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt gunicorn

# /etc/systemd/system/ats_pro.service
[Service]
WorkingDirectory=/var/www/ats_pro
Environment="ANTHROPIC_API_KEY=sk-ant-..."
Environment="SECRET_KEY=<random-64-char-string>"
ExecStart=/var/www/ats_pro/venv/bin/gunicorn app:app --bind 127.0.0.1:5000 --workers 4 --timeout 120
Restart=always

# Nginx proxy + SSL
sudo certbot --nginx -d yourdomain.com
```

---

## API Reference

### Guest (no auth required)
```
POST /api/guest/check
  Form fields: resume (file), check_type (overall|role), role (string)
```

### Company Auth
```
POST /api/company/register   {name, company, email, password, industry}
POST /api/company/login      {email, password}
GET  /api/company/me         → returns company profile
```

### Company (Bearer token required)
```
POST   /api/company/analyze                    resume upload (multipart)
GET    /api/company/candidates                 list + filter/search/sort
GET    /api/company/candidates/<id>            single detail
PATCH  /api/company/candidates/<id>/update     {status, hire_recommendation, notes}
DELETE /api/company/candidates/<id>            remove
POST   /api/company/compare                    {candidate_ids: [...], role}
GET    /api/company/jobs                       all roles
POST   /api/company/jobs                       {emoji, title, department, required_skills}
DELETE /api/company/jobs/<id>                  delete custom role
GET    /api/company/analytics                  full chart data
GET    /api/company/dashboard                  summary stats
```

---

## Tech Stack

| Layer | Tech |
|-------|------|
| Backend | Python 3.12 + Flask 3 |
| Database | SQLite (stdlib) |
| Auth | Custom JWT (HMAC-SHA256) |
| AI | Anthropic Claude API |
| PDF | pypdf |
| DOCX | python-docx |
| Charts | Chart.js |
| UI | 3D Glassmorphism CSS template |
| Deployment | Gunicorn |

---

## Production Notes
- Change `SECRET_KEY` to a long random string before deploying
- Set `FLASK_DEBUG=false` in production
- For high traffic, consider PostgreSQL instead of SQLite
- Add rate limiting on `/api/guest/check` to prevent abuse

© 2026 ATS Pro
