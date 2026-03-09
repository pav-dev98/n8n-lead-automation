# n8n Lead Automation Engine 🚀

This repository contains a real-time automation ecosystem designed to capture, process, and respond to new leads. It features an event-driven architecture connecting Supabase with communication services (Gmail/Telegram) through a self-hosted n8n instance.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Automation Engine | n8n (Self-hosted via Docker) |
| Database & Events | Supabase (PostgreSQL + Database Webhooks) |
| Networking | ngrok (Secure Reverse Proxy Tunneling) |
| Internal Persistence | PostgreSQL (n8n backend database) |
| Logic | JavaScript (Data transformation & Array manipulation) |
| Integrations | Gmail API & Telegram Bot API |

---

## 🏗️ System Architecture

```
Supabase (leads table)
        │
        │  INSERT trigger
        ▼
Supabase Webhook Dispatcher
        │
        │  POST request → static ngrok URL
        ▼
     ngrok Tunnel
        │
        │  Forwards to localhost:5678
        ▼
     n8n Engine
        │
        ├── Edit Fields (data cleaning)
        └── JS Node (.join() normalization)
                │
        ┌───────┴───────┐
        ▼               ▼
   Gmail API       Telegram Bot
 (welcome email)  (team alert)
```

1. **Trigger:** A new record is inserted into the Supabase `leads` table.
2. **Webhook Dispatcher:** Supabase sends a `POST` request to a static ngrok URL.
3. **Secure Tunnel:** ngrok forwards the traffic to local port `5678`.
4. **Processing (Middleware):**
   - Data cleaning via **Edit Fields** nodes.
   - JavaScript logic to transform data (e.g., using `.join()` to normalize interest arrays).
5. **Output Layer:**
   - **Email Marketing:** Automatic personalized welcome email via Gmail.
   - **Notifications:** Instant team alert via Telegram Bot.

---

## 📂 Project Structure

```
.
├── credentials/               # (Ignored) Local encryption keys & storage
├── docker/
│   └── docker-compose.yml     # Infrastructure: n8n + PostgreSQL
├── workflows/
│   └── SupabaseLeadThankYou.json
└── README.md
```

---

## 🐳 Infrastructure & Deployment

The system runs on Docker containers to ensure persistence and scalability.

**Services:**
- **n8n** — The workflow engine.
- **Postgres** — Dedicated database for n8n's internal data and execution history.

**Spin up the environment:**

To start the infrastructure in detached mode, run:

```bash
docker compose -f docker/docker-compose.yml up -d
```

---

## 🧠 Development Workflow

1. **Access:** Once the containers are up, go to [http://localhost:5678](http://localhost:5678).
2. **Import:** Import the `.json` file from the `workflows/` directory.
3. **Tunneling:** Ensure ngrok is pointing to port `5678` using your static domain.
4. **Versioning:** After making changes in the UI, download the workflow and replace the file in `workflows/` to keep Git history updated.

---

## 📈 Roadmap

- [ ] **Double Opt-In:** Implement email verification logic.
- [ ] **Data Backup:** Synchronize leads with Google Sheets for redundancy.