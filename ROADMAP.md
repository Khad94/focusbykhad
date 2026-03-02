# Focus by Khad — AI Automation Roadmap
### A step-by-step guide to building your personal AI photography studio

---

## PHASE 1 — iMac Setup & Autonomous Agents
*Goal: Turn your unused iMac into a 24/7 silent AI assistant*

---

### STEP 1 — Prepare the iMac
**Time estimate: 1–2 hours**

- [ ] Update macOS to latest version
- [ ] Enable "Wake for network access" in Energy settings (keeps it always on)
- [ ] Install Homebrew (package manager)
- [ ] Install Python 3.11+
- [ ] Install GitHub CLI (`gh`)
- [ ] Authenticate GitHub CLI with your Khad94 account
- [ ] Clone your portfolio repo: `gh repo clone Khad94/focusbykhad`

---

### STEP 2 — Get Claude API Access
**Time estimate: 30 minutes**
**Cost: ~$5–10/month for light use**

- [ ] Create an Anthropic account at console.anthropic.com
- [ ] Add a payment method (pay-as-you-go, no subscription)
- [ ] Generate an API key
- [ ] Store the key securely on the iMac

> 💡 Think of the API key as the "brain" that powers all agents below.
> You pay only for what you use — a daily digest costs fractions of a cent.

---

### STEP 3 — Agent 1: Website Manager
**Time estimate: 2–3 hours to build**

**What it does:**
- Watches a folder on the iMac for new photos
- When photos are added, automatically updates `index.html`
- Pushes changes to GitHub → site goes live on focusbykhad.com
- No action needed from you

**How it works:**
```
You drop photos in /Portfolio/new-photos/
        ↓
Agent detects new files (runs every 10 min)
        ↓
Claude API decides placement (Sports/Street/Portrait)
        ↓
index.html updated + pushed to GitHub
        ↓
focusbykhad.com updates automatically
```

**Tools needed:** Python, GitHub CLI, Claude API, folder watcher script

---

### STEP 4 — Agent 2: Daily Photography Digest
**Time estimate: 1–2 hours to build**
**Runs: Every morning at a time you choose**

**What it does:**
- Searches the web for photography news, gear reviews, software updates
- Checks for Lightroom and Photoshop updates
- Monitors trending photography styles and techniques
- Sends you a clean, formatted email digest every morning

**Sample digest format:**
```
☀️  Good morning Khad — Here's your daily Focus digest

📷 GEAR
  · Sony announces new 85mm f/1.4 GM II — $2,199
  · Sigma 24-70mm f/2.8 reviewed: score 94/100

🖥️  SOFTWARE
  · Lightroom 13.2 released — new AI masking features
  · Photoshop update: Generative Fill improvements

📈 TRENDS
  · High-contrast street photography trending on 500px
  · Sports burst mode techniques — popular this week

🌐 YOUR SITE
  · 12 visitors yesterday on focusbykhad.com
  · Contact form: 0 new messages
```

**Tools needed:** Python, NewsAPI (free tier), SendGrid (free tier for email), cron job

---

### STEP 5 — Schedule & Test Everything
**Time estimate: 1 hour**

- [ ] Set up cron jobs to run agents on schedule
- [ ] Test Agent 1 by dropping a photo in the watch folder
- [ ] Test Agent 2 by triggering the digest manually
- [ ] Verify emails are received at khad94@orange.fr
- [ ] Verify portfolio auto-updates on focusbykhad.com

---
---

## PHASE 2 — Photography Workflow Automation
*Goal: Go from 200 raw photos to 30–50 retouched, watermarked, exported finals — with minimal effort*

---

### STEP 6 — Agent 3: Smart Photo Culling
**Time estimate: 3–4 hours to build**
**What it saves you: 1–2 hours per shoot**

**What it does:**
- Scans all photos from a shoot
- Uses AI vision to detect and remove: blurry shots, closed eyes, duplicate poses, bad exposure
- Scores remaining photos by sharpness, composition, and expression
- Outputs a shortlist of the top 40–60 candidates for your final review

