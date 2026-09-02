# Malerei Basel — Rank-and-Rent Website

Static HTML/CSS site (no build tooling, no backend) for a house-painting "rank and rent" project targeting Basel-Stadt and the surrounding Basel-Landschaft municipalities.

## Structure

- `index.html`, `leistungen.html`, `galerie.html`, `ueber-uns.html`, `kontakt.html` — core pages
- `maler-*.html` — 11 town landing pages (Riehen, Bettingen, Allschwil, Binningen, Muttenz, Pratteln, Reinach, Birsfelden, Oberwil, Münchenstein, Arlesheim)
- `css/style.css` — single shared stylesheet
- `js/main.js` — mobile nav toggle only
- `robots.txt`, `sitemap.xml` — SEO
- `favicon.svg` — site icon

## Placeholder content

All contact details (phone `+41 61 000 00 00`, email `info@malerei-basel.ch`, address `Musterstrasse 1, 4051 Basel`) are PLACEHOLDERS marked with HTML comments (`PLACEHOLDER NAP`). Find-and-replace these consistently across all files before the site goes live / is rented to a real business. They appear in: every page's header nav (`nav-call`), footer NAP block, `kontakt.html`, and each page's JSON-LD `LocalBusiness` schema.

## Deploying (manual FTP upload)

1. Build the deploy zip (from the project root, PowerShell):
   ```
   Compress-Archive -Path index.html,leistungen.html,galerie.html,ueber-uns.html,kontakt.html,maler-*.html,css,js,images,favicon.svg,robots.txt,sitemap.xml -DestinationPath dist\malerei-basel-deploy.zip -Force
   ```
2. Extract the zip to a throwaway folder and confirm `index.html` is at the top level (no wrapping folder).
3. Upload the contents via FTP into NameHero's `public_html` (or the target domain's document root).
