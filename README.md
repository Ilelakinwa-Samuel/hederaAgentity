# Hedera Agentity — Monorepo (Frontend + Backend)

Agentity is a full-stack platform for **registering, simulating, auditing, and executing AI agents** with **verifiable blockchain traceability** and **microtransaction settlement on Hedera**.

This repository is a **hackathon-friendly wrapper repo** that contains two projects as **Git submodules**:
- **Frontend** (React + Vite): `./frontend`
- **Backend API** (Node.js + Express + Sequelize + Supabase): `./backend`

> Why submodules? You get a single repo to share/submit, while keeping frontend and backend as independent repos.


## 🌐 Live Demo (Deployed)

- **Frontend (UI):** https://hederaagentityfrontend.onrender.com  
- **Backend (API):** https://hederaagentitybackend.onrender.com  
- **Swagger API Docs:** https://hederaagentitybackend.onrender.com/docs :contentReference[oaicite:1]{index=1}


## 📦 Repo Structure

```bash
hederaAgentity/
  frontend/        # Submodule: Agentity-AI/hederaAgentityFrontend
  backend/         # Submodule: Agentity-AI/hederaAgentityBackend
  .gitmodules
  README.md
````


## ✅ Prerequisites

* **Node.js 18+** (recommended)
* **npm** (bundled with Node)
* **Git**
* Optional (for local DB via docker-compose):

  * **Docker Desktop**


## 🚀 Quick Start (Best for Teammates / Judges)

### 1) Clone this repo **with submodules**

```bash
git clone --recurse-submodules https://github.com/Ilelakinwa-Samuel/hederaAgentity.git
cd hederaAgentity
```

If you already cloned without submodules:

```bash
git submodule update --init --recursive
```


## 🧠 What the Backend Does (High-Level)

The backend supports:

* **Auth** via Supabase (JWT + httpOnly cookies)
* **Agent management** (register / verify / list agents)
* **Simulation engine** (sandboxed simulation runs)
* **Smart contract auditing** (submit source or repo for audit)
* **Hedera** integration for agent wallet/microtransactions (optional setup)
* Optional integrations:

  * **Chainlink CRE**
  * **AWS KMS** ([GitHub][1])


## 🛠️ Local Development

### A) Run Backend Locally

#### 1) Install deps

```bash
cd backend
npm install
```

#### 2) Create `backend/.env`

Backend requires the following environment variables. (Add only what you use.)

**Required**

```env
DATABASE_URL=
SUPABASE_URL=
SUPABASE_SERVICE_ROLE_KEY=
SUPABASE_ANON_KEY=
```

**Optional — Chainlink CRE**

```env
CRE_WEBHOOK_URL=
CRE_API_KEY=
```

**Optional — Hedera**

```env
HEDERA_OPERATOR_ID=
HEDERA_OPERATOR_KEY=
HEDERA_NETWORK=testnet
```

**Optional — AWS KMS**

```env
AWS_REGION=
AWS_KMS_KEY_ID=
```

([GitHub][1])

#### 3) Start backend

```bash
npm run dev
```

Backend runs on:

* `http://localhost:5000` ([GitHub][1])

Swagger docs (local):

* `http://localhost:5000/docs` ([GitHub][1])


### B) Run Frontend Locally

#### 1) Install deps

```bash
cd ../frontend
npm install
```

#### 2) Configure environment (recommended)

Create `frontend/.env`:

```env
VITE_API_URL=http://localhost:5000
```

> If the frontend is still hardcoded to a deployed API URL, update it to use `import.meta.env.VITE_API_URL` so you can switch between local and deployed backends easily.

#### 3) Start frontend

```bash
npm run dev
```

Frontend runs on:

* `http://localhost:5173` (Vite default)

---

## 🧪 Typical Demo Flow (Hackathon Friendly)

Use the deployed demo or run locally.

### Option 1: Use Deployed (fastest)

1. Open UI: [https://hederaagentityfrontend.onrender.com](https://hederaagentityfrontend.onrender.com)
2. Open API docs: [https://hederaagentitybackend.onrender.com/docs](https://hederaagentitybackend.onrender.com/docs) ([GitHub][1])
3. Use Swagger “Try it out” to:

   * Register/Login
   * Register an agent
   * Run a simulation / audit
   * View results

### Option 2: Local UI + Local API (best for offline judging)

1. Run backend locally (`localhost:5000`)
2. Set `VITE_API_URL=http://localhost:5000`
3. Run frontend locally (`localhost:5173`)


## 🔐 Authentication Notes (Backend)

Auth endpoints:

* `POST /auth/register`
* `POST /auth/login`
* `POST /auth/logout` ([GitHub][1])

Backend returns:

* `jwt` (Supabase access token)

And also sets:

* `agentity_jwt` cookie (httpOnly)

Protected endpoints accept either:

* `Authorization: Bearer <jwt>`
* or `agentity_jwt` cookie ([GitHub][1])


## 🧩 Working With Submodules (Important)

### Clone + init submodules

```bash
git clone --recurse-submodules https://github.com/Ilelakinwa-Samuel/hederaAgentity.git
```

### Pull updates safely

```bash
git pull
git submodule update --init --recursive
```

### Update submodules to latest remote commits

```bash
git submodule update --remote --merge
```

### Commit submodule pointer updates

If you updated a submodule and want this wrapper repo to point to the new commit:

```bash
git add frontend backend
git commit -m "Update submodule pointers"
git push
```


## 🐳 Optional: Postgres via Docker (If Needed)

If you want a local Postgres instance (and your backend is configured for it), you can use:

```bash
cd backend
docker compose up -d
```

Stop it:

```bash
docker compose down
```

> Make sure your `DATABASE_URL` matches the docker-compose credentials/port.

---

## 🧯 Troubleshooting

### “frontend/ backend/ is empty”

You didn’t init submodules:

```bash
git submodule update --init --recursive
```

### “Password authentication is not supported”

GitHub no longer supports password pushes over HTTPS. Use:

* **SSH** (recommended), or
* a **GitHub Personal Access Token** as your password.

### CORS / Cookies issues

If you rely on cookies (`withCredentials: true`), then:

* backend must allow credentials in CORS
* frontend must call API with credentials enabled
* allowed origins must include your frontend domain


## 📚 Extra Docs

Backend includes additional setup documentation:

* `backend/HEDERA_SETUP.md` (if present)
* Swagger at `/docs` for endpoint exploration/testing ([GitHub][1])

---

## 🏁 Hackathon Notes / Submission Checklist

* [ ] Live UI link works
* [ ] Live API link works
* [ ] Swagger `/docs` loads
* [ ] Demo account or clear signup/login instructions
* [ ] Env var checklist included (this README)
* [ ] “How to run locally” works on a fresh machine

---

## 📜 License

Hackathon project — add a license if required by the event.

```

If you want, I can also generate (copy-paste):
1) a **root `package.json`** so you can run everything from the repo root (`npm run dev:frontend`, `npm run dev:backend`), and  
2) a **“Judges Quick Demo”** section that lists exact endpoints to hit in Swagger (register → login → register agent → run simulation → view results) using the backend’s documented routes. :contentReference[oaicite:10]{index=10}

**a.** Want me to add a root `package.json` with scripts to start both apps easily?  
**b.** Want a “Demo Walkthrough” section with concrete Swagger steps + example request bodies?
::contentReference[oaicite:11]{index=11}
```

[1]: https://github.com/Agentity-AI/hederaAgentityBackend "GitHub - Agentity-AI/hederaAgentityBackend · GitHub"
