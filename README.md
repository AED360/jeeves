# The Jeeves Task Ledger

A persistent, Jeeves-voiced task manager hosted on GitHub Pages, backed by Google Sheets.

---

## Phase 1 — Deploy to GitHub Pages

1. Go to [github.com](https://github.com) and create a new repository named `jeeves`
2. Upload `index.html` to the repository root
3. Go to **Settings → Pages**
4. Under **Source**, select `Deploy from a branch` → `main` → `/ (root)` → Save
5. Your app will be live at: `https://aed360.github.io/jeeves`

At this point Jeeves works but saves tasks to **browser localStorage only** (this device, this browser).

---

## Phase 2 — Connect Google Sheets for persistent cross-device storage

### Step 1 — Set up the Apps Script

1. Open your **Jeeves_Bank** Google Sheet
2. Click **Extensions → Apps Script**
3. Delete all existing code in the editor
4. Open `Code.gs` from this repo and paste the entire contents
5. Click **Save** (floppy disk icon)

### Step 2 — Deploy the Apps Script as a Web App

1. Click **Deploy → New deployment**
2. Click the gear icon next to "Select type" → choose **Web app**
3. Fill in:
   - Description: `Jeeves Backend`
   - Execute as: **Me**
   - Who has access: **Anyone** *(this is required — the URL itself is the security)*
4. Click **Deploy**
5. Click **Authorize access** and follow the Google sign-in prompts
6. Copy the **Web app URL** — it will look like:
   `https://script.google.com/macros/s/XXXXXXXXXXXXXXXX/exec`

### Step 3 — Add the URL to Jeeves

1. Open `index.html` in a text editor
2. Find this line near the top of the `<script>` section:
   ```
   const APPS_SCRIPT_URL = ""; // <-- paste your Apps Script Web App URL here
   ```
3. Paste your URL between the quotes:
   ```
   const APPS_SCRIPT_URL = "https://script.google.com/macros/s/XXXXXXXXXXXXXXXX/exec";
   ```
4. Save the file
5. Upload the updated `index.html` to your GitHub repo (drag and drop to replace)

### Step 4 — Verify

Open `https://aed360.github.io/jeeves` — the status line should read:
> ✓ Google Sheet connected — tasks persist across sessions

Jeeves will now remember everything, on any device, indefinitely.

---

## Feature Backlog

| # | Feature | Status |
|---|---------|--------|
| 1 | Jeeves rephrases tasks in his own voice | Backlog |
| 2 | Jeeves voice — fruity Edwardian TTS | Backlog |
| 3 | Print daily briefing as morning memo | Backlog |
| 4 | Google Tasks integration for reminders | Backlog |
| 5 | Wellbeing intervention (too many Work tasks) | Backlog |
| 6 | Address as Madam / Miss Amy | ✓ Done |
| 7 | Mood-based task reordering | Backlog |
| 8 | Procrastination detection (task age > 3 days) | Backlog |
| 9 | Daily briefing email to Gmail | Backlog |
| 10 | Seasonal / weather-aware salutations | Backlog |
| 11 | Full ledger completion soliloquy | Backlog |
| 12 | Multi-task parsing from pasted text | ✓ Done |
| 13 | Persistent storage via Google Sheets | ✓ Done |

---

## Notes

- The Apps Script URL is effectively a password — keep it out of public commits. For a public repo, consider moving it to a GitHub Actions secret or simply accepting that anyone with the URL could read/write your tasks.
- Tasks also save to localStorage as a backup, so if the Sheet is temporarily unavailable, nothing is lost.
