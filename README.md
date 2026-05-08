# Remain Life Insurance &mdash; Website

Static site for **Remain Life Insurance Services, LLC** (Encinitas, California). Hosted on Vercel, source on GitHub.

## What's here

- `index.html` — homepage
- 17 spoke pages, one per coverage:
  `term-life.html`, `whole-life.html`, `universal-life.html`, `variable-life.html`, `ilit-funding.html`, `1035-exchange.html`, `term-conversion.html`, `life-settlements.html`, `412e3.html`, `professional-pension.html`, `key-person.html`, `legacy-giving.html`, `divorce-decree.html`, `collateral-assignment.html`, `vgli.html`, `premium-finance.html`, `policy-review.html`
- `404.html` — not-found page using brand chassis
- `vercel.json` — host config (URL rewrites, security headers, cache rules)
- `sitemap.xml`, `robots.txt`
- `remain-mark.png`, `remain-logo.png` — used for favicon/apple-touch-icon and homepage hero

All HTML files are standalone with inline `<style>` blocks. No build step. No external CSS or JS dependencies beyond Google Fonts.

## URL routing

Every internal link uses the canonical `/coverages/<slug>` pattern. Vercel rewrites these to the flat `<slug>.html` files via `vercel.json`. Two notes:

- **ILIT special case**: `/coverages/ilit` → `ilit-funding.html` (the slug differs from the filename).
- `cleanUrls: true` is on, so `.html` extensions are hidden in the address bar.

## Deploying to Vercel

1. Push this folder to GitHub.
2. In Vercel, import the GitHub repo. Choose the **Other** framework preset (it's plain HTML).
3. Vercel auto-detects `vercel.json` and applies the routing.
4. First push gives a `*.vercel.app` preview URL.
5. To attach the production domain (`remainlifeinsurance.com`, parked at GoDaddy):
   - In Vercel: Project → Settings → Domains → Add `remainlifeinsurance.com`
   - In GoDaddy DNS: change nameservers to Vercel's, OR add the A/CNAME records Vercel shows you.

## Open items before public launch

These work for an internal preview but should be resolved before publicizing the site:

1. **Email**: `office@remainlifeinsurance.com` is referenced in 60+ places. The mailbox isn't active yet, so `mailto:` links currently bounce. Either set up the inbox or swap to a working address.
2. **CA License #4524855**: confirmed working as-is. Verify whether this is the LLC's organizational license or the principal's individual license; if the LLC has a separate org license, swap.
3. **Open Graph / Twitter card meta tags + a 1200&times;630 OG image**: not added yet. Without these, link previews on iMessage/Slack/Twitter look generic. Easy add when you have the visual.
4. **Canonical URL meta tags**: not added. With `cleanUrls` on, both `/coverages/1035-exchange` and `/1035-exchange` resolve to the same file. Add `<link rel="canonical">` on each page pointing at the `/coverages/<slug>` form to remove ambiguity for search engines.
5. **Sitemap domain**: `sitemap.xml` and `robots.txt` reference `remainlifeinsurance.com`. If the production domain ends up different, update both files.
6. **Page weight**: each spoke page is ~440KB because the Torrey Pine logo is base64-embedded inline. Fine for now, but extracting to a single shared `<img>` reference would cut total bytes substantially.

## Known consistency notes

- `ilit-funding.html` keeps that filename for URL stability; the canonical slug is `/coverages/ilit`. Don't rename the file.
- The dropdown nav, footer grid, and coda all reflect the same 17-coverage taxonomy. Any future coverage additions need to update all three places, plus `sitemap.xml` and `404.html`.
- Homepage hub-and-spoke diagram intentionally shows only 12 of the 17 spokes &mdash; brand statement, not full index.
