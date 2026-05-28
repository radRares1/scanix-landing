# Scanix Landing Page — Deployment Guide

This guide walks you through two things:

1. **Connecting the email forms** via Web3Forms (free, no credit card)
2. **Publishing the landing page** live on GitHub Pages (free)

Total time: ~10–15 minutes.

---

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Step 1 — Set Up Web3Forms](#step-1--set-up-web3forms)
3. [Step 2 — Update index.html with Your Access Key](#step-2--update-indexhtml-with-your-access-key)
4. [Step 3 — Deploy to GitHub Pages](#step-3--deploy-to-github-pages)
5. [Step 4 — (Optional) Connect a Custom Domain](#step-4--optional-connect-a-custom-domain)
6. [Step 5 — Test Your Live Site](#step-5--test-your-live-site)
7. [Troubleshooting](#troubleshooting)

---

## Prerequisites

- A **GitHub account** — [github.com/signup](https://github.com/signup) (free)
- The file `index.html` from this project folder
- A modern web browser

---

## Step 1 — Set Up Web3Forms

Web3Forms is a free email-forwarding service. When a visitor submits the email capture form on your landing page, Web3Forms sends the submission to your inbox — no backend or server needed.

### 1.1 Create a free account

1. Go to **[https://web3forms.com](https://web3forms.com)**.
2. Click **Get your Access Key** (or **Sign Up Free**).
3. Enter your email address (this is where form submissions will be delivered).
4. Check your inbox and click the confirmation link.

### 1.2 Copy your Access Key

After confirming your email, Web3Forms shows you your **Access Key** — a string that looks like:

```
xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

Copy this key. You'll paste it into `index.html` in the next step.

> **Free plan limits:** 250 submissions/month on the free tier. For a new landing page this is more than enough. No credit card is required.

---

## Step 2 — Update index.html with Your Access Key

The file `index.html` contains the placeholder text **`COLOCA_CHEIA_AICI`** in several places. You must replace every occurrence with your real Web3Forms access key.

There are **4 occurrences** to replace:

| Line (approx.) | Context |
|---|---|
| Line 10 | Meta tag (commented out — optional, can leave as-is) |
| Line 1131 | Hero form — `data-web3forms-key` attribute |
| Line 1132 | Hero form — hidden `access_key` input |
| Line 1552 | Footer form — hidden `access_key` input |

### Option A — Using a text editor (recommended for beginners)

1. Open `index.html` in **Notepad** (Windows), **TextEdit** (Mac, plain text mode), or any code editor (VS Code, Sublime Text).
2. Use **Find & Replace** (`Ctrl+H` on Windows / `Cmd+H` on Mac).
3. In the **Find** field, type exactly:
   ```
   COLOCA_CHEIA_AICI
   ```
4. In the **Replace** field, paste your Web3Forms access key (e.g. `a1b2c3d4-...`).
5. Click **Replace All** — it should report **4 replacements**.
6. Save the file.

### Option B — Using the terminal (command line)

If you're comfortable with the command line:

```bash
# macOS / Linux
sed -i 's/COLOCA_CHEIA_AICI/YOUR_ACCESS_KEY_HERE/g' index.html

# Windows PowerShell
(Get-Content index.html) -replace 'COLOCA_CHEIA_AICI', 'YOUR_ACCESS_KEY_HERE' | Set-Content index.html
```

Replace `YOUR_ACCESS_KEY_HERE` with your actual key.

### Verify the replacement

After saving, open `index.html` in your browser and check that the forms render correctly (no visible placeholder text).

---

## Step 3 — Deploy to GitHub Pages

GitHub Pages hosts static websites (HTML, CSS, JS) directly from a GitHub repository — completely free.

### 3.1 Create a new repository

1. Go to **[https://github.com/new](https://github.com/new)**.
2. Fill in the form:
   - **Repository name:** `scanix-landing` (or any name you like, e.g. `scanix`)
   - **Visibility:** Public *(GitHub Pages requires Public for free accounts)*
   - Leave everything else as default (no README, no .gitignore).
3. Click **Create repository**.

### 3.2 Upload index.html

GitHub lets you upload files directly in the browser — no Git knowledge required.

1. On your new (empty) repository page, click **uploading an existing file** (the link in the middle of the page), or click **Add file → Upload files**.
2. Drag and drop your `index.html` file into the upload area, or click **choose your files** and select it.
3. Scroll down to the **Commit changes** section.
4. Leave the default commit message ("Add files via upload") or write something descriptive like `Add Scanix landing page`.
5. Make sure **Commit directly to the `main` branch** is selected.
6. Click **Commit changes**.

> **If you have other assets** (images, fonts, CSS files): upload them the same way, preserving the folder structure that `index.html` references. The Scanix `index.html` is fully self-contained (all styles and scripts are inline), so a single file upload is all you need.

### 3.3 Enable GitHub Pages

1. In your repository, click the **Settings** tab (top navigation bar).
2. In the left sidebar, scroll down and click **Pages**.
3. Under **Build and deployment**:
   - **Source:** Select **Deploy from a branch**
   - **Branch:** Select **main** (or **master** if that's what your repo uses)
   - **Folder:** Select **/ (root)**
4. Click **Save**.

GitHub will now build and deploy your site. This takes **1–3 minutes**.

### 3.4 Find your live URL

After saving, the Pages settings page will display a banner:

> ✅ Your site is live at **https://username.github.io/scanix-landing/**

The URL format is always:
```
https://<your-github-username>.github.io/<repository-name>/
```

Click the URL to confirm your site is live.

> **Tip:** If the page shows a 404 error immediately after enabling Pages, wait 2–3 minutes and refresh. The first deployment takes a little time.

---

## Step 4 — (Optional) Connect a Custom Domain

If you own a domain (e.g. `scanix.ro`) and want to use it instead of the `.github.io` URL:

### 4.1 Add your domain in GitHub Pages settings

1. Go to **Settings → Pages** in your repository.
2. Under **Custom domain**, type your domain (e.g. `scanix.ro` or `www.scanix.ro`).
3. Click **Save**. GitHub will create a `CNAME` file in your repo.

### 4.2 Update your DNS records

Log in to your domain registrar (the place where you bought the domain) and add these DNS records:

**For an apex domain (e.g. `scanix.ro`)** — add four A records:
```
Type: A    Host: @    Value: 185.199.108.153
Type: A    Host: @    Value: 185.199.109.153
Type: A    Host: @    Value: 185.199.110.153
Type: A    Host: @    Value: 185.199.111.153
```

**For a www subdomain (e.g. `www.scanix.ro`)** — add a CNAME record:
```
Type: CNAME    Host: www    Value: <your-github-username>.github.io
```

DNS changes can take **up to 24 hours** to propagate, though often much faster.

### 4.3 Enable HTTPS

Once GitHub verifies your domain (the Pages settings page will show a green checkmark), tick **Enforce HTTPS** for a secure connection. This is strongly recommended.

---

## Step 5 — Test Your Live Site

Once the site is live, test everything end-to-end:

### Test the email forms

1. Open your live site URL.
2. Enter a test email address in the **hero form** (top of page) and click the submit button.
3. Scroll to the bottom and do the same with the **footer form**.
4. Check the inbox you registered with Web3Forms — you should receive a notification email within a few seconds.

### View submissions in Web3Forms dashboard

1. Go to **[https://web3forms.com](https://web3forms.com)** and log in.
2. Click **Dashboard** or **Submissions** to see all received entries with timestamps.
3. You can also set up email notifications, Slack alerts, and more from the dashboard.

### Verify the page loads correctly

- Check the page on **mobile** (use browser DevTools or an actual phone).
- Confirm all images and sections render properly.
- Test the FAQ accordion (click to expand/collapse).

---

## Troubleshooting

### 🔴 Form submissions are not arriving in my inbox

| Possible cause | Fix |
|---|---|
| `COLOCA_CHEIA_AICI` was not fully replaced | Open `index.html`, search for `COLOCA_CHEIA_AICI` — if any instances remain, replace them with your key and re-upload the file. |
| Wrong access key pasted | Double-check the key in your Web3Forms dashboard. Keys are case-sensitive. |
| Email went to spam | Check your spam/junk folder and mark Web3Forms emails as "not spam". |
| Web3Forms free quota exceeded | Log in to web3forms.com and check your monthly submission count. |
| Form submitted while page is served as `file://` | Web3Forms requires the page to be served over HTTP(S). Always test on the live GitHub Pages URL, not by opening the file locally. |

### 🔴 GitHub Pages shows a 404 error

| Possible cause | Fix |
|---|---|
| Pages not yet deployed | Wait 2–3 minutes after enabling Pages and refresh. |
| Wrong file name | The main file **must** be named exactly `index.html` (all lowercase). Rename it if needed. |
| Wrong branch selected | In Settings → Pages, confirm "main" (or your default branch) is selected. |
| Repository is private | GitHub Pages requires a Public repository on free accounts. |

### 🔴 The page looks broken (missing styles or images)

| Possible cause | Fix |
|---|---|
| Assets uploaded to wrong path | If `index.html` references `images/logo.png`, the `images/` folder must exist in the repository root. |
| Cached old version | Hard-refresh with `Ctrl+Shift+R` (Windows) or `Cmd+Shift+R` (Mac). |

### 🔴 Custom domain not working

| Possible cause | Fix |
|---|---|
| DNS not propagated yet | Wait up to 24 hours. Use [dnschecker.org](https://dnschecker.org) to check propagation. |
| CNAME file missing | Re-add the custom domain in Settings → Pages to recreate the CNAME file. |
| HTTPS certificate not issued | Wait 15–30 minutes after DNS propagates, then tick "Enforce HTTPS" in Pages settings. |

---

## Quick Reference

| Item | Value / Location |
|---|---|
| Web3Forms signup | https://web3forms.com |
| Placeholder to replace | `COLOCA_CHEIA_AICI` (4 occurrences in index.html) |
| GitHub Pages settings | Repository → Settings → Pages |
| Live site URL | `https://<username>.github.io/<repo-name>/` |
| Web3Forms dashboard | https://web3forms.com/dashboard |

---

*Guide created for the Scanix landing page project.*
