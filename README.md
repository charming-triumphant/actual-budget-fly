# Actual Budget on Fly.io

Deployed from `actualbudget/actual-server:latest` to Fly.io (Sydney region) with persistent volume.

## Files
- `Dockerfile` - Uses official Actual Budget image
- `fly.toml` - Fly.io configuration (app: `charming-triumphant-actual`, region: `syd`)
- `.gitignore` - Standard ignores

## One-time Setup (run after pushing to GitHub)

```powershell
# Create persistent volume (1GB in Sydney)
flyctl volumes create actual_data --region syd --size 1
```

## Deploy Options

### Option 1: GitHub → Fly.io (Recommended)
1. Create repo at https://github.com/charming-triumphant/actual-budget-fly
2. Push this folder:
   ```powershell
   git init
   git add .
   git commit -m "Initial Fly.io deployment config"
   git branch -M main
   git remote add origin https://github.com/charming-triumphant/actual-budget-fly.git
   git push -u origin main
   ```
3. In Fly.io dashboard: **New App** → **Import from GitHub** → Select repo → Deploy

### Option 2: Direct CLI Deploy
```powershell
flyctl launch --no-deploy  # Uses fly.toml
flyctl deploy
```

## App Details
- **App name**: `charming-triumphant-actual`
- **Region**: Sydney (`syd`)
- **Port**: 5006 (internal) → HTTPS (external)
- **Volume**: `actual_data` (1GB) mounted at `/data`
- **Auto-stop**: Yes (scales to 0 when idle)
- **Auto-start**: Yes (wakes on request)

## Access
After deploy: `https://charming-triumphant-actual.fly.dev`