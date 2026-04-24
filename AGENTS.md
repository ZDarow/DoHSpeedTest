# AGENTS.md - DoHSpeedTest

## Project Overview
Static web-based DNS-over-HTTPS speed testing tool. Pure frontend (HTML + Vanilla JS + CSS), no build system, no Node/npm dependencies. CDN-only: Tailwind CSS, Chart.js.

## Stack
- **HTML5** — `index.html` (UI structure)
- **Vanilla JavaScript** — `script.js` (all logic, ~1000 lines)
- **Tailwind CSS** — via CDN
- **Chart.js** — via CDN (performance charts)
- **Protocol** — DNS-over-HTTPS (DoH) via Fetch API

## Development
No build step required. Simply edit files and refresh browser (Ctrl+F5).
- Open `index.html` directly in browser
- Or serve: `python3 -m http.server 8000`

## Project Structure
```
DoHSpeedTest/
├── index.html          # Main UI (400 lines)
├── script.js           # Core logic: DNS testing, results, charts (973 lines)
├── favicon/            # Site icons
├── loading.gif         # Loading animation
├── README.md           # Project documentation
├── AGENTS.md           # This file
└── .git/              # Git repository
```

## Key Variables in script.js
- `topWebsites` (line 23) — Hostnames for DNS resolution speed tests. Add regional sites here.
- `dnsServers` (line 31) — List of DoH servers to test. Each entry: `{ name, url, ips, type?, allowCors? }`
- `TIMEOUT_PENALTY_MS` (line 29) — Timeout for each DNS query (5000ms)

## Code Conventions
- Vanilla JS only, no frameworks
- No comments unless explicitly requested
- Keep it simple — this is a single-page tool, not a SPA framework
- When adding DoH servers: include `name`, `url` (DoH endpoint), `ips` (IPv4/IPv6), optionally `type` ("get"/"post") and `allowCors`
- Test hosts in `topWebsites` should be relevant to user's region

## Testing
No automated tests. Manual testing:
1. Open `index.html`
2. Click "Start" to run DNS speed tests
3. Verify chart renders and results display correctly
4. Test adding custom DoH servers
5. Test regional host customization

## Common Tasks
- **Add DoH server**: Edit `dnsServers` array in `script.js:31`
- **Add test hosts**: Edit `topWebsites` array in `script.js:23`
- **Modify UI**: Edit `index.html`
- **Change styling**: Inline in `index.html` (Tailwind classes) or inline `<style>`

## Notes
- All DNS queries run client-side in browser (no backend)
- DoH endpoints must support CORS or use `allowCors: false`
- GitHub Pages / static hosting compatible
- License: GNU GPL v3.0
