# Hackathon Tracker Telegram Bot

Telegram bot for tracking hackathons, status, links, and reminder schedules.

## Important security note

The token was hard-coded in the original uploaded script. Treat that token as compromised:
open **@BotFather** in Telegram, revoke/regenerate the bot token, and use only the new
token as the `BOT_TOKEN` environment variable. Never commit the token to GitHub.

## Deploy on Render

1. Create a new **private GitHub repository** and upload these files:
   `hackathon_bot.py`, `requirements.txt`, and `render.yaml`.
2. In Render, choose **New + → Blueprint** and connect that repository.
3. Render will detect `render.yaml` and create a Background Worker.
4. In the worker's Environment settings, set `BOT_TOKEN` to the new token from BotFather.
5. Deploy. Check the worker logs for `Bot chal raha hai...`.
6. Open your bot in Telegram and send `/start`.

**Storage:** `render.yaml` configures a 1 GB persistent disk at `/var/data`.
Render persistent disks are a paid feature. If you use a free worker without a disk,
its local filesystem may be erased on restart/redeploy, so hackathon data can be lost.
Keep the disk and `DATA_FILE=/var/data/hackathons.json` for persistence.

**Run only one worker instance** for this Telegram polling bot. Multiple polling instances
using the same token can conflict.

## Run locally

Python 3.10+ recommended.

```bash
python -m venv .venv
# Windows:
.venv\Scripts\activate
# macOS/Linux:
source .venv/bin/activate

pip install -r requirements.txt
```

Set the environment variable before starting:

**Windows PowerShell**
```powershell
$env:BOT_TOKEN="YOUR_NEW_TELEGRAM_BOT_TOKEN"
python hackathon_bot.py
```

**macOS/Linux**
```bash
export BOT_TOKEN="YOUR_NEW_TELEGRAM_BOT_TOKEN"
python hackathon_bot.py
```

## Bot commands

- `/start` or `/help` — start the bot
- `/menu` — show the main menu

Add hackathons and manage status/reminders through the inline buttons.
