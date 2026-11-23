# Simplifex website – setup guide

Upload **all files in this folder** to your GitHub repository (replace the old `index.html`). Keep `CNAME`.
Do the 3 steps below once.

---

## Step 1 – Connect the contact form to Google Sheets (about 5 minutes)

1. Go to <https://sheets.new> and name the sheet **Simplifex Website Enquiries**.
2. In the sheet: **Extensions → Apps Script**.
3. Delete the sample code, paste everything from **`google-apps-script.gs`**, and click **Save** (disk icon).
4. Click **Deploy → New deployment**.
   - Click the gear icon next to "Select type" → **Web app**
   - Execute as: **Me**
   - Who has access: **Anyone** *(required, or the website can't send data)*
   - Click **Deploy** → **Authorize access** → choose your Google account.
     If you see "Google hasn't verified this app": click **Advanced → Go to (project name) (unsafe)** → **Allow**. This is normal for your own script.
5. Copy the **Web app URL**. It looks like `https://script.google.com/macros/s/AKfy.../exec`.
6. Open `index.html`, search for `PASTE_YOUR_APPS_SCRIPT_URL_HERE`, and replace it with your URL (keep the quotes):
   ```js
   var SX_FORM_ENDPOINT = "https://script.google.com/macros/s/AKfy.../exec";
   ```
7. Upload `index.html` again, open your site, and send a test enquiry. A new row appears in the **Enquiries** tab and you get an email alert.

**Notes**
- Email alerts go to `contact@simplifex.co.in`. To change or turn them off, edit `NOTIFY_EMAIL` at the top of the script.
- **If you edit the script later**, go to **Deploy → Manage deployments → ✏️ Edit → Version: New version → Deploy**. The URL stays the same. Saving alone does **not** update the live form.
- Spam protection is built in: a hidden "honeypot" field plus a minimum time-to-submit.
- Use the **Status** column (New / Contacted / Won / Lost) to track leads.

---

## Step 2 – Google Search Console (get indexed)

1. Go to <https://search.google.com/search-console> → **Add property** → **Domain** → `simplifex.co.in`.
2. Verify by adding the **TXT record** Google gives you at your domain registrar (DNS settings). This is the recommended method.
   *(Or choose "URL prefix" → "HTML tag" and paste the `<meta name="google-site-verification" …>` tag into `index.html`, where the comment marks the spot.)*
3. **Sitemaps** → enter `sitemap.xml` → **Submit**.
4. **URL Inspection** → enter `https://simplifex.co.in/` → **Request indexing**.
5. Check back in a few days: **Pages** shows whether the page is indexed.

Also do this:
- **GitHub Pages → Settings → Pages → tick "Enforce HTTPS".**
- Make sure `www.simplifex.co.in` redirects to `simplifex.co.in` (GitHub does this automatically if both DNS records are set up).

---

## Step 3 – Google Business Profile (biggest win for local searches)

Searches like "ERP software company Perumbavoor" or "e-commerce developer Ernakulam" are mainly won through the map results.

1. Go to <https://business.google.com> → add **Simplifex**.
2. Category: **Software company** (add "Website designer" / "E-commerce service" as secondary).
3. Use the same name, phone (+91 85909 96674) and website as on the site. Matching details help Google trust you.
4. Add your logo, office photos, and a short description. Ask happy clients for reviews.

---

## What was changed for SEO

| Before | After |
|---|---|
| Page was a bundled file. Google saw only "Loading… Unpacking…" | Plain HTML with all text visible to Google instantly. No JavaScript needed to read it |
| Title: "Simplifex home page" | "Custom ERP & E-commerce Development in Kerala \| Simplifex" |
| No meta description | Keyword-rich description (≈150 characters) |
| No structured data | Schema.org JSON-LD: Organization / ProfessionalService (location, phone, email, services), WebSite and FAQPage |
| No social preview | Open Graph + Twitter cards with a 1200×630 share image (`og-image.jpg`) |
| No favicon | Favicon, Apple touch icon, web manifest |
| No robots.txt / sitemap | `robots.txt` + `sitemap.xml` |
| ~490 KB single file, fonts and React bundled inside | ~60 KB HTML + 24 KB WebP logo. No React, much faster load (Core Web Vitals) |
| Location only as "Perumbavoor" | "Perumbavoor, Ernakulam, Kerala" in the hero text, contact section and footer |
| No FAQ | New FAQ section (6 Qs) that adds useful, searchable content |
| Contact form did nothing | Working form → Google Sheet + email alert, with validation and spam protection |
| Email and phone as plain text | Clickable `mailto:` and `tel:` links |

## Next steps that improve ranking further (optional)

- **Add pages per service** (e.g. `/erp-software-kerala/`, `/ecommerce-development-kerala/`, `/manufacturing-erp/`). One page can only rank well for a few keywords.
- **Add case studies or client logos** with real results. These build trust for both Google and visitors.
- **Get listed** on directories (JustDial, IndiaMART, Clutch, GoodFirms) with the same name, phone and address.
- **Add Google Analytics 4** if you want to track visitors. The form already sends a `generate_lead` event when gtag is present.
- When you add pages, list them in `sitemap.xml` and update `<lastmod>`.
