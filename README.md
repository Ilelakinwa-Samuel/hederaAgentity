# 🚀 Hedera Agentity

A full-stack AI-powered application built during a hackathon, combining a modern frontend and scalable backend.

---

## 📦 Project Structure

```
hederaAgentity/
├── frontend/   # React / Next.js frontend
├── backend/    # Node.js / API backend
```

---

## 🧠 Overview

This repository acts as a **monorepo wrapper** combining:

* Frontend: User interface and client interactions
* Backend: API, business logic, and integrations

Both are managed as **Git submodules** for modular development.

---

## ⚙️ Setup Instructions

### 1. Clone the repository

```bash
git clone --recurse-submodules git@github.com:Ilelakinwa-Samuel/hederaAgentity.git
cd hederaAgentity
```

---

### 2. Install dependencies

#### Frontend

```bash
cd frontend
npm install
```

#### Backend

```bash
cd ../backend
npm install
```

---

### 3. Run the application

#### Start backend

```bash
cd backend
npm run dev
```

#### Start frontend

```bash
cd ../frontend
npm run dev
```

---

## 🔗 Environment Variables

Create `.env` files in both `frontend` and `backend` folders.

Example:

```
PORT=5000
API_URL=http://localhost:5000
```

---

## 🔄 Working with Submodules

### Clone with submodules

```bash
git clone --recurse-submodules <repo-url>
```

### Update submodules

```bash
git submodule update --remote
```

---

## 🛠 Tech Stack

* Frontend: React / Next.js
* Backend: Node.js / Express
* Version Control: Git + Submodules

---

## 🚀 Deployment

* Frontend: Vercel / Netlify
* Backend: Render / Railway / AWS

---

## 👥 Contributors

* Team Agentity AI

---

## 📜 License

MIT License
