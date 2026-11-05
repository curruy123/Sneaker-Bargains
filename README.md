# Sneaker Bargains

**Find the best price for any sneaker, across every resale platform, in one search.**

Sneaker Bargains is a full-stack web app that pulls live resale listings for a sneaker from multiple platforms and shows them side by side, so you can see the price range at a glance and save the shoes you're watching.

Built by a team of 4 as a software engineering term project.

---

## Features

- **Search any sneaker** and get matching products with images, colorways and SKUs
- **Filter by platform** to compare only the resale sites you care about
- **Price comparison** across platforms, with a visual price range for each shoe
- **Google sign-in and saved wishlist** (Firebase), so your watchlist follows you
- **Keyboard accessible**, with ARIA roles and shortcuts throughout
- **Mock mode** that runs the whole app on saved sample data, with no API key needed

## How it works

```
React + TypeScript frontend  ──►  Java REST API (Spark)  ──►  Sneaker pricing API
         │                              │
     Firebase                    Guava cache layer
 (sign-in, wishlist)          (avoids repeat API calls)
```

- **Frontend:** React and TypeScript (Vite), styled with Bootstrap, Material UI and Ant Design. State is managed with a reducer, and type guards validate every server response.
- **Backend:** a Java server built with Spark that exposes three endpoints. Each one goes through a caching proxy (Guava), so repeat searches don't hit the paid API again.
- **Data:** live listings from a real-time sneaker pricing API (RapidAPI), or saved JSON responses in mock mode.

### API endpoints (`localhost:3232`)

| Endpoint | Returns |
|---|---|
| `GET /sneakers?query=...` | Products matching a search |
| `GET /platforms` | Resale platforms available for filtering |
| `GET /price_stats?sku=...` | A sneaker's prices across platforms |

---

## Run it locally

**Backend** (Java 17+, Maven)
```bash
cd backend
mvn package
# then run server.Server (starts on port 3232)
```

**Frontend** (Node 18+)
```bash
cd frontend
npm install
npm run dev
```

Mock mode is on by default (`frontend/src/data/mockingMode.ts`), so the app works without any API keys. For live data, add your own RapidAPI key and Firebase config to the backend and frontend config files.

## Testing

- **Frontend:** DOM tests for every component (including ones that only appear after user actions) and unit tests for the data layer, using React Testing Library
- **Backend:** JUnit tests for JSON parsing and serialization, plus integration tests against the mock server

```bash
cd frontend && npm test
cd backend && mvn test
```

## Tech stack

React · TypeScript · Vite · Bootstrap · Material UI · Ant Design · Java · Spark · Guava · Moshi · Firebase · React Testing Library · JUnit

## Team

Zeeshan Bhalwani · Omer Chaudhry · Safae Merigh · Kyle Sohn
