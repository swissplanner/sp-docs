# API Reference & Data Specs

This page documents the API endpoints, global JavaScript configurations, and JSON data schemas used by **Swiss Travel Planner**.

---

## 1. Backend Proxy Endpoint (`/api/chat`)

### `POST /api/chat`

Routes AI queries through a Node.js Express server or Vercel Serverless Function to fetch live transport fares and exchange rates.

#### Request Body Schema

```json
{
  "season": "Jun-Agu",
  "days": 5,
  "entry": "Zurich"
}
```

#### Response Payload Schema (`200 OK`)

```json
{
  "chf_to_usd": 1.10,
  "swiss_travel_pass": {
    "3day": 244,
    "4day": 295,
    "6day": 389,
    "8day": 429,
    "15day": 469
  },
  "swiss_half_fare_card": 120,
  "berner_oberland_pass": {
    "3day": 230,
    "6day": 290
  },
  "tell_pass": {
    "2day": 210,
    "5day": 250
  },
  "saver_day_pass_avg": 52,
  "cable_cars": {
    "gornergrat": { "adult": 98, "child": 49 },
    "schilthorn": { "adult": 105, "child": 53 },
    "first_grindelwald": { "adult": 66, "child": 33 },
    "rigi": { "adult": 72, "child": 36 },
    "pilatus": { "adult": 72, "child": 36 },
    "harder_kulm": { "adult": 36, "child": 18 },
    "jungfraujoch": { "adult": 247, "child": 124 }
  },
  "with_half_fare_discount": 0.5,
  "with_travel_pass_free": ["rigi", "pilatus", "harder_kulm"]
}
```

---

## 2. Global JavaScript API (`window.APP_CONFIG`)

Access or modify the configuration programmatically via JavaScript:

```javascript
// Get active branding
console.log(window.APP_CONFIG.branding.siteName); // "Swiss Travel Planner"

// Get default exchange rate
console.log(window.APP_CONFIG.defaults.chf_to_usd); // 1.10

// Inspect AI provider options
console.log(window.APP_CONFIG.ai.providers);
```

---

## 3. Browser Local Storage Keys

| Key | Type | Description |
| :--- | :--- | :--- |
| `swiss_travel_planner_ai_config` | JSON String | Stores user-selected AI provider, endpoint, model, and API key. |
| `swiss_travel_planner_pricing_cache` | JSON String | Cached pricing data object. |
| `swiss_travel_planner_pricing_cache_time` | Timestamp | Epoch timestamp (ms) when cache was populated. |