**The workflow:**
```
You dump 200 photos in /Shoots/football-march-01/raw/
        ↓
Agent scans all photos (takes ~5 min)
        ↓
Rejects: blurry, duplicates, eyes closed (~80 removed)
        ↓
Scores remaining 120 by quality
        ↓
Top 50 candidates copied to /Shoots/football-march-01/review/
        ↓
You review 50 instead of 200 ✅
```

> 🎯 For portraits: Agent applies stricter scoring on facial expression,
> eye sharpness, and skin texture — the candidates it gives you will
> already be the strongest frames.

**Tools needed:** Python, Claude Vision API (or open-source model), ExifTool

---

### STEP 7 — Agent 4: Lightroom Style Application
**Time estimate: Setup 2–3 hours | ongoing = automatic**
**What it saves you: 30–60 min per shoot**

**Two options (you choose):**

| Option | Tool | Cost | Notes |
|--------|------|------|-------|
| A — AI learns your style | Imagen AI | ~$10/mo | Trains on your past edits, applies your exact look |
| B — Apply your preset | Lightroom script | Free | Applies a fixed preset you already love |

**Recommended: Option A** — Imagen AI integrates directly with Lightroom and gets smarter the more you use it. After 3–4 shoots it will edit very close to how you would.

**Workflow:**
```
Your 50 review photos
        ↓
Imagen AI / script applies your style
        ↓
Photos are edited and ready in Lightroom
        ↓
You make final tweaks to your 30–50 picks
        ↓
Export from Lightroom
```

---

### STEP 8 — Agent 5: Photoshop Finisher
**Time estimate: 2–3 hours to build**
**What it saves you: 30–60 min per shoot**

**What it does:**
- Takes your exported photos from Lightroom
- Adds your frame automatically
- Places your logo in the correct position
- Adds your signature
- Applies final sharpening/export settings
- Saves to your delivery folder, named correctly

**Your frame template (set up once):**
```
┌─────────────────────────────┐
│                             │
│      [your photo here]      │
│                             │
│  [logo]      [signature]    │
└─────────────────────────────┘
```

**Workflow:**
```
30–50 edited photos exported from Lightroom
        ↓
Agent applies frame template to all photos
        ↓
Logo + signature placed automatically
        ↓
Final export to /Shoots/football-march-01/final/
        ↓
Ready to share / post / deliver ✅
```

**Tools needed:** Python, ImageMagick (free) or Photoshop scripting (JS/Python)

---
---

## FULL PIPELINE SUMMARY
*From shoot to delivery*

```
📸  You come home with 200 photos
            ↓
🤖  Agent 3 culls → 50 candidates (5 min, automatic)
            ↓
🖥️   Agent 4 edits in Lightroom style (10 min, automatic)
            ↓
👁️   YOU review 50 edited photos, pick your 30 favourites
            ↓
🖼️   Agent 5 adds frame, logo, signature (5 min, automatic)
            ↓
📁  Finals land in your delivery folder
            ↓
🌐  Agent 1 updates focusbykhad.com with best shots
```

**Your actual time spent: reviewing 50 photos + final creative decisions**
**Everything else: handled.**

---

## TIMELINE & PRIORITY

| Phase | What | When | Effort |
|-------|------|------|--------|
| Now | Finish portfolio with real photos | Next session | Low |
| Phase 1 | iMac + daily digest + website agent | Session 2–3 | Medium |
| Phase 2A | Photo culling agent | Session 4 | Medium |
| Phase 2B | Lightroom + finisher agents | Session 5–6 | Medium |
| Ongoing | Tune, improve, add features | As needed | Low |

---

## COSTS OVERVIEW

| Tool | Cost | Notes |
|------|------|-------|
| Claude API | ~$5–10/mo | Powers all agents |
| NewsAPI | Free | For daily digest |
| SendGrid | Free | For digest emails |
| Imagen AI | ~$10/mo | Optional, for Lightroom |
| ImageMagick | Free | For frame/watermark |
| GitHub | Free | Already set up ✅ |
| Netlify | Free | Already set up ✅ |

**Total: $5–20/month** depending on options chosen

---

*Built with Claude — Focus by Khad AI Roadmap v1.0 — March 2026*
