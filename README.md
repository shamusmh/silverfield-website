# Silver Field Capital — Marketing Site

A 5-page static marketing site for Silver Field Capital. Built as plain HTML/CSS — no build step, no framework, no dependencies. Drop it on any static host and it works.

## Pages

| File | Purpose |
|---|---|
| `index.html` | Home / hero — "Who we are" |
| `approach.html` | Values, how we're different, the playbook, operating model |
| `criteria.html` | What we look for in target businesses |
| `team.html` | Shamus + John bios |
| `contact.html` | Contact form with role-based routing |
| `styles.css` | All shared styling |

## Before You Publish — Three Things To Do

### 1. Add John Rietema's bio
Open `team.html` and search for `PLACEHOLDER BIO`. Replace the placeholder paragraphs and the three credential chips with John's real background.

### 2. Wire up the contact form (5 minutes)
The form posts to **Formspree** (free, no credit card needed for the basic plan).

1. Sign up at https://formspree.io
2. Click **+ New Form**, name it "Silver Field Site"
3. Set the receiving email to where you want submissions to land (probably `shamus@silverfieldcapital.com`)
4. Formspree will give you a form endpoint that looks like `https://formspree.io/f/abcd1234`
5. In `contact.html`, find `YOUR_FORM_ID` and replace it with your real form ID (the part after `/f/`)

Free tier is 50 submissions/month. If you need more, the paid tier is around $10/month, or swap to **Web3Forms** (free, unlimited) — same setup pattern.

### 3. (Optional) Replace the placeholder portraits
The team page currently uses initials as portraits (SH and JR). If you want actual photos:
- Add `shamus.jpg` and `john.jpg` to the project folder
- In `team.html`, replace `<span class="team-initials">SH</span>` with `<img src="shamus.jpg" alt="Shamus Hines" style="width:100%;height:100%;object-fit:cover;">`

---

## Deployment — GitHub + Cloudflare Pages

### Step 1 — Push to GitHub

```bash
cd silverfield
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/silverfield.git
git push -u origin main
```

(Create the repo on github.com first — make it private if you don't want the source public.)

### Step 2 — Deploy on Cloudflare Pages

1. Log in to https://dash.cloudflare.com
2. **Workers & Pages → Create → Pages → Connect to Git**
3. Authorize Cloudflare to access your GitHub, select the `silverfield` repo
4. Build settings:
   - **Framework preset:** None
   - **Build command:** *(leave blank)*
   - **Build output directory:** `/`
5. Click **Save and Deploy**

Within ~60 seconds you'll have a live site at something like `silverfield.pages.dev`.

### Step 3 — Connect silverfieldcapital.com

1. In your Cloudflare Pages project: **Custom domains → Set up a custom domain**
2. Enter `silverfieldcapital.com`
3. If your domain DNS is already on Cloudflare, it auto-configures. If not, follow Cloudflare's instructions to point your nameservers (your registrar will let you do this — it's a one-time DNS change).
4. Add `www.silverfieldcapital.com` as a second custom domain so both versions work.

### Step 4 — You're live

Every time you push a change to GitHub (`git push`), Cloudflare auto-rebuilds and redeploys within a minute. To make a content change:

```bash
# edit the file, then:
git add .
git commit -m "Updated John's bio"
git push
```

Done.

---

## Design Notes

- **Type:** Fraunces (display) + Manrope (body), pulled from Google Fonts via CSS `@import`. Already wired up.
- **Color palette:** Deep navy base (`#07101f`) with three accents — sky blue (`#7cb8e8`), warm gold (`#d4a574`), and mint (`#7dd3b7`). All exposed as CSS variables in `styles.css` if you want to tweak.
- **Logo:** Currently using an inline SVG shield-and-tree mark. If you have a proper brand logo file, drop it in and swap the `<svg>` in the nav (and in the hero) with an `<img>` tag.
- **No JavaScript dependencies.** A tiny inline script on each page handles scroll reveals and (on contact) form submission. Everything works without JS too — JS just adds polish.
- **Mobile-responsive** down to 380px.
- **Accessibility:** Semantic HTML, reduced-motion support, proper form labels, keyboard-navigable.
