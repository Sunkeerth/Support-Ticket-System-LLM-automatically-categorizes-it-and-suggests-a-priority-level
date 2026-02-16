# 🚀 Support Ticket System with LLM Auto-Classification

[![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?logo=docker)](https://www.docker.com/)
[![Django](https://img.shields.io/badge/Django-4.2-092E20?logo=django)](https://www.djangoproject.com/)
[![React](https://img.shields.io/badge/React-18-61DAFB?logo=react)](https://reactjs.org/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT-412991?logo=openai)](https://openai.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-336791?logo=postgresql)](https://www.postgresql.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A **production-ready full-stack support ticket system** that automatically suggests ticket **category and priority using LLM (OpenAI GPT)** while allowing manual override.

Built with **Django + React + PostgreSQL + Docker** and designed with real-world architecture for AI/full-stack engineering roles.

---

# ✨ Features

- 🤖 **LLM Auto-Classification** (category + priority suggestions)
- ✏️ Editable suggestions (user override allowed)
- 📊 Live stats dashboard (auto refresh)
- 🔎 Search & filter tickets
- 🧾 Full CRUD ticket management
- 🐳 Dockerized full stack setup
- 🛡️ Graceful fallback if LLM fails
- ⚡ Clean scalable architecture

---

# 🧰 Tech Stack

| Layer | Technology |
|------|-----------|
| Frontend | React |
| Backend | Django + DRF |
| Database | PostgreSQL |
| AI | OpenAI GPT |
| Container | Docker Compose |

---

# 🏗️ Architecture

```
React Frontend → Django API → PostgreSQL
                       ↓
                    OpenAI GPT
```

Flow:
1. User types ticket description  
2. Frontend calls `/api/tickets/classify/`  
3. Backend sends prompt to OpenAI  
4. Suggested category & priority returned  
5. User can edit and submit  

---

# ⚙️ Setup Instructions

## 1️⃣ Add OpenAI API Key

Create `.env` file in project root:

```env
OPENAI_API_KEY=your_openai_api_key_here
```

⚠️ Do NOT upload `.env` to GitHub.

---

## 2️⃣ Run Project with Docker

```bash
docker compose up --build
```

First run may take few minutes.

---

## 3️⃣ Access Application

Frontend:
```
http://localhost:3000
```

Backend API:
```
http://localhost:8000/api/
```

---

# 🧠 How LLM Integration Works

### Endpoint
```
POST /api/tickets/classify/
```

### Request
```json
{
  "description": "Payment failed during checkout"
}
```

### Prompt Used
```
You are a ticket classifier.

Classify ticket into:
billing, technical, account, general

Assign priority:
low, medium, high, critical

Return JSON only:
{"category":"...","priority":"..."}

Description: {description}
```

### Backend Validation
- Ensures valid category & priority
- If API fails → returns null safely
- Ticket creation never blocked

### Frontend Behaviour
- 500ms debounce while typing
- Auto suggestion shown
- User can override anytime

---

# 📡 API Endpoints

| Method | Endpoint | Description |
|--------|---------|-------------|
| POST | `/api/tickets/` | Create ticket |
| GET | `/api/tickets/` | List tickets |
| GET | `/api/tickets/?search=` | Search/filter |
| PATCH | `/api/tickets/<id>/` | Update ticket |
| GET | `/api/tickets/stats/` | Stats dashboard |
| POST | `/api/tickets/classify/` | LLM classify |

---

# 🗄️ Database Schema

### Ticket Model

| Field | Type |
|------|------|
| title | CharField |
| description | TextField |
| category | billing/technical/account/general |
| priority | low/medium/high/critical |
| status | open/in_progress/resolved/closed |
| created_at | DateTime |

---

# 🧪 Testing

Backend:
```bash
docker compose exec backend python manage.py test
```

Frontend:
```bash
docker compose exec frontend npm test
```

---

# 📁 Project Structure

```
.
├── backend/
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── manage.py
│   ├── backend/
│   └── tickets/
│       ├── models.py
│       ├── views.py
│       ├── serializers.py
│       ├── llm_client.py
│       └── urls.py
│
├── frontend/
│   ├── Dockerfile
│   ├── package.json
│   └── src/
│       ├── App.js
│       ├── api.js
│       └── components/
│
├── docker-compose.yml
└── README.md
```

---

# 🔐 Environment Variables

| Variable | Required | Description |
|---------|----------|-------------|
| OPENAI_API_KEY | Yes | OpenAI key |
| POSTGRES_DB | No | Database name |
| POSTGRES_USER | No | DB user |
| POSTGRES_PASSWORD | No | DB password |

---

# 🚀 Future Improvements

- JWT Authentication
- Role-based dashboard
- Email notifications
- Ticket assignment system
- Vector search (RAG)
- Local LLM support
- Kubernetes deployment

---

# 👨‍💻 Author

**Sunkeerth**  
AI/ML Engineer | Full-Stack Developer  

Interested in:
- AI systems
- Robotics simulation
- LLM apps
- VR education platforms

---

# 🤝 Contributing
Pull requests welcome.

1. Fork repo  
2. Create branch  
3. Commit  
4. Open PR  

---

# 📜 License
MIT License

---

# ⭐ Star this repo if useful
Supports visibility and motivates further development.
