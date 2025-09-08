# 🌸 Shario

A Pinterest-style visual discovery and sharing platform built with React + Vite on the frontend and Sanity.io as the headless CMS.

Shario lets users create, save, and explore themed pins with a clean UI, smooth Google login, and responsive masonry layout.

## ✨ Features

- 🔑 Google OAuth authentication – one-click login & session persistence
- 📌 Pins management – create, view, categorize, and search pins
- ❤️ Save pins – keep your favorite pins in a personal collection
- 👤 User profiles – see created and saved pins, with logout option
- 💬 Pin details – view related pins, add comments, engage with community
- 🧱 Responsive masonry grid – dynamic layout that adapts to any screen

## 🛠️ Tech Stack

- **Frontend**: React 19, Vite, React Router, TailwindCSS, React Icons, react-masonry-css
- **Auth**: @react-oauth/google, jwt-decode
- **Backend (CMS)**: Sanity v4 with structured schemas for users, pins, saves, and comments

## 📂 Monorepo Structure

```
shario/
├── backend/    # Sanity Studio (content schemas + studio config)
└── frontend/   # React app (Vite + Tailwind)
```

## ⚡ Quick Start

### Prerequisites

- Node.js 18+
- Sanity account + project (Project ID + dataset)
- Google OAuth Client ID (type: Web)

### Environment Variables (`frontend/.env`)

```
VITE_GOOGLE_API_TOKEN=<your_google_oauth_client_id>
VITE_SANITY_PROJECT_ID=<your_sanity_project_id>
VITE_SANITY_TOKEN=<optional_if_dataset_private>
```

💡 `VITE_SANITY_TOKEN` is only required if your dataset is private or write-restricted.

---

## 🚀 Run Locally

### Backend (Sanity Studio)

```bash
cd backend
npm install
npm run dev   # starts Sanity Studio at http://localhost:3333
```

Optional:

```bash
npm run deploy         # deploy Studio to Sanity Hosting
npm run deploy-graphql # publish Sanity GraphQL API
```

### Frontend (React + Vite)

```bash
cd frontend
npm install
npm run dev     # starts dev server at http://localhost:5173
npm run build   # production build
npm run preview # preview production build
```

---

## 🏗️ Sanity Schemas

Located in `backend/schemaTypes/`:

- **user** → userName, image, googleId
- **pin** → title, about, destination, category, image, postedBy, saves[], comments[]
- **comment** → postedBy, comment
- **save** → postedBy, userId
- **postedBy** → reference to user

---

## 🔧 Project Notes

- Make sure Sanity CORS origins include your dev and production frontend URLs.
- Add your frontend URLs to Google OAuth Authorized JavaScript Origins.
- User data is persisted in `localStorage` under `user`. Clearing it = logout.
- Images are fetched from Sanity asset pipeline with dynamic transformations.

---

## 🌐 Deployment

- **Frontend**: deploy easily with Vercel, Netlify, or Render
- **Backend**: deploy Sanity Studio with `npm run deploy`

---

## 📜 License

This project is currently **UNLICENSED** (per backend package.json).  
Update or add a license file before public release.

---

✨ Shario is designed to be a fun, minimal, and extensible playground for image-driven social apps.  
Customize it, extend schemas, and make it yours!
