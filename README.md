# Forge — BMH Research Signal Compiler (PWA shell)

The installable phone/desktop client for **Forge**, Bryan's read-only research analyst.
This repo is a **dumb shell** — zero data, zero doctrine. It talks to the Forge backend
on the Mac Pro over Tailscale and renders the signal feed.

Mission: PhD-level read-only internet research that compiles **signals** (title ·
summary · why-it-matters · confidence · score · cited sources) for review across
crypto, AI, business opportunities, and freight.

## Architecture (same split as `now-brief` / `companion`)
- **Shell (this repo)** → `https://bmhsolutions3711.github.io/forge/` (GitHub Pages).
  Public origin so it installs as a PWA on the phone. Holds no secrets.
- **Backend** → `~/Local Models/bik/forge/` on the Mac Pro (`server.py`, port 8490),
  reached via Tailscale Serve. Serves `/api/*` only and 302-redirects `/` here.

## The moat boundary
- **Search + scrape** = always local/free (ddgs + BeautifulSoup, GET-only).
- **Synthesis brain** = Claude (default, reliable) or Gemma (local toggle). The cloud
  brain is a **stateless tenant** — it sees only one run's sources + lens, never the
  signal corpus, stars, or doctrine.
- **Everything that compounds** — signals, lenses, curation, Atlas learnings — lives in
  SQLite on the Pro, never synced here. Starred signals feed Atlas's memory.

## First connect
1. Open the shell, enter the backend's Tailscale URL (`https://<host>.ts.net:8490`).
2. Token = `FORGE_TOKEN` (or `COMPANION_TOKEN`) from `~/.config/bmh/.env`.
   On localhost the token is optional (loopback bypasses auth).

## Files
- `index.html` — the whole app (setup, feed, research, topics, briefs)
- `manifest.json` / `sw.js` — PWA install + network-first service worker
- `static/` — Forge anvil icons (32/180/192/512)
