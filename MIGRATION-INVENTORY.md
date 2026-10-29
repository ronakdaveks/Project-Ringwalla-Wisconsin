# Ringwala Allergy & Asthma: Migration Inventory

Source: uploaded saveweb2zip export of https://ringwalaallergy.com (WordPress + Elementor).
Target: Webflow site "Ringwala Allergy & Asthma" (`studio-market-c40469`, id `6abb51224a882d7104be4797`, unpublished, no domain).

**Limitation:** the export contains the **homepage only** (plus assets). Inner pages are known from the navigation but their content is not in the export.

## Pages

| Page | URL | In export? |
|---|---|---|
| Home | `/` | Yes |
| About | `/about-ringwala-allergy-and-asthma/` | No |
| Allergy Treatment | `/allergy-treatment/` | No |
| Asthma Treatment | `/asthma-treatment/` | No |
| Contact Us | `/contact-us/` | No |
| Primary Care | `/primary-care/` | No |
| Wisconsin Food Allergy | external: wisconsinfoodallergy.com | n/a (keep as external link) |
| Request an Appointment | `/request-an-appointment/` | No (likely has the Contact Form 7 form) |
| Location: Kenosha / Sturtevant / Franklin / Oshkosh | `/location-kenosha/`, `/location-sturtevant/`, `/location-franklin/`, `/location-oshkosh/` | No |

**Problem on the live homepage:** the CTA and location links (Schedule Your Consultation, Learn More, Book Appointment, 4 Location Details) point to a staging host, `lavender-dog-323741.hostingersite.com`, not the real domain. Fix these during the rebuild.

## SEO (homepage)
- Title: `Home - Ringwala Allergy & Asthma`
- Description: "Ringwala Allergy & Asthma in Kenosha, WI offers expert care for seasonal, food, and year-round allergies, plus asthma treatment. Four locations & telemedicine available. Call 262-657-9390 to reclaim your quality of life."
- Robots: index, follow. Canonical: `https://ringwalaallergy.com/`. OG image: `hero-sec-img.jpg`.
- Most images have **no alt text** (logo, hero, 3 treatment cards); condition images do have alt.

## Homepage sections (in order)
1. **Header:** logo, nav (Home, About, Allergy Treatment, Asthma Treatment, Contact Us, Primary Care, Wisconsin Food Allergy), mobile hamburger.
2. **Hero:** H1 "We Help You Live a Better Life." + intro paragraph + CTA "Schedule Your Consultation". Image: `hero-sec-img.jpg`.
3. **Three feature cards:** Complete Treatment / Allergy Treatments / Asthma Treatments, each with image and "Learn More".
4. **Conditions We Treat** (10 cards, each with image, description, "Book Appointment"): Asthma, Hay Fever (Allergic Rhinitis), Sinus Problems, Food Allergy, Hives, Eczema, Drug Allergy, Insect Venom Allergy, Contact Allergy, Latex Allergy. Rendered as a carousel (Element Pack). **CMS candidate: "Conditions".**
5. **Call banner:** "Call us now for any questions about your allergies or asthma!" with 262-657-9390.
6. **FAQ accordion** (4 items): What is an allergy? / How are allergies treated? / Why have allergy shots when very effective medications are available? / What is an allergist?
7. **Doctor and offices:** Sudip N. Ringwala, D.O. blurb; "four offices in Kenosha, Oshkosh, Franklin, and Sturtevant, WI"; 4 office cards, each with a Google Maps iframe embed and a "Location Details" button. **CMS candidate: "Locations".**
8. **Footer:** Quick Links (repeat of nav), social icons (Facebook, Instagram), copyright "Legally operated under S&A Ringwala S.C.", credit "Designed and Developed by Abstract MediaVerse".
9. **Floating social sidebar** (Fuse Social Floating Sidebar plugin).

## Locations (NAP data)
| Office | Address | Phone |
|---|---|---|
| Kenosha | 4906 39th Ave, Kenosha, WI 53144 | 262-657-9390 |
| Sturtevant | 10180 Washington Ave, Sturtevant, WI 53177 | 262-657-9390 |
| Franklin (Neurosurgery Office) | 10500 W Loomis Rd, Suite 130, Franklin, WI 53132 | 414-267-7534 |
| Oshkosh | 10 E Irving Ave, Oshkosh, WI 54901 | 262-657-9390 |

Social: facebook.com/ringwalaallergy, instagram.com/Ringwalaallergyandasthma

## Assets (in the export, `wp-content/uploads/2025/`)
Logo: `RingwalaLogo.png`, `RAA-300x300.png` / `RAA-150x150.png` (likely favicon/app icon). Hero: `hero-sec-img.jpg`. Cards: `Complete-treatment-new.jpg`, `Allergy-treatment-new.jpg`, `Asthma-treatment-new.jpg`. Conditions (full-size and 300x200 versions): Asthma (png), Hay-fever, Sinus-problem, Food-allergies, Hives, Eczema, Drug-allergy-New-img, Insect-venom-allergy, Contact-allergy, Latex-allergy. Upload the full-size files to Webflow and skip the `-300x200` thumbnails.
Fonts: Roboto, Roboto Slab (Google Fonts). Icons: Font Awesome, Elementor icons (replace with Webflow-native icons or SVGs).

## Plugins and features, and what replaces them in Webflow
| WordPress piece | Webflow replacement |
|---|---|
| Elementor + Hello theme + Header/Footer Elementor | Native Webflow Designer build, shared Navbar/Footer symbols |
| Element Pack carousel | Webflow slider or CMS collection list |
| Essential Addons (accordion) | Native accordion (or a Webflow component) |
| Contact Form 7 | Webflow Forms (field list and email recipients needed from the old form) |
| Jetpack (Forms, PayPal payments, stats.wp.com) | Webflow Forms; check whether the PayPal button is used anywhere; drop WP stats and use GA4 |
| Fuse Social Floating Sidebar | Fixed-position social links element |
| Google Maps iframes | Webflow Embed or Google Maps element |
| Yoast-style SEO meta (robots, OG, canonical) | Webflow page SEO settings |

## Gaps and risks
1. **Only the homepage was exported.** For the other 9 or more pages, I need either the page content (each page saved, or pasted) or network access to the live site. A new session with `ringwalaallergy.com` allowed would let me crawl everything.
2. No tracking IDs (GA, GTM, Pixel) found in the saved HTML. Confirm whether the live site has any.
3. The appointment form's fields and recipients are unknown until `/request-an-appointment/` is captured.
4. The homepage says "telemedicine available" in the meta description only; confirm where else it is mentioned.
5. This is a medical practice. Check any HIPAA-sensitive form use (don't collect health details in plain Webflow forms without a compliant setup).
6. Redirects: if Webflow URLs change from the WordPress slugs, add 301s. Keeping the same slugs avoids this.

## Proposed Webflow structure
- Pages: Home, About, Allergy Treatment, Asthma Treatment, Primary Care, Contact Us, Request an Appointment.
- CMS: **Conditions** (name, slug, symptoms, image) and **Locations** (name, address, phone, map embed, slug) feeding the home page and `/location-*` template pages.
- Shared: navbar, footer, CTA banner, FAQ.
