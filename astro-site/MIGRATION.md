# Migrate to Cloudflare Pages

## Phase 1: Cloudflare Account + Domain Zone

1. Create a Cloudflare account at https://dash.cloudflare.com (if you don't have one)
2. Click "Add a site" and enter `patrickspieker.com`
3. Select the **Free** plan
4. Cloudflare will scan and import your existing DNS records — verify they look right
5. Cloudflare gives you two nameservers (e.g. `ada.ns.cloudflare.com`, `bob.ns.cloudflare.com`)
6. Go to your current registrar and change the nameservers to the two Cloudflare gave you
7. Wait for propagation (usually <1 hour, can take up to 48)

Your site still works during this step — Cloudflare proxies to GitHub Pages using the imported DNS records.

## Phase 2: Push the Astro Site

The Astro project is in the `astro-site/` directory. You can either:

**Option A: Replace the current repo contents**
```bash
# From the repo root
git checkout -b astro-migration

# Move astro project files to root
cp -r astro-site/* .
cp astro-site/.* . 2>/dev/null

# Remove old files
rm -rf blog/ essays/ labnotes/ projects/ drink/ style.css CNAME Gemfile.lock index.html old-prof.png astro-site/

# Commit
git add -A
git commit -m "migrate to astro"
git push -u origin astro-migration
```

**Option B: New repo** (cleaner)
```bash
cd astro-site
git init
git remote add origin git@github.com:PatrickSpieker/patrickspieker.github.io.git
# Or create a new repo like PatrickSpieker/site
git add -A
git commit -m "initial astro site"
git push -u origin main
```

## Phase 3: Connect to Cloudflare Pages

1. Go to Cloudflare Dashboard > **Workers & Pages** > **Create** > **Pages** tab
2. Click **Connect to Git** and select your GitHub repo
3. Set the build configuration:
   - **Build command**: `npm run build`
   - **Build output directory**: `dist`
   - **Production branch**: `main` (or whatever your default branch is)
4. Click **Save and Deploy**
5. Wait for the build to finish — your site is now live at `<project-name>.pages.dev`
6. Visit the `.pages.dev` URL and verify everything looks right

## Phase 4: Point the Custom Domain

1. In Cloudflare Pages: your project > **Custom domains** > **Set up a domain**
2. Enter `patrickspieker.com`
3. Since your domain zone is already on Cloudflare (Phase 1), it will automatically create the right DNS records
4. Remove the old GitHub Pages DNS records (A records or CNAME pointing to `patrickspieker.github.io`)
5. Wait for SSL certificate to provision (automatic, usually minutes)
6. Verify: `patrickspieker.com` should now serve your Astro site

## Phase 5: Clean Up + Make Private

1. **Disable GitHub Pages**: repo Settings > Pages > set source to "None"
2. **Delete the CNAME file** from the repo if it's still there
3. **Make the repo private**: repo Settings > Danger Zone > Change visibility > Private
4. Push a small change and verify Cloudflare Pages still builds from the private repo

## Verification Checklist

- [ ] `patrickspieker.com` loads with valid SSL
- [ ] Homepage shows correctly with nav bar
- [ ] `/blog` shows "No posts yet"
- [ ] `/essays` lists Inversion with link
- [ ] `/essays/inversion` renders the full essay
- [ ] `/labnotes` shows all lab notes with images
- [ ] `/projects` shows the Syria visualization link
- [ ] `/drink` redirects to Google Form
- [ ] Repo is private on GitHub
- [ ] Pushing a commit triggers a new Cloudflare Pages build

## Writing a New Blog Post

Once deployed, writing a post is:

1. Create `src/content/blog/my-post-title.md`:
```markdown
---
title: "My Post Title"
date: 2026-04-16
---

Write your content here in Markdown.
```

2. Push to GitHub — Cloudflare Pages rebuilds automatically.

To preview locally first: `npm run dev` (runs at `localhost:4321`).

Set `draft: true` in front matter to hide a post from the blog list while you work on it.
