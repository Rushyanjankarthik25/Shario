## Shario

Pinterest-like image sharing app built with a React + Vite frontend and a Sanity.io backend.

### Features

- User authentication with Google OAuth
- Create, view, search, and categorize pins
- Save pins and view saved/created pins in a profile
- Pin details with related pins and comments
- Responsive Masonry grid layout

### Tech Stack

- Frontend: React 19, Vite, React Router, TailwindCSS, React Icons, react-masonry-css
- Auth: @react-oauth/google, jwt-decode
- Backend (CMS): Sanity v4 (schemas for users, pins, comments, saves)

### Monorepo Structure

```
backend/   # Sanity Studio (content schemas and studio config)
frontend/  # React app (Vite)
```

### Prerequisites

- Node.js 18+
- Sanity account and project (Project ID + dataset)
- Google OAuth Client ID (Web)

### Environment Variables

Create a `.env` file inside `frontend/` with:

```
VITE_GOOGLE_API_TOKEN=<your_google_oauth_client_id>
VITE_SANITY_PROJECT_ID=<your_sanity_project_id>
VITE_SANITY_TOKEN=<optional_sanity_api_token_if_needed>
```

Notes:

- `VITE_SANITY_TOKEN` is only required for actions that need authenticated writes from the browser (the current app uses anonymous writes via Sanity’s client depending on dataset rules; add a token if your dataset is private or you restrict mutations).
- Dataset is set to `production` by default.

### Backend (Sanity Studio)

Inside `backend/`:

1. Install deps

```
npm install
```

2. Configure `sanity.config.js` with your `projectId` and `dataset` (already present). If you created a new Sanity project, update these values.
3. Run the studio locally

```
npm run dev
```

4. (Optional) Deploy studio and GraphQL

```
npm run deploy
npm run deploy-graphql
```

Schemas included (`backend/schemaTypes/`):

- `user` (userName, image, googleId)
- `pin` (title, about, destination, category, image, userId, postedBy, save[], comments[])
- `comment` (postedBy, comment)
- `save` (postedBy, userId)
- `postedBy` (reference to user)

### Frontend (Vite React)

Inside `frontend/`:

1. Install deps

```
npm install
```

2. Start dev server

```
npm run dev
```

3. Build / Preview

```
npm run build
npm run preview
```

Key files:

- `src/client.jsx`: Sanity client and image URL builder
- `src/utils/data.jsx`: GROQ queries and categories
- `src/container/Home.jsx`: App shell, sidebar, router mount
- `src/container/Pins.jsx`: Routes for feed, search, create, detail
- `src/components/Login.jsx`: Google OAuth login and user bootstrap
- `src/components/Feed.jsx`: Category feed or general feed
- `src/components/Pin.jsx`: Pin card with save/download/delete
- `src/components/PinDetail.jsx`: Details, comments, related pins
- `src/components/UserProfile.jsx`: Created vs saved pins, logout

### Running End-to-End Locally

1. Start Sanity Studio: `cd backend && npm run dev`
2. Start frontend: `cd ../frontend && npm run dev`
3. Ensure `.env` values exist in `frontend/` and that Sanity projectId/dataset match `backend/sanity.config.js`.

### Notes & Tips

- If you restrict dataset access in Sanity, set up a CORS origin for your dev URL and provide `VITE_SANITY_TOKEN` for mutations.
- Update Google OAuth authorized JavaScript origins to match your dev URL (e.g., `http://localhost:5173`).
- The app expects user info in `localStorage` under `user` post-login; clearing localStorage will log you out.

### Scripts Reference

Backend (from `backend/`):

- `npm run dev` – run Sanity Studio locally
- `npm run build` – build studio
- `npm run deploy` – deploy studio to Sanity hosting
- `npm run deploy-graphql` – deploy GraphQL API

Frontend (from `frontend/`):

- `npm run dev` – start Vite dev server
- `npm run build` – build for production
- `npm run preview` – preview production build

### License

UNLICENSED (per backend package.json). Update as needed.
