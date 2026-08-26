# Medium C website

A plain, static marketing website for Medium C, a Sydney-based social media and content marketing studio. No frameworks, no build step: semantic HTML, one shared stylesheet, and a small vanilla JS file for the mobile nav and a subtle scroll reveal.

## File structure

```
Medium C Website/
├── index.html          Home
├── about.html           About Us (founder section)
├── services.html         Services
├── case-studies.html      Case Studies
├── contact.html          Contact Us (Web3Forms form)
├── css/
│   └── style.css         Shared stylesheet — colours, type, layout, components
├── js/
│   └── main.js           Mobile nav toggle, scroll reveal, footer year
├── images/                Founder photo lives here
├── _headers               Cloudflare Pages security headers
└── README.md
```

## Previewing locally

No build tools needed. Either:

1. Open `index.html` directly in a browser, or
2. Run a tiny local server from the project folder so relative paths and the browser's dev tools behave exactly as they will in production:

   ```bash
   python3 -m http.server 8000
   ```

   Then visit `http://localhost:8000`.

## Deploying to Cloudflare Pages

1. Push this folder to a GitHub repository.
2. In the Cloudflare dashboard, go to **Workers & Pages → Create → Pages → Connect to Git**, connect your GitHub account, and select the repo.
3. Build settings: leave the build command empty and set the build output directory to `/` (the repo root) — this is a plain static site, there's nothing to build.
4. Deploy. Cloudflare Pages will publish the site and give you a `*.pages.dev` URL to check first.
5. Once you're happy with the deploy, point your domain at it: in the Pages project go to **Custom domains → Set up a custom domain**, add `mediumc.com.au`, and follow the prompts. If `mediumc.com.au` is already using Cloudflare for DNS, this is close to instant; otherwise Cloudflare will show you the DNS records to add at your registrar.

### Builds are capped, not billed — batch your changes anyway

Cloudflare Pages' free plan is genuinely free for a site like this: static asset hosting has no bandwidth or request charges, and there's no spending cap to configure because there's no metered billing to run away from. The one number worth watching is **500 builds per month** on the free plan — each push to your production branch uses one. That's a lot of headroom for a small marketing site, but it's still good practice to batch up a handful of small edits into one push rather than deploying every single typo fix separately.

**Preview deployments are free to use liberally.** Push to any branch other than your production branch, or open a pull request, and Cloudflare Pages will build a preview URL you can check changes on without touching the live site. Merge to your production branch only when you're ready to publish.

## Contact form (Web3Forms)

The contact form on `contact.html` posts directly to [Web3Forms](https://web3forms.com), a free form-backend service — no server of your own required.

1. Go to [web3forms.com](https://web3forms.com) and generate an access key with your email address.
2. In `contact.html`, replace `[PLACEHOLDER-web3forms-key]` (the hidden `access_key` input's value) with your real access key.
3. That's it — submissions will be emailed to the address you registered. The hidden `botcheck` checkbox is Web3Forms' built-in honeypot: leave it as-is, it's invisible to real visitors and just needs to stay unchecked.

## Founder photo

The site is built to feature you, the founder, in three places: a small band on the Home page, a prominent section on the About Us page, and a friendly photo next to the contact form on the Contact page.

`images/founder.jpeg` is already in place and wired up on the Home page (both the hero and the "person behind Medium C" band). It's still a `[PLACEHOLDER-founder-photo]` reference on the About Us and Contact pages — point those at the same file (or a different crop of it) when you're ready, along with the matching `[PLACEHOLDER-founder-name]` and founder bio text on those two pages.

If you ever need to swap the photo, keep it a compressed web-sized JPG, ideally **under ~300 KB**, to keep the site fast (Squoosh or TinyJPG will do this in a few seconds; a width of around 1200px is more than enough for how the photo is displayed).

## Finding the placeholders

Every piece of content you need to personalise is wrapped in an obvious `[PLACEHOLDER...]` tag. Search the project for `PLACEHOLDER` to find them all in one pass:

```bash
grep -rn "PLACEHOLDER" --include="*.html" .
```
