# Hyde

A Jekyll blog theme (forked from [Reverie](https://github.com/amitmerchant1990/reverie)) with one addition: **a mobile-first post composer that writes directly to GitHub, no app or server required.**

Open `/compose.html` on your live site from any phone or computer, write a post, hit publish. It commits straight to your repo via the GitHub API. Drafts, image pasting, GIF support, and a load-and-edit picker for existing posts are all built in.

---

## 🗑 Setup — delete this section once you're done

### 1. Fork and rename

Click **Use this template** (or fork normally), then rename the new repository to `YOUR-GITHUB-USERNAME.github.io`. This exact naming is what makes GitHub Pages serve it automatically.

### 2. Enable GitHub Pages

In your new repo: **Settings → Pages**. Set the source to the `master` (or `main`) branch, root folder. Your site will be live at `https://YOUR-GITHUB-USERNAME.github.io` within a minute or two.

### 3. Edit `_config.yml`

Open `_config.yml` and replace the placeholders:

- `name` — your blog's name
- `author` — your name
- `description` — a short tagline
- `avatar` — point this at your own image, or upload one to `/images/`
- `url` / `enforce_ssl` — your site URL
- `footer-links` — fill in whichever social accounts you want shown, leave the rest blank

### 4. Create a GitHub Personal Access Token

The composer needs a token to write to your repo on your behalf.

1. Go to [github.com/settings/tokens?type=beta](https://github.com/settings/tokens?type=beta)
2. **Generate new token** → fine-grained
3. **Repository access** → only select repositories → your `*.github.io` repo
4. **Permissions** → Repository permissions → **Contents** → Read and write
5. Generate, copy the token (starts with `github_pat_`)
6. Save it somewhere safe — a password manager is ideal, since you'll only see it once

### 5. Configure the composer

Open `/compose.html` in this repo and edit the four lines at the top of the `<script>` block:

```js
const GH_USER    = 'YOUR-GITHUB-USERNAME';
const GH_REPO    = 'YOUR-GITHUB-USERNAME.github.io';
const GH_BRANCH  = 'master';   // check Settings → Pages if unsure
const SITE_URL   = 'https://YOUR-GITHUB-USERNAME.github.io';
```

Commit that change. Then visit `https://YOUR-GITHUB-USERNAME.github.io/compose.html`, tap the **⚿ token** button, paste your PAT, and save. You're ready to write.

### 6. (Optional) Custom domain

If you'd rather use your own domain instead of `*.github.io`, you have two routes:

**Route A — GitHub Pages native DNS**
Add a `CNAME` file to the repo root containing your domain, then add the DNS records GitHub specifies under **Settings → Pages → Custom domain**. Simple, but you're relying on GitHub's edge network and basic HTTPS.

**Route B — Cloudflare in front (recommended)**
Point your domain's nameservers at Cloudflare, keep GitHub Pages as the origin, and let Cloudflare handle DNS, SSL, and caching. This gets you a CDN, more flexible redirect rules, and faster failover if GitHub Pages has issues. Cloudflare's free tier covers this completely. Search "Cloudflare GitHub Pages custom domain" for an up to date walkthrough — the steps occasionally shift as both products update.

Either way, once your domain is live, update `url` and `enforce_ssl` in `_config.yml` and the `SITE_URL` line in `compose.html` to match.

### 7. Delete your training wheels

Once everything above is done — delete this entire section from the README, delete the sample `Hello, Hyde` post in `_posts/`, and replace the rest of this file with whatever you want people to see when they land on your repo.

---

## What's actually in this repo

- **Reverie** — the Jekyll theme itself (layouts, Sass, includes), unchanged from upstream except for the placeholder content
- **`compose.html`** — the mobile post composer, the actual point of this fork
- **`_drafts/`, `shared/`** — empty folders (with `.gitkeep`) that the composer writes to
- **`_posts/2026-06-17-Hello-Hyde.md`** — a single sample post, safe to delete

## Using the composer day to day

Open `compose.html` on your site. Front matter (title, date, tags, excerpt) is handled by form fields — you just write the body in Markdown.

A few things worth knowing:

- **Paragraphs need a blank line between them.** Single returns join onto the same line, same as standard Markdown/Kramdown. The composer has a `¶` button that inserts an extra visual gap if you want more space than a normal paragraph break gives you.
- **Pasting a screenshot** while writing stages it as an image, resizes it, and inserts the right Markdown reference automatically.
- **Drafts** live in `_drafts/` and don't appear on the live site. The load picker shows both posts and drafts, color-coded.
- **Editing an existing post** and changing its title will delete the old file automatically once the new one is committed successfully — no orphaned duplicates.
- **Handoff docs** — attach any `.md` or `.txt` file (a writeup, a methodology, notes from somewhere else) and the composer commits it to `/shared/` with a copyable link to drop into your post.

## License

MIT, same as upstream Reverie. See `LICENSE`.
