# Vibe Shooting

Vibe Shooting is a browser-based AR gesture shooting game. Your webcam stays local in the browser while MediaPipe Hands tracks your hand, Three.js renders futuristic target discs, and your index finger becomes the aim controller.

Public repository: https://github.com/anmolkaw/vibe-shooting

Production deployment: https://vibe-shooting.vercel.app

Custom domain status: `vibeshooting.com` and `www.vibeshooting.com` are attached to the Vercel project, but DNS must be updated at the current DNS provider before they resolve to the game.

## Features

- Webcam-based AR play with a mirrored camera background
- Index-finger aiming and thumb-to-index trigger firing
- Three.js enemies, crosshair, laser, particles, hit bursts, and lock-on effects
- Magnetic aim assist that gently pulls toward nearby discs
- Generated Web Audio shot, hit, miss, and combo sounds
- Score, accuracy, combo, best combo, shots, and local best score
- Pause and restart controls
- Static single-file game source with no backend, no build step, and no API keys

## Controls

- Point with your index finger to aim.
- Bring your thumb close to your index finger to fire.
- Use good lighting and keep your hand in frame for the most reliable tracking.

## Browser Requirements

- Best on desktop Chrome or another modern Chromium browser
- Webcam permission
- WebGL support
- HTTPS for production camera access

## Privacy

Camera processing happens locally in your browser. No video is recorded, uploaded, stored, or sent to a backend. The game has no backend, database, user accounts, API keys, or analytics.

## Local Testing

From this directory:

```bash
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000
```

## GitHub Repository Setup

If GitHub CLI is authenticated, the repository can be created with:

```bash
git init
git add .
git commit -m "feat: launch Vibe Shooting"
git branch -M main
gh repo create vibe-shooting --public --source=. --remote=origin --push
```

If `gh auth status` is not authenticated, run:

```bash
gh auth login
```

Then rerun the repository creation commands above.

## Vercel Deployment

This project is a static website. Use the Vercel Hobby plan with:

- Framework preset: Other
- Build command: none
- Output directory: project root
- Environment variables: none
- Serverless functions: none

If Vercel CLI is installed and authenticated:

```bash
vercel --version
vercel whoami
vercel
vercel --prod
```

Use the project name:

```text
vibe-shooting
```

The verified free production URL is:

```text
https://vibe-shooting.vercel.app
```

## Custom Domain: vibeshooting.com

The game can be hosted for free, but a `.com` domain must be registered separately through a domain registrar.

Current custom-domain setup:

1. `vibeshooting.com` is added to the Vercel project.
2. `www.vibeshooting.com` is added to the Vercel project.
3. `https://vibeshooting.com` is the intended canonical domain.
4. `www.vibeshooting.com` redirects to the canonical domain through `vercel.json` once DNS points to Vercel.

Vercel currently reports these DNS actions as required:

```text
A vibeshooting.com 76.76.21.21
A www.vibeshooting.com 76.76.21.21
```

The domain currently uses Cloudflare nameservers, so update these records in Cloudflare or change the domain nameservers to Vercel's intended nameservers:

```text
ns1.vercel-dns.com
ns2.vercel-dns.com
```

Vercel will verify the domain automatically after DNS propagation.

## MediaPipe Version Lock

MediaPipe Hands is intentionally pinned to version `0.4.1646424915` from unpkg to avoid WASM/resource version mismatches. All MediaPipe package URLs in `index.html` use the same pinned version, and `locateFile` loads Hands assets from:

```text
https://unpkg.com/@mediapipe/hands@0.4.1646424915/
```

## Production Checklist

- HTTPS active
- Camera permission works after clicking `ENABLE CAMERA & START`
- First MediaPipe result required before gameplay
- Four discs always active during gameplay
- Gesture shooting fires once per trigger pull
- Aim assist, laser, hit effects, miss effects, HUD, pause, restart, and local best score work
- No API keys
- No package installation or build step required
- Static hosting only
