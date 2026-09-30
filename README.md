# Kessler & Associates — website

Static HTML. No build step, no dependencies. 18 pages.

Open `authority-site.html` directly, or serve the folder:

    python3 -m http.server 8000

## Deploying to Netlify

Publish directory is the repo root; `netlify.toml` sets it. Build command is empty.

- **Connect the repo**: Netlify → Add new site → Import an existing project → this
  repo → deploy from `main`. `netlify.toml` fills in the rest.
- **Or drag and drop**: zip this folder and drop it at https://app.netlify.com/drop.
  To update an existing site instead of creating a new one: that site → Deploys →
  drag onto "Need to update your site?".

`_redirects` serves the homepage at `/` without changing any page's canonical URL.
`_headers` sets security headers and asset caching.

## Pages

| File | Page |
| --- | --- |
| `authority-site.html` | Home |
| `authority-car-accident.html` | Car, Truck & Rideshare Accidents |
| `authority-construction.html` | Construction & Labor Law |
| `authority-malpractice.html` | Medical Malpractice |
| `authority-wrongful-death.html` | Wrongful Death |
| `authority-catastrophic.html` | Catastrophic Injuries |
| `authority-premises.html` | Premises Liability |
| `authority-manhattan.html` … `authority-harlem.html` | 8 area-served pages |
| `authority-blog-1.html` … `-3.html` | 3 articles |

## SEO / AEO state

Every page has a unique title under 60 characters, a description between 120 and
160, an absolute canonical, full Open Graph and Twitter tags, and JSON-LD
(`LegalService`, `Service`, `BreadcrumbList`, `FAQPage`, `Article`). FAQ markup
mirrors the visible page text exactly, which Google's structured data policy
requires. `sitemap.xml`, `robots.txt` and `llms.txt` are generated and current.

Audited clean against the website-seo-aeo playbook:

    audit_site.py     ISSUES 0    (18 pages, 18 sitemap urls)
    browser_check.js  problems 0  (18 pages × 390px and 1440px, contrast included)

## Before this goes on a real domain

1. **Attorney photos are placeholders.** The three headshots are Unsplash images of
   real people unconnected to the firm. Replace the `src` on each `.att-card img`.
2. **Nothing legal has been verified.** Recovery figures, case counts and every
   statute citation need attorney review — the site cites CPLR 214(5) and 214-a,
   EPTL 5-4.1 and 11-3.2, Gen. Mun. Law 50-e, Ins. Law 5102(d), Labor Law 240 and
   241(6), NYC Admin. Code 7-210, and 11 NYCRR 65-1.1.
3. **Forms post nowhere.** They validate and show a confirmation only. Wire them to
   an intake endpoint or Netlify Forms before launch.
4. **Change the domain** if it is not `sweet-platypus-bc9aa4.netlify.app`. Canonicals,
   OG URLs, `sitemap.xml`, `robots.txt` and `llms.txt` all carry the hostname.
5. **Placeholder links**: the Google review URL is `https://g.page/r/leave-review`.

## After launch

Submit `sitemap.xml` to Google Search Console and to Bing Webmaster Tools — Bing is
the index behind ChatGPT search and Copilot, so it is the one that affects whether
AI assistants cite the firm. Then spot-check one practice page and one article in
Google's Rich Results Test.
