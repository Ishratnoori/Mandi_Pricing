# Mandi\_Pricing – Farmer’s Portal

A Next.js (App Router) web app that helps farmers and traders quickly find **live mandi crop prices**, view **local weather**, skim **agri news**, and use **smart search** to locate the **best nearby price** with map directions.

**Live:** [https://mandi-pricing.vercel.app](https://mandi-pricing.vercel.app)

---

## ✨ Features

* **Smart Search**: Enter your **state** and **crop** (e.g., “Rice”) to fetch the best nearby mandi price.
* **Auto Location Hint**: Detects your location (permission-based) to pre-fill the nearest state/area.
* **Live Mandi Prices Table**: See **Min / Max / Modal** prices (₹/Quintal), mandi name, and one‑click **Directions**.
* **Weather Snapshot**: Local current weather (temperature, conditions) to plan market trips.
* **Agri News Feed**: Headlines relevant to agriculture, policy updates, and commodity trends.
* **Clean UI**: TypeScript, Tailwind CSS, shadcn/ui components, responsive and accessible.

> UI strings seen in the current build: *Farmer's Portal, Mandi Prices, Weather, News, Smart Search, Your Location, Crop, Live Mandi Crop Prices, Directions.*

---

## 🏗️ Tech Stack

* **Framework**: Next.js 14+ (App Router) + TypeScript
* **Styling**: Tailwind CSS, CSS Modules, shadcn/ui, lucide-react icons
* **Package Manager**: pnpm
* **Deployment**: Vercel

> Repo layout suggests: `app/`, `components/`, `hooks/`, `lib/`, `public/`, `styles/`, `components.json` (shadcn), `next.config.mjs`, `postcss.config.mjs`, `tsconfig.json`.

---

## 📂 Project Structure

```
Mandi_Pricing/
├─ app/                 # App Router routes, layouts, pages
├─ components/          # Reusable UI components (tables, forms, cards)
├─ hooks/               # Custom React hooks (e.g., geolocation, fetch)
├─ lib/                 # API clients, helpers, constants
├─ public/              # Static assets
├─ styles/              # Tailwind/CSS files
├─ components.json      # shadcn/ui config
├─ next.config.mjs
├─ package.json
├─ pnpm-lock.yaml
└─ tsconfig.json
```

---

## 🔌 Data Sources (typical)

> Adjust to match your implementation.

* **Mandi Prices**: Agmarknet / eNAM / data.gov.in API (Govt of India commodity prices)
* **Weather**: OpenWeatherMap (Current Weather API)
* **News**: NewsAPI / gnews / other agri‑news feeds
* **Geocoding/Maps**: HTML5 Geolocation + Google Maps link for directions

---

## 🚀 Getting Started

### Prerequisites

* Node.js **18+**
* **pnpm** (recommended)

### Installation

```bash
pnpm install
```

### Local Development

```bash
pnpm dev
# open http://localhost:3000
```

### Build & Start

```bash
pnpm build
pnpm start
```

### Lint (if configured)

```bash
pnpm lint
```

---

## 🔐 Environment Variables

Create a `.env.local` in the project root. Example:

```bash
# Price API (choose one that you use)
AGMARKNET_API_KEY=""
PRICE_API_BASE_URL="https://api.data.gov.in/resource/<resource-id>"

# Weather
OPENWEATHER_API_KEY=""

# News
NEWS_API_KEY=""

# Maps (for any server-side geocoding or advanced maps)
NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=""

# CORS proxy (only if you’re using one; avoid in production when possible)
NEXT_PUBLIC_PROXY_URL=""
```

Update `lib/` clients to read from these keys. On **Vercel**, set the same variables in *Project Settings → Environment Variables* and redeploy.

---

## 🧭 How It Works

1. **Input**: User selects **State** and **Crop** in Smart Search.
2. **Fetch**: App calls price API with the filters (state/crop/date) and parses **Min/Max/Modal**.
3. **Augment**: If available, compute **distance** from user to mandi using geolocation and mandi coordinates.
4. **Display**: Render a **table** with mandi name, crop, prices, distance, and **Directions** link.
5. **Extras**: Weather widget pulls current local weather; News lists latest agri headlines.

**Directions link example** (no SDK needed):

```
https://www.google.com/maps/dir/?api=1&destination=<lat>,<lng>
```

---

## ✅ Accessibility & UX

* Keyboard‑navigable inputs and table
* Proper labels/aria for form controls
* Responsive layout (mobile‑first)
* Clear empty/error states (e.g., “Failed to fetch”)

---

## 🧰 Common Issues

### “Failed to fetch”

* **Missing API key**: Ensure keys are in `.env.local` and on Vercel.
* **Wrong endpoint/params**: Verify `resource_id`, query params, or date format.
* **CORS**: If the API blocks browser calls, route via a Next.js **Route Handler** under `app/api/*` to call server‑side.
* **Rate limits**: Add basic caching (Next.js `fetch` cache, `revalidate`, or in‑memory) and backoff.
* **Network**: Check HTTPS and that you aren’t mixing `http://` with `https://` on a secure page.

### Location not detected

* Ensure browser permission granted. Provide a manual state selector as fallback.

---

## 🛣️ Roadmap

* Historical price trends (charts)
* Filters: date range, variety/grade
* CSV/Excel export of price table
* Offline hints / PWA
* Multi‑language (hi/te/ta)
* Compare mandis side‑by‑side

---

## 🤝 Contributing

1. Fork the repo
2. Create a feature branch: `git checkout -b feat/awesome`
3. Commit: `git commit -m "feat: add awesome thing"`
4. Push: `git push origin feat/awesome`
5. Open a PR

Please follow conventional commits if possible.

---

## 📜 License

MIT

---

## 🙌 Acknowledgements

* Government of India open data initiatives (commodity pricing)
* OpenWeatherMap / News providers
* shadcn/ui, Tailwind CSS, Next.js community

---

## 🖼️ Screenshots
* Home – Smart Search & Widgets
<img width="1883" height="632" alt="image" src="https://github.com/user-attachments/assets/dc82a66a-c87e-4f2a-bee4-96d0a4461804" />
* Live Mandi Prices – Table view
<img width="1876" height="481" alt="image" src="https://github.com/user-attachments/assets/63b762c1-6d37-4ea1-969b-1f8f86bdc13e" />

---

## 📝 Notes for Maintainers

* Keep API clients in `lib/` small and typed.
* Centralize constants (state/crop lists) and re‑use across form + API layer.
* Prefer **server components** for data fetching when possible; stream UI for snappy loads.
* Validate inputs on both client and server route handlers.
