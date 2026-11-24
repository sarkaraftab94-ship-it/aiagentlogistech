# Logistech Daily B2B Posting Agent

Every day at **7:00 PM Saudi time** it: picks a rotating target industry → writes the strategy, Saudi Arabic caption,
hashtags and CTA (Gemini, free) → renders a branded 1080×1350 design → posts to your connected platforms.
Everything runs free on GitHub Actions. Past posts are stored in `data/history.json` so industries/hooks never repeat.

## Setup (≈20 min)
1. Create a **public** GitHub repo and upload this folder. (Public is required so Instagram/Pinterest can download the image URL. The repo contains only your marketing posts, no secrets.)
2. Fill `brand_profile.json` (approved facts/services/cities) and drop your logo in `assets/logo.png`. The agent will not claim anything not listed there.
3. Get a free Gemini key: https://aistudio.google.com/apikey → repo **Settings → Secrets and variables → Actions → New secret** `GEMINI_API_KEY`.
4. Add the secrets for each platform you want (names in `.env.example`). Any platform without secrets is skipped automatically.
5. **Actions → Logistech daily post → Run workflow** with `dry_run = 1` to test. Then run with `0`. After that it runs daily by itself.

## Platform reality (honest status)
| Platform | Cost | Notes |
|---|---|---|
| Telegram | Free | Easiest to start. Also delivers the ready package for manual platforms. |
| LinkedIn | Free | Personal profile: self-serve ("Share on LinkedIn" product). Company page needs Community Management API approval. Token lasts ~60 days, then refresh. |
| Instagram + Facebook | Free | Needs Instagram Business/Creator account linked to a Facebook Page + Meta developer app. Long-lived token needed. |
| X | **Not free**, but cheap | X has no free API tier now; it's pay-per-use. Plain post ≈ US$0.015 → about **US$0.50/month** for daily posting. Posts containing a link cost ~US$0.20 each, so the agent posts without links. |
| Pinterest | Free | Needs API access approval (trial) and a board ID. |
| TikTok | Free but blocked | Posting API requires app audit; unaudited apps can't publish publicly. Use the Telegram package. |
| Snapchat | No option | No public API for organic posting. Use the Telegram package. |

## Notes
- GitHub cron can start 5–30 min late under load.
- Keep an eye on the first week of posts; approve/edit via Telegram if you want a human check (set `DRY_RUN=1` and post manually).
- Not tested against live accounts. API versions change, so check logs in the Actions tab on first run.
