# Deployment Guide — Kanchana Events Hub (Vercel)

This document walks you through deploying the Kanchana Events Hub to Vercel. It assumes a typical frontend stack (Next.js) and environment variable usage as described in the app's `.env.local` file.

---

## Phase 1 — Prepare your code on GitHub

1. Create a GitHub repository
   - Go to https://github.com and sign in.
   - Click the plus icon (+) → New repository.
   - Repository name: `kanchana-events-hub`.
   - Choose Public or Private (private recommended if it contains secrets).
   - Click Create repository.

2. Push your code to GitHub (PowerShell example)

```powershell
# 1. Initialize git (if not already done in your local project)
git init

# 2. Stage all files
git add .

# 3. Commit your changes
git commit -m "Initial deployment commit"

# 4. Add remote (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/kanchana-events-hub.git

# 5. Push branch to remote
git push -u origin main
```

Tip: If `git push` fails due to authentication, sign in through VS Code or configure GitHub credentials.

---

## Phase 2 — Deploy to Vercel

1. Import your project
   - Visit https://vercel.com and log in with GitHub.
   - Click `Add New` → `Project` → `Import Git Repository`.
   - Select `kanchana-events-hub` and click Import.

2. Configure project
   - Project Name: leave as `kanchana-events-hub`.
   - Framework Preset: Next.js (auto-detected if present).
   - Root Directory: `./` by default.

3. Setup Environment Variables (CRITICAL)
   - Expand the Environment Variables section.
   - Copy values from local `.env.local` (if present) and add them to Vercel.
   - Key names (examples used by this app):
     - `NEXT_PUBLIC_SUPABASE_URL` — e.g. `https://your-project-id.supabase.co`
     - `NEXT_PUBLIC_SUPABASE_ANON_KEY` — your Supabase anon key
     - `GEMINI_API_KEY` — example 3rd-party service key

How to add:
   - Name (left box): environment variable name
   - Value (right box): paste the secret value
   - Click Add for each env var

Notes:
   - **NEXT_PUBLIC_*** environment variables are readable by the browser and should not contain secrets. Keep all sensitive keys private or use server-side only variables where possible.
   - If you have a `.env.production` value set that differs from `.env.local`, use the production values in Vercel.

4. Deploy
   - Click `Deploy`.
   - Vercel builds and deploys the project; build logs are shown in the UI.

---

## Phase 3 — Verify & Share

1. Confirm Live App URL
   - After a successful deploy, click `Visit` from Vercel or open the deployment URL.
   - The URL will look like: `https://kanchana-events-hub.vercel.app` (or a temporary preview URL for branch commits).

2. Test the application
   - Test user flows (e.g. login, dashboard, content display).
   - Check browser devtools for errors and network calls to Supabase/third-party APIs.
   - Test on mobile by opening the link on your device.

---

## Troubleshooting

"Build Failed" errors
- Open the Vercel build logs, identify the failing step, and reproduce failure locally:
  - Run `npm run build` (or `yarn build`) locally to surface TypeScript or build-time errors.
- Common causes:
  - Missing environment variables
  - TypeScript type errors (fix locally then push commit)
  - Incompatible Node.js version (set `engines` in `package.json` or configure in Vercel `Settings > General > Build & Development Settings`)

App loads with no data
- If authentication/authorization is enabled, ensure the keys and RLS policies in Supabase are configured correctly.
- Confirm that public keys have correct values (no extra spaces) in Vercel env vars.

Updates not appearing
- Vercel redeploys automatically on `git push` to branches linked to the project.
- To trigger a redeploy manually: Changes → Commit & Push to GitHub → Vercel automatically queues a new build.

---

## Advanced Options / Tips

- Use `vercel` CLI for local deployments and previews
  ```powershell
  npm i -g vercel
  vercel login
  vercel link # links project with remote Vercel project if not auto-linked
  vercel --prod # to deploy a production build
  ```
- Configure a custom domain in Vercel `Settings > Domains`.
- If your project uses SSR or serverless functions, use server-side environment variables for secrets (not `NEXT_PUBLIC_...`).
- Add `Vercel` deployment status checks or required reviewers as needed.

---

## Minimal Checklist before Deployment
- [ ] Project pushed to GitHub
- [ ] `.env.local` values copied to Vercel env vars
- [ ] Project builds locally (`npm run build`)
- [ ] Linting and tests pass

---

If you want, I can help scaffold a GitHub Actions workflow and a `vercel.json` file for more control (rewrites, headers, and root settings).