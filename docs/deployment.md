# Deployment & Hosting Guide

**Swiss Travel Planner** can be deployed to static web hosts, serverless platforms, Docker containers, or self-hosted Linux VPS servers.

---

## 1. Vercel Deployment (Recommended)

Vercel provides automatic serverless API routing via `/api/chat.js`.

1. Fork the repository: [https://github.com/swissplanner](https://github.com/swissplanner).
2. Log into [Vercel](https://vercel.com) and click **Add New Project**.
3. Import your forked `swiss-travel-planner` repo.
4. Add environment variables in Vercel settings (optional):
   - `AI_API_KEY`: Your AI Provider API Key
   - `AI_PROVIDER`: `openrouter` (or `openai`, `groq`, `minimax`)
   - `AI_MODEL`: `google/gemini-2.5-flash`
5. Click **Deploy**.

---

## 2. Netlify / Cloudflare Pages / GitHub Pages

### GitHub Pages (Static Mode)
1. In your GitHub repository settings, navigate to **Pages**.
2. Set Source to `Deploy from a branch` -> Branch `main` -> `/ (root)`.
3. Save. Your application will be live at `https://<username>.github.io/swiss-travel-planner/`.

### Cloudflare Pages / Netlify
1. Connect your GitHub repository to Cloudflare Pages or Netlify.
2. Build command: *(Leave empty)*
3. Build output directory: `./` or `.`

---

## 3. Docker Deployment (Self-Hosted VPS)

Deploy on any Docker host (DigitalOcean, AWS EC2, Hetzner, Linode):

1. Build the Docker image:
   ```bash
   docker build -t swiss-travel-planner .
   ```

2. Run the container on port 80:
   ```bash
   docker run -d -p 80:80 --name swiss-planner --restart unless-stopped swiss-travel-planner
   ```

---

## 4. Node.js Express Server on Linux (Ubuntu + Nginx)

1. Clone repo on your server:
   ```bash
   git clone https://github.com/swissplanner.git /var/www/swiss-planner
   cd /var/www/swiss-planner
   npm install
   ```

2. Setup `.env` configuration:
   ```bash
   cp .env.example .env
   ```

3. Manage process with PM2:
   ```bash
   npm install -g pm2
   pm2 start server.js --name "swiss-planner"
   pm2 save
   ```

4. Configure Nginx Reverse Proxy (`/etc/nginx/sites-available/default`):
   ```nginx
   server {
       listen 80;
       server_name yourdomain.com;

       location / {
           proxy_pass http://localhost:3000;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
       }
   }
   ```
