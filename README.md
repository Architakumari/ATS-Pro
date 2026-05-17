# ATS Pro v2 — Smart Resume Screening & Hiring Platform

ATS Pro is a Flask-based smart resume screening and hiring platform designed to simplify candidate evaluation and recruitment workflows. The platform helps recruiters analyze resumes, calculate ATS scores, manage candidates, and streamline hiring processes through an interactive dashboard.

---

## Features

### Candidate Features

* Resume upload and analysis
* ATS score calculation
* Skill matching and evaluation
* Resume parsing and candidate ranking
* Authentication system for users

### Recruiter Features

* Recruiter dashboard and analytics
* Candidate management system
* Resume comparison and filtering
* Job listing and management
* Recruitment insights and tracking

### Technical Features

* RESTful API integration
* Flask backend architecture
* SQLite database integration
* Responsive UI using HTML, CSS, and JavaScript
* Secure authentication modules
* Dynamic dashboard components

---

# Tech Stack

| Category   | Technologies            |
| ---------- | ----------------------- |
| Backend    | Flask (Python)          |
| Frontend   | HTML, CSS, JavaScript   |
| Database   | SQLite                  |
| Charts     | Chart.js                |
| UI         | Glassmorphism UI Design |
| Deployment | Gunicorn                |

---

# Project Structure

```bash
ATS_PRO/
│
├── static/
│   ├── css/
│   ├── js/
│   └── uploads/
│
├── templates/
│   ├── analytics.html
│   ├── analyze.html
│   ├── candidates.html
│   ├── company_analytics.html
│   ├── company_compare.html
│   ├── company_jobs.html
│   ├── home.html
│   ├── jobs.html
│   ├── login.html
│   └── register.html
│
├── app.py
├── requirements.txt
├── Procfile
├── README.md
└── .env.example
```

---

# Installation & Setup

## Clone Repository

```bash
git clone https://github.com/Architakumari/ATS-Pro.git
cd ATS-Pro
```

## Create Virtual Environment

```bash
python -m venv venv
```

### Activate Environment

#### Windows

```bash
venv\Scripts\activate
```

#### Linux / MacOS

```bash
source venv/bin/activate
```

---

# Install Dependencies

```bash
pip install -r requirements.txt
```

---

# Run Application

```bash
python app.py
```

Application will run at:

```bash
http://127.0.0.1:5000
```

---

# Main Modules

## Resume Analysis

Analyzes uploaded resumes and calculates ATS scores based on skills and job requirements.

## Candidate Management

Allows recruiters to view, manage, and compare candidate profiles.

## Analytics Dashboard

Provides hiring analytics, candidate insights, and recruitment statistics.

## Job Management

Supports job posting, candidate tracking, and hiring workflows.

---

# Future Improvements

* PostgreSQL integration
* AI-based resume recommendations
* Interview scheduling system
* Email notifications
* Cloud deployment support
* Advanced recruiter analytics

---

# Author

**Archita Kumari**

GitHub: [https://github.com/Architakumari](https://github.com/Architakumari)

---

# License

This project is developed for educational and learning purposes.
