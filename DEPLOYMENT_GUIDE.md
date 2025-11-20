# Deployment Guide for Mother India Stock Management

This guide will help you deploy your application using the best free-tier combination:
- **Database:** Supabase (PostgreSQL)
- **Backend:** Render (Node.js/Express)
- **Frontend:** Vercel (React)

## Prerequisites
- Accounts on [Supabase](https://supabase.com/), [Render](https://render.com/), and [Vercel](https://vercel.com/).
- Your code pushed to a GitHub repository.

---

## Step 1: Database Connection String
You have already provided your Supabase credentials.
**Your Connection String:**
`postgresql://postgres.knbgzutzgygdchrpgees:12345@aws-1-ap-northeast-2.pooler.supabase.com:6543/postgres`

Keep this handy for Step 2.

---

## Step 2: Backend Deployment (Render)
**You must deploy the Backend FIRST so you have a URL to give to the Frontend.**

1.  **Create a Web Service:**
    - Log in to [Render Dashboard](https://dashboard.render.com/).
    - Click **New +** -> **Web Service**.
    - Connect your GitHub repository.

2.  **Configure Service:**
    - **Name:** `mother-india-backend`
    - **Root Directory:** `server` (Important! This tells Render the backend is in the `server` folder)
    - **Environment:** `Node`
    - **Build Command:** `npm install`
    - **Start Command:** `npm start`
    - **Plan:** Free

3.  **Environment Variables:**
    - Scroll down to **Environment Variables** and add:
        - `DATABASE_URL`: Paste the connection string from Step 1.
        - `NODE_ENV`: `production`
        - `CLIENT_URL`: `https://mother-india-stock.vercel.app` (You can use `*` temporarily if you don't know your Vercel URL yet).

4.  **Deploy:**
    - Click **Create Web Service**.
    - Wait for deployment.
    - **Copy the Service URL** (e.g., `https://mother-india-backend.onrender.com`).

---

## Step 3: Frontend Deployment (Vercel)

1.  **Create a Project:**
    - Log in to [Vercel Dashboard](https://vercel.com/dashboard).
    - Click **Add New ...** -> **Project**.
    - Import your GitHub repository.

2.  **Configure Project:**
    - **Framework Preset:** Create React App.
    - **Root Directory:** Click `Edit` and select `client`. **(Crucial Step!)**

3.  **Environment Variables:**
    - Expand **Environment Variables**.
    - Add:
        - `REACT_APP_API_URL`: Paste your Render Backend URL from Step 2.
        - **Important:** Add `/api` at the end.
        - Example: `https://mother-india-backend.onrender.com/api`

4.  **Deploy:**
    - Click **Deploy**.

---

## Step 4: Final Connection
1.  Once Vercel deploys, copy your new Frontend URL (e.g., `https://mother-india-stock.vercel.app`).
2.  Go back to **Render** -> **Environment Variables**.
3.  Update `CLIENT_URL` to this exact Frontend URL.
