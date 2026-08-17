# Madhushri Patil — portfolio + blog

Astro site. Free to host, free to edit, no paid services.

## Everything is editable from a browser

Once deployed, go to **yoursite.com/admin**, log in, and you get forms for:

- **Homepage content** — name, intro, photo, about paragraphs, work history, projects (with images), roadmap, thinking, off-screen
- **Blog posts** — create, write, upload images, publish

Publish saves to GitHub, which rebuilds the site. Live in about a minute.

## Deploy free on Netlify

1. Push this repo to GitHub (free).
2. netlify.com → Add new site → Import from GitHub → pick the repo.
3. Base directory `site` · Build command `npm run build` · Publish directory `site/dist`.

## Turn on the admin panel (free)

In your Netlify site dashboard:

1. **Site configuration → Identity → Enable Identity**
2. Identity → **Registration: Invite only** → **Invite users** → your email (accept the link, set a password)
3. Identity → **Services → Git Gateway → Enable**

Then visit `yoursite.com/admin` and log in.

## Images

Upload through the admin panel, or drop files into `site/public/images/`. The homepage expects `portrait.jpg`, `project-eval.jpg`, `project-robot.jpg` until you replace them from the panel.

## Run locally (optional)

```bash
cd site
npm install
npm run dev
```
