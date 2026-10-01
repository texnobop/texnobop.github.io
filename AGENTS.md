# Base44 Dev Environment

## Project Overview
Static HTML website (Uzbek tech/gadget comparison site). No build step, no framework, no backend, no external services, no secrets required.

## Setup
- Served by `nginx:alpine` via `docker-compose.base44.yml`
- Repo root is bind-mounted read-only at `/usr/share/nginx/html`
- Web entry point: host port 3000 → container port 80

## Quirks
- The repo root directory permissions are `700` by default; nginx's worker user can't traverse it. Run `chmod 755 .` if you get 403 errors after a fresh clone or container restart.
- nginx blocks directory listing (403 on `/images/logos/`), but individual files serve fine.

## Verification
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/` → 200
- Check sub-pages: `Iphone.html`, `samsung.html`, `macbook.html`, etc.
- Check images: `http://localhost:3000/images/logos/uzum-logo.png` → 200
