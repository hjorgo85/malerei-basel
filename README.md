# Malerei Basel — Rank-and-Rent Website

Static HTML/CSS site (no build tooling, no backend) for a house-painting "rank and rent" project targeting Basel-Stadt and the surrounding Basel-Landschaft municipalities.

## Business model: real painter to visitors, referral network on paper

Publicly, Malerei Basel presents itself as a real Malerbetrieb — first-person copy ("Malerei Basel übernimmt...", "wir sind Ihr Ansprechpartner"), `LocalBusiness`/`HomeAndConstructionBusiness` JSON-LD, real contact details. Underneath, the legal pages quietly keep a different structure:

- **Legal pages** (`impressum.html`, `agb.html`, `datenschutz.html`) disclose that Malerei Basel is actually a **Vermittlungsportal** operated by a network entity (placeholder: "Regio Handwerk Netzwerk GmbH"), that the contract for any painting work forms between the customer and an independent partner firm (Partnerbetrieb), and that contact/project data is passed to partner firms for quoting. These pages are `noindex` and linked only from the footer.
- Everywhere else — hero copy, service pages, town pages, JSON-LD — reads as if Malerei Basel itself is the painter. This is deliberate: it keeps the site converting/ranking like a real local business while the fine print protects against liability for work it doesn't itself perform.

**Do not blur this line accidentally:** new marketing copy should stay first-person "we are the painters," and the referral-network language ("vermitteln", "Partnerbetrieb", "Vermittlungsportal") should only ever appear in the three legal pages.

## Structure

- `index.html`, `leistungen.html`, `galerie.html`, `ueber-uns.html`, `kontakt.html` — core pages
- `innenanstrich.html`, `fassadenanstrich.html`, `gipser-spachtelarbeiten.html`, `umzugsmalerei.html` — dedicated service pages (linked from `leistungen.html` and the footer); each has a 3-question FAQ (`.faq-list`, native `<details>/<summary>`, no JS) plus `Service` + `FAQPage` JSON-LD. Other services (Tapezieren, Lackierarbeiten, etc.) stay as plain cards on `leistungen.html` only — they had no measurable search volume in keyword research, so no dedicated page was built (avoids thin/doorway pages).
- `blog.html` + `blog-*.html` — a small blog (3 posts) targeting informational keyword opportunities, each with `Article` JSON-LD
- `maler-*.html` — 11 town landing pages (Riehen, Bettingen, Allschwil, Binningen, Muttenz, Pratteln, Reinach, Birsfelden, Oberwil, Münchenstein, Arlesheim)
- `impressum.html`, `agb.html`, `datenschutz.html` — legal pages (network/referral disclosures, `noindex`), linked from every page's footer
- `css/style.css` — single shared stylesheet (also holds breadcrumb, FAQ accordion, and blog card styles)
- `js/main.js` — mobile nav toggle only
- `robots.txt`, `sitemap.xml` — SEO (legal pages are `noindex` and intentionally excluded from the sitemap)
- `favicon.svg` — site icon

## Contact details (real, not placeholder)

The site's displayed NAP is real — it belongs to **Smart Maler & More GmbH** (https://www.smartmaler.ch/), the friends' business this site is intended to be rented to once it ranks:

- Address: St. Galler-Ring 156, 4054 Basel
- Phone: +41 78 683 60 26 (a second number, +41 76 803 30 24, exists but isn't used on the site)
- Email: info@smartmaler.ch

The site's own brand/display name stays "Malerei Basel" (that's the domain and the whole point of the rank-and-rent play) — only the underlying contact info is Smart Maler & More GmbH's.

**Still placeholder:** the network-operator entity named in the legal pages ("Regio Handwerk Netzwerk GmbH", UID `CHE-000.000.000`, managing director) — marked `PLACEHOLDER NETZWERK-BETREIBERIN` / `PLACEHOLDER GESCHÄFTSFÜHRUNG` in `impressum.html`. That's a separate legal-entity question from the public contact info and hasn't been resolved yet.

Since the site's address/phone now match Smart Maler & More GmbH's own already-live listing exactly, don't set up a separate Google Business Profile for "Malerei Basel" at this address — Google will very likely flag it as a duplicate listing at the same location.

## Deploying (manual FTP upload)

1. Build the deploy zip (from the project root, PowerShell):
   ```
   Compress-Archive -Path index.html,leistungen.html,galerie.html,ueber-uns.html,kontakt.html,impressum.html,agb.html,datenschutz.html,innenanstrich.html,fassadenanstrich.html,gipser-spachtelarbeiten.html,umzugsmalerei.html,blog.html,blog-*.html,maler-*.html,css,js,images,favicon.svg,robots.txt,sitemap.xml -DestinationPath dist\malerei-basel-deploy.zip -Force
   ```
2. Extract the zip to a throwaway folder and confirm `index.html` is at the top level (no wrapping folder).
3. Upload the contents via FTP into NameHero's `public_html` (or the target domain's document root).
