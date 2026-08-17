# Madhushri Patil — portfolio + blog

Astro site, hosted free on **Cloudflare Pages**, edited from a browser with **Sveltia CMS**.

No Netlify. No paid services. No terminal needed after setup.

## How editing works

Go to **yoursite.pages.dev/admin** and sign in. You get forms for:

- **Homepage content** — name, intro, photo, about paragraphs, work history, projects (with images), roadmap, thinking, off-screen
- **Blog posts** — create new posts, write in markdown, drag in images, publish

When you hit **Publish**, the CMS commits straight to `main` on GitHub. Cloudflare sees the commit
and rebuilds the site automatically. Live in about a minute.

---

## Setup — do this once

### 1. Deploy the site on Cloudflare Pages

1. Sign in at [dash.cloudflare.com](https://dash.cloudflare.com) (free account).
2. **Workers & Pages → Create → Pages → Connect to Git**, authorize GitHub, pick `portfolio-`.
3. Build settings:
   | Setting | Value |
   | --- | --- |
   | Framework preset | Astro |
   | Build command | `npm run build` |
   | Build output directory | `dist` |
   | Root directory | `site` |
4. **Save and Deploy.** You get a URL like `https://portfolio-abc.pages.dev`.

Put that URL into `site/astro.config.mjs` (the `site:` line) so links and metadata are correct.

### 2. Get into the admin panel

Open `yoursite.pages.dev/admin`. You'll see three buttons — use **Sign In Using Access Token**.

To make the token:

1. GitHub → **Settings → Developer settings → Personal access tokens → Fine-grained tokens →
   Generate new token**.
2. **Repository access**: Only select repositories → `portfolio-`.
3. **Permissions → Repository permissions**: set **Contents** to **Read and write**.
   (That's the only one you need.)
4. Set an expiry you're happy with, generate, and copy the token.
5. Paste it into the CMS login box.

The token is stored in your browser only. When it expires, generate a new one the same way.
Treat it like a password — don't paste it anywhere else.

That's it. You can now edit, upload and publish.

---

## Nicer login (optional)

The token works fine, but it expires and you have to re-paste it. If you'd rather click
**Sign In with GitHub** and be done, set up the OAuth worker:

1. Deploy [sveltia-cms-auth](https://github.com/sveltia/sveltia-cms-auth) to Cloudflare Workers
   (there's a deploy button in its README). Copy the worker URL.
2. GitHub → **Settings → Developer settings → OAuth Apps → New OAuth App**:
   - **Homepage URL**: your `.pages.dev` URL
   - **Authorization callback URL**: `https://your-worker-url.workers.dev/callback`
   - Register, then generate a client secret.
3. In the worker's **Settings → Variables and Secrets**, add:
   | Name | Value |
   | --- | --- |
   | `GITHUB_CLIENT_ID` | from the OAuth app |
   | `GITHUB_CLIENT_SECRET` | from the OAuth app |
   | `ALLOWED_DOMAINS` | e.g. `portfolio-abc.pages.dev` |
4. In `site/public/admin/config.yml`, uncomment the `base_url` line and set it to your worker URL.
   Commit and push.

---

## Writing a blog post

1. Open `/admin` → **Blog posts** → **New Blog posts**.
2. Fill in title, summary, date, tag. Write the body in the markdown editor.
3. Need an image? Click the image button, drag a file in — it uploads to `site/public/images/`
   and gets inserted for you.
4. Leave **Draft** off to publish, or turn it on to keep it hidden from the site.
5. **Publish** → committed to `main` → site rebuilds.

## Images

Anything you upload through `/admin` lands in `site/public/images/` and is referenced as
`/images/filename.jpg`. You can also drop files into that folder directly and push.

The homepage currently uses placeholder graphics for the portrait and the two project images —
replace them from **Homepage content** in the admin panel.

## Editing without deploying (optional)

You can run the CMS locally against files on your own disk — useful for drafting offline, and it
needs no token at all.

```bash
cd site
npm install
npm run dev
```

Open `http://localhost:4321/admin` in Chrome or Edge and choose **Work with Local Repository**.
Edits write straight to your files; commit and push when you're happy.

## Custom domain (optional)

Cloudflare Pages → your project → **Custom domains → Set up a domain**. If the domain is already
on Cloudflare it's one click. Afterwards, update `site/astro.config.mjs` and (if you set up the
worker) `ALLOWED_DOMAINS` to match.
