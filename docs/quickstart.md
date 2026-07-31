# Quick Start Guide

This guide will walk you through setting up and running **Swiss Travel Planner** locally or on your own server.

---

## Prerequisites

Before starting, make sure you have:

- A modern web browser (Chrome, Firefox, Safari, Edge).
- (Optional) [Node.js](https://nodejs.org/) v18+ if you want to run the Express backend proxy server.
- (Optional) An API Key from an AI provider (e.g., OpenRouter, OpenAI, Groq, MiniMax).

---

## 1. Clone the Repository

Fork and clone the repository from GitHub:

```bash
git clone https://github.com/swissplanner.git
cd swiss-travel-planner
```

---

## 2. Choose Your Execution Mode

### Option A: Static Client-Side Mode (No Installation Required)

Because **Swiss Travel Planner** is built as a zero-dependency static application, you can run it immediately without compiling code:

1. Open `index.html` directly in your browser or serve it using VS Code **Live Server**.
2. Click the **AI Settings** button (⚙️) in the top-right navigation bar.
3. Select your preferred AI Provider, enter your API Key, and click **Save Settings**.

---

### Option B: Node.js Backend Proxy Server

If you want to proxy requests through a Node.js server to hide your API keys from client-side network tabs:

1. Install project dependencies:
   ```bash
   npm install
   ```

2. Copy the environment variables template:
   ```bash
   cp .env.example .env
   ```

3. Configure your `.env` file:
   ```env
   PORT=3000
   AI_PROVIDER=openrouter
   AI_API_KEY=sk-or-v1-your-actual-api-key
   AI_MODEL=google/gemini-2.5-flash
   AI_ENDPOINT=https://openrouter.ai/api/v1/chat/completions
   ```

4. Enable backend proxying in `config.js`:
   ```javascript
   ai: {
     useBackendProxy: true,
     backendProxyUrl: "/api/chat"
   }
   ```

5. Launch the Node.js server:
   ```bash
   npm start
   ```

6. Access the live application at `http://localhost:3000`.

---

## Next Steps

- Learn how to customize site branding and default prices in **[Configuration](configuration.md)**.
- Configure different AI model providers in **[AI Providers Integration](ai-providers.md)**.
