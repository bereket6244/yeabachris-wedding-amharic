# Deploying the Amharic invitation to menaincet.com/yeabsrachristian-amharic

This repo auto-deploys to `https://menaincet.com/yeabsrachristian-amharic` whenever you push to `main`.

## One-time setup

### 1. Keep credentials in GitHub Actions secrets
Do not commit cPanel or GitHub tokens to the repo. Store deployment credentials only as repository secrets.

### 2. Create the GitHub repo and push
From this folder:
```bash
git init
git add .
git commit -m "Engagement invitation site"
git branch -M main
git remote add origin https://github.com/<you>/yeabachris-wedding-amharic.git
git push -u origin main
```
(Create the empty repo on github.com first, or use `gh repo create`.)

### 3. Add the deploy secrets in GitHub
Repo → Settings → Secrets and variables → Actions → New repository secret:

| Secret name    | Value                                    |
|----------------|------------------------------------------|
| `CPANEL_HOST`  | `menaincet.com`                         |
| `CPANEL_USER`  | cPanel username                          |
| `CPANEL_TOKEN` | cPanel API token                         |
| `CPANEL_TARGET_DIR` | `/home/menainpy/public_html/yeabsrachristian-amharic` |

Credentials live only in GitHub's encrypted secrets — never in the repo.
The old `FTP_*` and `SSH_*` secrets can be deleted if this repo no longer uses them.

### 4. Push again (or run the workflow manually)
Any push to `main` now uploads the public site files into `/home/menainpy/public_html/yeabsrachristian-amharic/`.
First run also creates missing directories.

## Notes
- The site uses relative paths, so it works fine under the `/yeabsrachristian-amharic` subpath.
- `.github/workflows/deploy.yml` controls the deploy.
- `scripts/deploy-cpanel.mjs` uploads only `index.html`, `support.js`, `flower-petal.png`, and `assets/**`.
