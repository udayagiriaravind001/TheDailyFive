# The Daily Five - Deployment Guide

Everything you need to get the site live in about 30 minutes.

---

## What's in this folder

- `index.html` — the main landing page
- `thank-you.html` — the gated welcome page (shown after form submission, reveals the WhatsApp invite)
- `README.md` — this file

Both HTML files are fully self-contained: inline CSS, inline JS, fonts loaded from Google. No build step. No dependencies.

---

## Step 1 — Set up the signup form (10 minutes)

You have two options. Pick one. The HTML supports both — there's a primary Tally iframe and a fallback Formspree HTML form. Once you choose, delete the other.

### Option A: Tally (recommended for ease)

1. Sign up at [tally.so](https://tally.so) — free
2. Create a new form with three fields:
   - **Email** (required, email type)
   - **Which role are you looking for?** (required, dropdown with options: `Data Analyst`, `QA Engineer`, `Other — I'll tell you below`)
   - **WhatsApp number** (optional, short answer)
3. Go to the form's **Settings → After submission** and set the redirect URL to: `https://thedailyfive.co.uk/thank-you.html`
4. Get your form ID — it's in the embed code, looks something like `3jY7vQ`
5. In `index.html`, find both instances of `REPLACE_TALLY_FORM_ID` and replace with your real form ID
6. Delete the fallback `<form class="signup-form">...</form>` blocks (there are two — one in the hero, one at the bottom)

### Option B: Formspree (more styling control)

1. Sign up at [formspree.io](https://formspree.io) — free for 50 submissions/month
2. Create a new form, get the endpoint URL (looks like `https://formspree.io/f/abcdefgh`)
3. In Formspree settings, set **Thank you redirect** to: `https://thedailyfive.co.uk/thank-you.html`
4. In `index.html`, replace both instances of `REPLACE_FORMSPREE_ID` with your endpoint ID (the part after `/f/`)
5. Delete the Tally `<iframe>` blocks (there are two)

---

## Step 2 — Push to GitHub Pages (10 minutes)

1. Create a new GitHub account if you don't have one
2. Create a new **public** repository — name it `thedailyfive` (or anything; the name doesn't matter once you connect the custom domain)
3. Upload `index.html` and `thank-you.html` to the root of the repo. Easiest way: drag-and-drop on the GitHub website, or use `git`:
   ```
   git init
   git add index.html thank-you.html
   git commit -m "Initial landing page"
   git remote add origin https://github.com/YOUR_USERNAME/thedailyfive.git
   git push -u origin main
   ```
4. Go to **Settings → Pages**
5. Under **Source**, select **Deploy from a branch**, branch `main`, folder `/ (root)`
6. Click **Save**. GitHub will give you a URL like `https://YOUR_USERNAME.github.io/thedailyfive/`
7. Wait 1–2 minutes, then visit that URL to confirm the page loads

---

## Step 3 — Connect your custom domain (10 minutes + DNS wait)

1. In GitHub: **Settings → Pages → Custom domain** → enter `thedailyfive.co.uk` → Save
2. GitHub will show you the IP addresses to use. They are currently:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`
3. In Namecheap: **Domain List → thedailyfive.co.uk → Manage → Advanced DNS**
4. Add these records:
   - **A record** | Host: `@` | Value: `185.199.108.153` | TTL: Automatic
   - **A record** | Host: `@` | Value: `185.199.109.153` | TTL: Automatic
   - **A record** | Host: `@` | Value: `185.199.110.153` | TTL: Automatic
   - **A record** | Host: `@` | Value: `185.199.111.153` | TTL: Automatic
   - **CNAME record** | Host: `www` | Value: `YOUR_USERNAME.github.io` | TTL: Automatic
5. Wait 10–60 minutes for DNS to propagate. You can check progress at [whatsmydns.net](https://whatsmydns.net)
6. Back in GitHub Pages settings, tick **Enforce HTTPS** once it becomes available (usually within an hour after DNS resolves)

Once it's live, visit `https://thedailyfive.co.uk` to confirm.

---

## Step 4 — Test the full flow (5 minutes)

Before sharing the URL anywhere:

1. Visit `https://thedailyfive.co.uk` on desktop AND mobile
2. Submit the form with a real email
3. Confirm the redirect to `/thank-you.html` works
4. Click the WhatsApp button and confirm it opens the community
5. Check `hello@thedailyfive.co.uk` and confirm you received the form submission email (Tally and Formspree both notify you)

If any of those break, fix before sharing.

---

## Step 5 — Distribute (the actual hard part)

The page is the easy 20%. Getting 50 signups is the 80%. Places to post:

- **Reddit:** `r/UKJobs`, `r/cscareerquestionsEU`, `r/QualityAssurance`, `r/dataanalysis` (read each subreddit's self-promotion rules first — some require flair or weekly threads)
- **LinkedIn:** Post from your personal profile. Your story (QA professional in Newcastle, tired of ghost jobs, built this) IS the marketing. Don't make it a corporate launch announcement — make it a personal "here's why I built this" post
- **Communities:** Ministry of Testing (Slack), DataTalks Club (Slack), Locally Optimistic, any UK-focused job-hunt Discords
- **Twitter/X:** Tag with #UKJobs, #DataAnalyst, #QAJobs

Goal: 50 signups in 2–3 weeks. If you can't hit that, the message needs refining before you build anything else.

---

## Step 6 — Have the conversations

Once you have ~10 signups, email each one personally and ask for a 15-minute call. Six questions, same every time:

1. What role are you currently job hunting for?
2. How long have you been looking?
3. What's the worst part of the search right now?
4. Where do you currently find job listings?
5. Have you ever applied to something that turned out to be fake / ghost?
6. If something like The Daily Five existed today and worked well, would you pay for it? How much?

Take notes. After 10 calls you'll see patterns that completely reshape what to build.

---

## Things to update before launch

- Set the launch date in your head and stick to it (current copy says "Launching soon")
- Set a calendar reminder for ~3 weeks from today to decide whether to keep or cancel the Namecheap Private Email free trial before it auto-renews
- If you change the WhatsApp invite link, update it in `thank-you.html` (search for `chat.whatsapp.com`)
- If you switch from "first 100 free" pricing, update both the hero eyebrow and the pricing section in `index.html`

---

## Cost summary so far

- Domain: £5.18/year
- GitHub Pages: free
- Tally or Formspree: free
- Namecheap Private Email: free for 1 month, then ~£10/year if you keep it (or switch to free email forwarding before it renews)

**Total to launch: £5.18**

That's it. Good luck.
