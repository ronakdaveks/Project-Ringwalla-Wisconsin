# Webflow build: handoff notes

Target site: **Ringwala Allergy & Asthma** (Webflow site id `6abb51224a882d7104be4797`, shortName `studio-market-c40469`). Not published, no custom domain.
Source site: https://ringwalaallergy.com (WordPress + Elementor). Page inventory: `MIGRATION-INVENTORY.md`.

## Done (all unpublished drafts of work, nothing live)
| Page | Webflow page id | Slug |
|---|---|---|
| Home | `6abb51234a882d7104be47a5` | `/` |
| Contact Us | `6ae3792993af9ca9367a5b97` | `/contact-us` |
| Request an Appointment | `6ae3792a93af9ca9367a5c1f` | `/request-an-appointment` |
| Kenosha | `6ae3792b9cc5f1b3ccf030e2` | `/location-kenosha` |
| Sturtevant | `6ae3792bc9be2a32b7882548` | `/location-sturtevant` |
| Franklin | `6ae3792cfa001e13dcd44826` | `/location-franklin` |
| Oshkosh | `6ae3792dfa001e13dcd448cd` | `/location-oshkosh` |

Shared components (edited, used on every page): Navigation `6abb51444c722a6b51c7faba`, Footer `6abb51444c722a6b51c7fabb`.
Leftover Studio Market template pages (Work, Services, Process, Case Studies, Style guide) are set to **draft**. The API cannot delete pages; delete them in the Designer if wanted.

## Still to build
About (`/about-ringwala-allergy-and-asthma`), Allergy Treatment (`/allergy-treatment`), Asthma Treatment (`/asthma-treatment`), Primary Care (`/primary-care`). Nav, footer and homepage buttons already link to these slugs. Crawl them from the live site once `ringwalaallergy.com` and `www.ringwalaallergy.com` are allowed in the environment's network settings (the previous session was blocked).

## Open items
- Appointment form: set the notification recipient in Webflow (Site settings, Forms). Not settable via API. No success/error message configured.
- Opening hours are not on the location pages (not in the source homepage).
- Fonts Roboto (400/500/700) and Roboto Slab (400/700) are uploaded as custom fonts, but the page builder still warned "font unavailable" on some inserts. Verify rendering in a preview.
- Nothing has been previewed in a browser or the Designer yet (mobile menu, map iframes, spacing).
- Old agency credit "Designed and Developed by Abstract MediaVerse" was left out of the footer.
- Original site also has: Wisconsin Food Allergy external link (kept), Facebook/Instagram (kept as text links).

## Conventions and tooling notes
- All custom classes use the `rw-` prefix (e.g. `rw-hero`, `rw-section`, `rw-btn`, `rw-container`, `rw-loc-*`, `rw-office*`, `rw-faq*`). Reuse them; do not recreate.
- Palette: navy `#12324a`, teal `#0f7080`, tint `#eef7f8`, border `#dcebee`, body text `#3d5566`.
- To add a page: `create_page` with `duplicateOf` the Home page id (inherits nav/footer), remove the copied `rw-*` sections, insert new ones before the Footer instance `6abb515a4c722a6b51c7fe78` with `data_whtml_builder` (position `before`).
- `data_whtml_builder` only accepts breakpoints 991 / 767 / 479 px. It drops `<iframe>` (add with `data_element_builder`: type `DOM`, `dom_tag: iframe`) and inserts images without an asset (attach afterwards with `set_image_asset`).
- Bulk page draft update did not apply; use `update_page_settings` per page.
- Uploaded image assets (alt text already set), by id: logo `6ae3766ea9eeb72d2927ebdf`, hero `6ae37690151cbe4c560294b9`, Complete/Allergy/Asthma treatment `6ae376912f228b7b0ee44fd7` / `6ae376912f228b7b0ee44fea` / `6ae3769190ff9ff47516ddc5`, conditions: Asthma `6ae376915c3a3646ddee8c90`, Hay fever `6ae376912f228b7b0ee4503a`, Sinus `6ae37691707e4674532d511c`, Food `6ae376917d5c395942dae7d8`, Hives `6ae3769290ff9ff47516de27`, Eczema `6ae376921ac3cfacf9999c49`, Drug `6ae376931ac3cfacf9999c6b`, Insect `6ae37693b5c4e4ac022dede1`, Contact `6ae37693d2c5d57b1aeb0a31`, Latex `6ae376935e27054d9cb91a8a`.
- Presigned S3 uploads (assets and fonts) work from this environment via `curl -F`; npm (`@fontsource/*`) is reachable for font files.
