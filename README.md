# Relay

> Say exactly what you mean. In any language.

Relay is a single-file AI-powered web app that helps you reply to foreign-language messages with the right tone, context, and nuance — without losing your own voice.

Built for people who regularly chat across language barriers: international friends, online communities, or anyone who's ever stared at a message wondering *"how do I even reply to this?"*

---

## What it does

Paste a message from your friend. Relay reads it, detects the language, and generates 3 reply options — each with a translation so you know exactly what you're sending. The first option always preserves your original style. The other two adapt based on the conversation tone.

The tone isn't static either. It evolves as the conversation grows, and you can adjust it manually or let the AI re-analyze your chat history.

---

## Features

- 🌐 **Auto language detection** — replies always match your friend's language
- 🎭 **Tone-aware generation** — 3 reply options per message, including an "Original Style" that keeps your voice intact
- 📝 **Draft intent** — type a rough idea, Relay shapes it into a proper reply
- 🔄 **Auto retry on rate limit** — unlimited retry with backoff, no babysitting required
- 💾 **Session history** — multiple conversations, all stored locally in your browser
- 🔒 **No backend required** — single HTML file, deployable anywhere

---

## Tech

- Vanilla HTML + Tailwind CSS (glassmorphism UI)
- Gemini API (direct) or n8n webhook proxy
- localStorage for persistence
- Web Crypto API for JWT auth (n8n mode)
- Zero dependencies, zero build step

---

## Setup

**1. Get a Gemini API key**
Go to [Google AI Studio](https://aistudio.google.com/apikey) and generate a free key.

**2. Edit the config block in `relay.html`**
```js
const AI_METHOD = 1;              // 1 = Gemini direct, 2 = n8n proxy
const GEMINI_API_KEY = "YOUR_KEY_HERE";
const GEMINI_MODEL   = "gemini-2.0-flash";
```

**3. Open the file in your browser or deploy to GitHub Pages**

That's it.

---

## n8n Proxy Mode (optional)

If you want to keep your API key off the frontend, Relay supports routing through an n8n webhook with JWT auth.

Set up a workflow: `Webhook → Gemini node → Respond to Webhook`, then update the config:

```js
const AI_METHOD      = 2;
const N8N_WEBHOOK_URL = "https://your-n8n-instance/webhook/relay-ai-submit";
const N8N_JWT_SECRET  = "your-jwt-secret";
```

Relay will auto-generate a signed HS256 JWT on each request.

> ⚠️ If your repo is public, the JWT secret will still be visible in source. For personal use this is fine; for production, consider a proper backend.

---

## Deploying to GitHub Pages

1. Rename the file to `index.html`
2. Push to a GitHub repo
3. Enable Pages under `Settings → Pages → Deploy from branch`

Done. Your Relay instance is live.

---

## License

MIT — use it, fork it, build on it.
