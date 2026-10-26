# matterflow-usa.com

Static site. No build step, no framework, no dependencies.

```
index.html            the whole site — all copy lives here
style.css             the design system — tokens at the top
robots.txt            keeps the site out of search results
assets/               photos, diagrams, favicon, social card
```

Repository: **github.com/MatterFlow-web/matterflow-site**

---

## 1 · Upload the files

Open the repo and click **uploading an existing file** (or **Add file ▸ Upload files**).

Unzip this folder and drag in **the contents**, not the folder itself. `index.html` must sit at
the repository root, not inside a `site/` folder — this is the single most common mistake.

When it's done the repo should list exactly:

```
index.html   style.css   robots.txt   README.md   assets/
```

Write a commit message and click **Commit changes**.

> There is deliberately **no CNAME file** in this upload. GitHub writes one for you in step 3,
> and having one present before DNS is configured makes the site unreachable while you're
> trying to check it.

## 2 · Turn on Pages and check it works

**Settings ▸ Pages ▸ Source: Deploy from a branch ▸ Branch `main` / `(root)` ▸ Save.**

Wait a minute, then open:

```
https://matterflow-web.github.io/matterflow-site/
```

Look at it properly — on a phone too. Fix anything that needs fixing before you touch DNS. At
this point nothing points at your domain, so there is no way to break anything.

## 3 · Claim the domain in GitHub — before DNS

**Settings ▸ Pages ▸ Custom domain** → enter `matterflow-usa.com` → **Save**.

GitHub commits a `CNAME` file for you. Do this *before* step 4: pointing DNS at GitHub without
first claiming the domain in your repo leaves a window where someone else could serve a site
on it.

## 4 · DNS at Squarespace

**Squarespace account ▸ Domains ▸ matterflow-usa.com ▸ DNS.**

Add four **A records** on the apex (host `@`):

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

Add one **CNAME** so the www address works:

```
Host: www    →    matterflow-web.github.io
```

## ⚠ Do not break your email

This domain is managed by **Google Workspace**, and its **MX records** deliver your mail.

- **Add** the records above. Never use "reset to defaults", "remove all records", or any bulk
  replace option.
- **Leave every MX record untouched.**
- Leave Domain Forwarding empty.

Adding A and CNAME records does not affect mail. Wiping the zone does, and that is how people
take their own email offline during a migration.

## 5 · HTTPS

Back in **Settings ▸ Pages**, wait for the DNS check to pass, then tick **Enforce HTTPS**.
GitHub issues a free certificate. Usually minutes; allow up to 24 hours.

---

## Editing later

Click any file in GitHub, hit the pencil, edit, commit. The site rebuilds in about a minute.

- **Copy** — `index.html`, in sections marked by comments.
- **Colours, type, spacing** — the `:root` block at the top of `style.css`. Change `--mint`
  once and it changes everywhere.
- **Photos** — drop a replacement into `assets/` using the same filename and it swaps itself.

## What's on the page

Hero (sort-line photo with live-style ID boxes) · 01 Mission · 02 The problem (four tabs with
images) · 03 How it works (Full build / Cutaway toggle, five steps, spec strip) · 04 Waste
auditing (illustrative dashboard, "Where the record goes." tabs, data commitments) · 05 What
changes · 06 Pilot · 07 Where we're going · 08 Team · 09 Careers · 10 Contact.

Works on phones, iPads, and desktop: every tab and toggle responds to tap and keyboard as well
as mouse.

**Hero detection boxes** are positioned as percentages of `assets/hero-sort-line-*.jpg`. If the
photo is swapped, move each `.bbox` (`--x`, `--y`, `--w`, `--h` in `index.html`) onto real items,
and only tag aluminum as ID: YES.

**Renders** in How it works come from the Figma file "MatterFlow System Design" (node 2:5 full
build, node 3:155 cutaway), exported as `assets/mechanism-*.webp` on one 1200 x 1200 canvas. The
numbered pins are percentages of that canvas.

**Image placeholders** in the use-case tabs (A to D) say what photo belongs there. Replace the
`.ph` block with an `<img>` when it arrives.

**Photo credits:** the game-day photo in problem tab 01 is by John McGillen / USC Athletics and is
credited in its caption and alt text. Credit any outside photo the same way (a `.credit` span
inside the `figcaption`).

**The dashboard numbers are sample data**, tagged on the page as illustrative. Replace them with
pilot results once they exist.

## Notes

**Search indexing is off.** `robots.txt` plus a `noindex` meta tag keep the site out of search
results and name the major AI crawlers explicitly. It stays public to anyone with the link —
noindex is a request to crawlers, not a lock. Delete both when you want to be found.

**The repo is public**, which the free GitHub Pages tier requires. Nothing sensitive is in it,
but the source is readable by anyone who finds it.

**The one-day figure is stated as a target**, not a result. Once the Coliseum pilot produces a
real number, change that line in `index.html` — an achieved figure is a far stronger claim.

**Contact is a `mailto:` link.** Static hosting has no form handler. If you want a real form,
Formspree's free tier needs only a form `action` attribute.
