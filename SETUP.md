# Portfolio site — setup guide

Three style variants, all single-file HTML. No build step, no dependencies.

| Folder | Style |
|---|---|
| `variant-minimal/` | Clean, lots of white space. Auto light/dark. |
| `variant-bold/` | Dark, gradient accents, scroll animations. |
| `variant-warm/` | Cream + rust, serif headings, personal tone. |

Open each `index.html` in a browser to compare. Pick one — you only deploy one.

---

## 1. Deploy to GitHub Pages

1. Create a repo named **`YOUR-USERNAME.github.io`** (use your real GitHub username — the name must match exactly).
2. Copy the `index.html` from your chosen variant into the root of that repo.
3. Push. Wait ~1 minute.
4. Visit `https://YOUR-USERNAME.github.io`

That's it. Pages is on by default for repos named this way. For any other repo name, go to **Settings → Pages → Source → Deploy from branch → `main` / root**, and your URL becomes `https://YOUR-USERNAME.github.io/repo-name`.

**Custom domain (optional):** buy a domain, add a file named `CNAME` at the repo root containing just `yourdomain.com`, then point your domain's DNS at GitHub's IPs. Settings → Pages walks you through it.

---

## 2. Wire up the contact form

The form uses [Formspree](https://formspree.io) — free tier covers 50 submissions/month.

1. Sign up with `azizrajimbunda@gmail.com`.
2. Create a new form. Copy the form ID (looks like `xyzabcd`).
3. In `index.html`, find:
   ```html
   <form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```
   Replace `YOUR_FORM_ID` with yours.
4. Submit the form once yourself — Formspree emails you to confirm.

Alternatives if you'd rather not use Formspree: [Web3Forms](https://web3forms.com) (no signup, unlimited), or Netlify Forms if you switch hosts.

---

## 3. Find-and-replace before you publish

In whichever `index.html` you picked, search for these and fix them:

- `YOUR-USERNAME` → your GitHub username (appears in the GitHub link and the `og:` meta tags)
- `YOUR_FORM_ID` → your Formspree form ID
- Every `<!-- TODO: ... -->` comment → your actual words
- Each project's `href="#"` → the real link (GitHub repo, live demo, or a Facebook post)

Your Facebook page URL and email are already filled in correctly.

---

## 4. Adding a project

Each project is one self-contained block. Copy the block marked `PROJECT TEMPLATE`, paste it above the others (newest first), and edit:

```html
<a class="project" href="https://github.com/you/thing" target="_blank" rel="noopener">
  <h3>Thing</h3>
  <p>What it does, in one or two plain sentences.</p>
  <div class="tags">
    <span class="tag">Python</span>
    <span class="tag">CLI</span>
  </div>
  <div class="meta">2026 · Open source</div>
</a>
```

Write the description around the *outcome*, not the stack. "Cuts invoice processing from 2 hours to 5 minutes" beats "Built with Python and Pandas."

---

## 5. Social preview image

When you paste your site link on Facebook, it pulls the `og:image`. Without one you get a blank grey card.

1. Make a 1200×630px PNG — your name, one line about what you do, that's enough.
2. Save it as `assets/og-image.png` in the repo.
3. The meta tag already points there once you replace `YOUR-USERNAME`.
4. Test it at [Facebook's Sharing Debugger](https://developers.facebook.com/tools/debug/) — this also forces Facebook to re-scrape if you update the image later.

---

## 6. Using the website + Facebook page together

They do different jobs. The site is the **permanent record**; the page is the **distribution**.

**Set up once:**
- Add the website URL to your Facebook page's About → Website field.
- Add a "Learn More" or "Contact Us" call-to-action button on the page pointing at your site.

**Per project, in order:**

1. **Write it up on the website first.** This is the canonical version — it's yours, it doesn't disappear into an algorithm, and it's what you send a client.
2. **Post to Facebook with the link.** Native photos or a short video get much more reach than a bare link, so lead with an image and put the URL in the post text. Say something specific about the project rather than "check out my new project."
3. **Reply to comments.** This is where the reaching-out part actually happens — Facebook rewards engagement, and it's how interested people find you.

**A rhythm that works:** website post is the long version (what, why, how, what you learned). Facebook post is the hook (one image, one interesting detail, one link). Don't duplicate the text.

**When talking to clients:** send the website. It has no ads, no distractions, no "People You May Know" in the sidebar. The Facebook page is for discovery; the site is for closing.

---

## Notes

- All three variants are mobile-responsive and work with JavaScript disabled (except the scroll animations in the bold variant, which degrade to just showing everything).
- The bold variant respects `prefers-reduced-motion`.
- Minimal and warm variants auto-switch to dark mode based on system settings.
- The warm variant loads fonts from Google Fonts. If you want zero external requests, delete the two `<link rel="preconnect">` lines and the font `<link>`, and it'll fall back to Georgia.
