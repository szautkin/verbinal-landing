# Translating verbinal.com (English + French)

The site is a static, no-build set of HTML pages. It is bilingual:

- **English** lives at the site root: `/`, `/blog`, `/blog/<slug>`, `/verbinal-thought`, …
- **French** mirrors it under `/fr/`: `/fr/`, `/fr/blog`, `/fr/blog/<slug>`, `/fr/verbinal-thought`, …

Every page ships as an **EN (root) + FR (`/fr/`) pair**. There is no build step or framework — the two
copies are real files kept in sync by hand.

## The convention

When you add or change a page:

1. **Add/edit both copies.** Shared chrome (header, footer, nav, announcement banners) is duplicated, so a
   structural change must be mirrored in the EN file and its `/fr/` counterpart.
2. **Language switcher** — each page carries an `EN | FR` switch in the header and footer, wrapped in
   `<!--LANGSWITCH-->…<!--/LANGSWITCH-->` (and `-FOOTER`) sentinels. The current language has
   `aria-current="page"`; the other links to the counterpart URL.
3. **`hreflang`** — every page's `<head>` lists reciprocal alternates:
   `<link rel="alternate" hreflang="en|fr|x-default" …>` (x-default → the English URL). Self-`canonical`
   points at the page's own language URL.
4. **Assets are absolute** (`/assets/…`, `/style.css`) so they resolve from any depth, including `/fr/…`.
5. **`sitemap.xml`** lists both languages with hreflang pairs — add new pages there too.

## French style

- Canadian French (fr-CA). Terminology matches the **macOS app's own French** — the source of truth is the
  app String Catalog: `~/projects/canfar-mac/Verbinal/Resources/Localizable.xcstrings`. Examples:
  Settings → Réglages, Storage → Stockage, Notebook → Calepin, AI Guide → Guide IA,
  Keychain → trousseau macOS, sandbox → bac à sable.
- Keep brand/tech/tool names untranslated (Verbinal, CANFAR, CADC, Skaha, Claude Desktop/Code, the
  `<code>` tool names, license names, version numbers).
- Typography: guillemets « » with non-breaking spaces, and a non-breaking space before `: ; ! ?`.
- The Verbinal Thought legal pages (`/fr/verbinal-thought/privacy`, `/support`) carry a note that the
  **English version prevails** in case of divergence, linking to the English page.

## Migration trigger

This hand-maintained mirror is fine at the current page count. **If the site grows past ~10–12 pages or a
third language is added, move to a static-site generator** (e.g. Eleventy) with one layout + per-language
data files, so shared chrome stops being duplicated.
