# Clear Advantage Window Cleaning — Website

Live site for [clearadvantagedl.com](https://clearadvantagedl.com)

## Quick Start (Local Dev)

```bash
npm install
npm run dev
```

Opens at `http://localhost:5173`

## Deploy to Netlify (Free)

### First Time Setup

1. **Push to GitHub**
   ```bash
   cd clearadvantage-site
   git init
   git add .
   git commit -m "initial site"
   ```
   Then create a repo on GitHub (e.g. `clearadvantage-site`) and:
   ```bash
   git remote add origin https://github.com/YOUR_USERNAME/clearadvantage-site.git
   git branch -M main
   git push -u origin main
   ```

2. **Connect Netlify**
   - Go to [netlify.com](https://netlify.com) → sign up with GitHub
   - Click **"Add new site"** → **"Import from Git"**
   - Pick your `clearadvantage-site` repo
   - Build settings should auto-fill (if not: Build command = `npm run build`, Publish directory = `dist`)
   - Click **Deploy**

3. **Add your Anthropic API key** (for the chat feature)
   - In Netlify: **Site configuration** → **Environment variables**
   - Add variable: `ANTHROPIC_API_KEY` = your key (starts with `sk-ant-...`)
   - Redeploy the site for this to take effect

4. **Point your domain**
   - In Netlify: **Domain management** → **Add custom domain** → type `clearadvantagedl.com`
   - At your domain registrar: update DNS to point to Netlify (they'll give you instructions)
   - Netlify auto-provisions free HTTPS

### Future Updates

Edit code → commit → push:
```bash
git add .
git commit -m "describe your change"
git push
```
Site auto-deploys in ~30 seconds.

## Project Structure

```
clearadvantage-site/
├── index.html              ← Entry HTML
├── src/
│   ├── main.jsx            ← React mount point
│   └── App.jsx             ← Entire site (landing page, estimator, gallery, chat)
├── netlify/
│   └── functions/
│       └── chat.js         ← Serverless proxy for Anthropic API (keeps key safe)
├── netlify.toml            ← Netlify build config
├── vite.config.js          ← Vite bundler config
└── package.json
```

## Chat Feature

The AI chat widget calls `/api/chat` which routes to a Netlify serverless function (`netlify/functions/chat.js`). This proxies requests to Anthropic's API so your API key stays server-side and is never exposed to browsers.

**Without the API key configured**, the chat will gracefully fall back to showing Tina's phone number.

## EmailJS (Lead Capture)

The estimator tool and chat both send lead emails via EmailJS. The service/template IDs are already configured in the code. No extra setup needed — leads go to your inbox.
