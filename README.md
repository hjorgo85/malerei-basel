# Malerei Basel — Rank-and-Rent Website

Static HTML/CSS site (no build tooling, no backend) for a house-painting "rank and rent" project targeting Basel-Stadt and the surrounding Basel-Landschaft municipalities.

## Business model: referral network, not a Malerbetrieb

Malerei Basel presents itself as a **Vermittlungsportal** — a lead-generation network that connects visitors to independent local partner painting firms (Partnerbetriebe), rather than as a painting company that performs the work itself. This is deliberate and runs through the whole site:

- **Legal pages** (`impressum.html`, `agb.html`, `datenschutz.html`) spell out the model: the operator is a network entity (placeholder: "Regio Handwerk Netzwerk GmbH", which also runs other regional trade portals), the contract for any painting work forms between the customer and the matched Partnerbetrieb, and contact/project data is passed to partner firms for quoting.
- **JSON-LD** on every page uses a plain `Organization` type with a `ContactPoint` and a `"Vermittlungsportal für Malerarbeiten..."` description — not `LocalBusiness`/`HomeAndConstructionBusiness` with a `priceRange`, which would claim the site itself is the trade business.
- **Marketing copy** on the core and town pages says "Malerei Basel vermittelt Ihnen einen Partnerbetrieb für ..." rather than "Malerei Basel übernimmt ...". SEO-facing elements (titles, H1s, meta keywords targeting "maler [ort]") are unaffected — a search for "maler riehen" is served equally well by a portal that connects the visitor to a maler in Riehen.

Keep new copy and structured data consistent with this framing — don't reintroduce "we perform the work ourselves" language without also updating the legal pages.

## Structure

- `index.html`, `leistungen.html`, `galerie.html`, `ueber-uns.html`, `kontakt.html` — core pages
- `maler-*.html` — 11 town landing pages (Riehen, Bettingen, Allschwil, Binningen, Muttenz, Pratteln, Reinach, Birsfelden, Oberwil, Münchenstein, Arlesheim)
- `impressum.html`, `agb.html`, `datenschutz.html` — legal pages (network/referral disclosures, `noindex`), linked from every page's footer
- `css/style.css` — single shared stylesheet
- `js/main.js` — mobile nav toggle only
- `robots.txt`, `sitemap.xml` — SEO (legal pages are `noindex` and intentionally excluded from the sitemap)
- `favicon.svg` — site icon

## Placeholder content

All contact details (phone `+41 61 000 00 00`, email `info@malerei-basel.ch`, address `Musterstrasse 1, 4051 Basel`) are PLACEHOLDERS marked with HTML comments (`PLACEHOLDER NAP`). Find-and-replace these consistently across all files before the site goes live / is rented to a real business. They appear in: every page's header nav (`nav-call`), footer NAP block, `kontakt.html`, and each page's JSON-LD `Organization` schema.

The legal pages also carry a separate placeholder for the **network operator entity** ("Regio Handwerk Netzwerk GmbH", UID `CHE-000.000.000`, managing director) — marked `PLACEHOLDER NETZWERK-BETREIBERIN` in `impressum.html` and `datenschutz.html`. Replace this with the real operating company's details before launch.

## Deploying (manual FTP upload)

1. Build the deploy zip (from the project root, PowerShell):
   ```
   Compress-Archive -Path index.html,leistungen.html,galerie.html,ueber-uns.html,kontakt.html,impressum.html,agb.html,datenschutz.html,maler-*.html,css,js,images,favicon.svg,robots.txt,sitemap.xml -DestinationPath dist\malerei-basel-deploy.zip -Force
   ```
2. Extract the zip to a throwaway folder and confirm `index.html` is at the top level (no wrapping folder).
3. Upload the contents via FTP into NameHero's `public_html` (or the target domain's document root).
