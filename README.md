<p align="center">
  <img src="assets/clamav-sentinel-logo.png" width="300" alt="n8n-ClamAV Sentinel Logo" />
</p>

<h1 align="center">n8n-ClamAV Sentinel</h1>
<p align="center"><em>Automated weekly ClamAV scanning and alerts via ntfy — built for n8n power users and sysadmins</em></p>

<p align="center">
  <a href="https://ko-fi.com/s/d61795e2af" target="_blank">
    <img src="https://ko-fi.com/img/githubbutton_sm.svg" alt="Buy Me a Coffee on Ko-fi" />
  </a>
</p>

<p align="center">
  <img alt="License" src="https://img.shields.io/github/license/gusinfosec/n8n-clamav-sentinel" />
  <img alt="Status" src="https://img.shields.io/badge/status-active-success" />
  <img alt="Stars" src="https://img.shields.io/github/stars/gusinfosec/n8n-clamav-sentinel?style=social" />
</p>


A full-featured **n8n workflow** that runs a **weekly ClamAV scan via SSH** and posts alerts/reports to **ntfy**.

> Triggered weekly (Sunday 03:00). Runs `clamscan`, parses results, and notifies through ntfy with rich summaries.

## Workflow Summary

- **Cron Weekly (Sun 03:00)** → **SSH ClamAV Scan** → **If Infected (text check)** →  
  • **ntfy Infected (HTTP POST)** (🚨 priority 5 with FOUND file lines + summary)  
  • **ntfy Clean (HTTP POST)** (✅ summary with counts and times)

## Features

- SSH execution of `clamscan -r /path/to/scan -i`  
- Infection alerts show top 10 lines containing `FOUND` plus scan summary  
- Clean report includes `Scanned`, `Infected`, `Time`, `Start Date`, `End Date` lines  
- Posts to `https://ntfy.sh/<your-topic>` with headers (`X-Title`, `X-Priority`)  
- Works with public or self-hosted ntfy servers

## Repo layout

```
n8n-clamav-sentinel/
├─ workflows/
│  └─ clamav_weekly_scan_full.json
├─ scripts/
│  └─ import.sh
├─ LICENSE
├─ .gitignore
└─ README.md
```

## Setup

1. Import workflow:
   - UI: Workflows → Import from File → select `workflows/clamav_weekly_scan_full.json`
   - CLI: `./scripts/import.sh`
2. In SSH node, configure credentials (`your SSH credentials`).
3. Adjust path `/path/to/scan` or schedule as needed.
4. Ensure ClamAV is installed on the remote host.

## Customization

- **Topic:** replace `https://ntfy.sh/<your-topic>` with your ntfy topic  
- **Threshold / parsing:** workflow checks for `Infected files: 0` absence to flag infection  
- **Priority:** change `X-Priority` values for clean/alert messages

## Security Notes

- Use SSH keys over passwords when possible.  
- Limit scope of user running ClamAV for safer scans.

## GitHub Quickstart

Choose HTTPS **or** SSH.

**HTTPS** (use a Personal Access Token when prompted):
```bashbash
git init
git add .
git commit -m "feat: n8n ClamAV weekly scan full → ntfy alerts"
git branch -M main
git remote add origin https://github.com/<your-username>/n8n-clamav-sentinel.git
git push -u origin main
```

## Screenshot

Here’s how the workflow looks inside n8n:

![ClamAV Workflow](docs/workflow.png)

---

Built from the provided full workflow JSON. See `workflows/clamav_weekly_scan_full.json`.

### SSH alternative
```bash
git init
git add .
git commit -m "feat: n8n ClamAV sentinel → ntfy alerts"
git branch -M main
git remote add origin git@github.com:<your-username>/n8n-clamav-sentinel.git
git push -u origin main
```
