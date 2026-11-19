# Deploy on Railway (step by step)

1. Push this folder to a **private** GitHub repo (Railway deploys from GitHub).
2. Railway -> New Project -> Deploy from GitHub repo -> pick it.
3. Service -> **Variables** -> add:

| Variable | What to put |
|---|---|
| `GITHUB_TOKEN` | Your GitHub personal access token (repo scope) |
| `GITHUB_REPO` | `your-username/your-private-repo` (must contain `users.json`) |
| `ADMIN_KEY` | Your admin panel key |
| `SECRET_KEY` | A long random string |
| `OPENROUTER_API_KEY` | Optional (AI assistant only) |
| `START_BACKGROUND` | `1` (keep) |

Railway sets `PORT` automatically. Do not add it.

4. Service -> Settings -> Networking -> **Generate Domain**. Open it.
5. Health check: `https://<your-domain>/health` should show `{"status":"ok"}`.

Notes:
- Railway's disk is temporary. Files are backed up to GitHub and restored at startup, so keep `GITHUB_TOKEN` and `GITHUB_REPO` set.
- Keep exactly one instance (`-w 1` in the start command), because bot process state lives in memory.
- `users.json` format: `{"username": {"p": "password", "status": "active", "memory": "512MB", "disk": 1024}}`
