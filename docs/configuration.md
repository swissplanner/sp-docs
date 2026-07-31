# Configuration Guide

All site settings, default pricing values, exchange rates, and AI provider configurations are centrally managed in `config.js`.

---

## Configuration Overview (`config.js`)

The configuration object is attached to `window.APP_CONFIG` so it is instantly available across the entire application:

```javascript
window.APP_CONFIG = {
  branding: { ... },
  defaults: { ... },
  ai: { ... }
};
```

---

## 1. Branding Settings

Customize your site title, tagline, logo text, author name, and repository URL:

```javascript
branding: {
  siteName: "Swiss Travel Planner",
  tagline: "Swiss Travel Planner & Budget Calculator",
  description: "Calculate budget estimates using Swiss Travel Pass fares, cable car prices, real-time exchange rates, and personalized day-by-day itineraries.",
  logoText: "S",
  author: "Swiss Travel Planner Team",
  repoUrl: "https://github.com/swissplanner"
}
```

!!! tip
    The `logoText` property takes the first character to render crisp icon avatars in the header navigation and footer.

---

## 2. Default Pricing & Fallback Data

When no AI provider is configured or when offline, the calculation engine uses these baseline prices (in CHF):

```javascript
defaults: {
  currency: "CHF",
  targetCurrency: "USD",
  chf_to_usd: 1.10,
  
  // Transport Passes (CHF)
  swiss_travel_pass: {
    "3day": 244,
    "4day": 295,
    "6day": 389,
    "8day": 429,
    "15day": 469
  },
  swiss_half_fare_card: 120,
  berner_oberland_pass: {
    "3day": 230,
    "6day": 290
  },
  tell_pass: {
    "2day": 210,
    "5day": 250
  },
  saver_day_pass_avg: 52,

  // Cable Cars & Mountain Excursion Fares (Full adult prices in CHF)
  cable_cars: {
    gornergrat: { adult: 98, child: 49 },
    schilthorn: { adult: 105, child: 53 },
    first_grindelwald: { adult: 66, child: 33 },
    rigi: { adult: 72, child: 36 },
    pilatus: { adult: 72, child: 36 },
    harder_kulm: { adult: 36, child: 18 },
    jungfraujoch: { adult: 247, child: 124 }
  },
  
  with_half_fare_discount: 0.5,
  with_travel_pass_free: ["rigi", "pilatus", "harder_kulm"]
}
```

---

## 3. AI Configuration Presets

Define default providers and backend proxy rules:

```javascript
ai: {
  defaultProvider: "openrouter",
  
  providers: {
    openrouter: {
      name: "OpenRouter",
      endpoint: "https://openrouter.ai/api/v1/chat/completions",
      model: "google/gemini-2.5-flash",
      requiresApiKey: true
    },
    // ... additional presets
  },

  useBackendProxy: false,
  backendProxyUrl: "/api/chat"
}
```
