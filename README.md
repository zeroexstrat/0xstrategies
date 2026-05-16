# 0xStrategies — Public Companion

Portfolio site for Rafael Almeida, Operations Supervisor & AI-Assisted Automation Developer at UPS CHEMA Hub.

## Structure

| File | Description |
|------|-------------|
| `index.html` | Public companion — main portfolio page |
| `si_whitepaper_v2.2.html` | Sort Intelligence whitepaper |
| `ltc_whitepaper_v1.0.html` | LTC Mathematical Abstractions whitepaper |
| `tracker_architecture_v2.11.html` | Tracker v2.11 Architecture docs |
| `presentation_v1.1.html` | Hub Operations Suite presentation |
| `UPS Sort Training Platform.pdf` | Sort Training Platform (PDF) |

## Deployment

Deployed via **Cloudflare Pages** — auto-deploys on push to `main`.

## Local preview

```bash
# Python
python3 -m http.server 8080

# Then open http://localhost:8080
```

## Updating

1. Rebuild the assets by running `build_dashboard.py` in `ai_memory/`
2. Copy updated files into this folder
3. `git add . && git commit -m "update: <description>"`
4. `git push origin main`

Cloudflare Pages auto-deploys within ~30 seconds of push.
