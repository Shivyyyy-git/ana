# Anastasia Tahou — personal site

Single-page personal website. Plain HTML + CSS, no build step.

## Local preview

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

Or open `index.html` directly in a browser.

## Layout

```
index.html                       the site (one page, all sections)
404.html                         not-found page
anastasia-tahou-resume.pdf       résumé download (PDF)
anastasia-tahou-resume.docx      résumé source (Word)
assets/
  css/style.css                  single shared stylesheet
  favicon.svg
```

## Editing the content

All copy lives in `index.html`. Sections are clearly marked:

- `#home` — hero with name, role, location, and CTA buttons
- `#about` — bio paragraphs and quick-stat cards
- `#experience` — list of `.role-card` blocks (one per role)
- `#education` — `.edu-card` blocks
- `#skills` — `.chip` lists and `.skill-list` lists
- `#contact` — clickable contact cards

To add a new role, copy a `<article class="role-card">` block and edit the
fields. Same pattern for education.

## Updating the résumé download

When the résumé changes:

1. Replace `anastasia-tahou-resume.docx` (the Word source).
2. Re-export to PDF and replace `anastasia-tahou-resume.pdf`.
3. Update the corresponding role/education/skills sections in `index.html`
   so the on-page version matches the download.

## Customising the look

All styles are in `assets/css/style.css`. The palette is in CSS custom
properties at the top of the file:

```css
--bg:        #ffffff;     /* page background */
--bg-soft:   #f8fafc;     /* alternating section background */
--ink:       #0f172a;     /* primary text */
--muted:     #64748b;     /* secondary text */
--accent:    #4f46e5;     /* buttons, links, highlights */
--border:    #e2e8f0;     /* card borders */
```

Change those six values to re-skin the site.

## Hosting

Pure static files — any static host works:

- **GitHub Pages** — Settings → Pages → deploy from this branch.
- **Vercel / Netlify / Cloudflare Pages** — connect the repo, no build
  command, output dir `.`.

## Print

The print stylesheet hides the nav, hero buttons, avatar, and footer so
`Cmd/Ctrl + P` produces a clean text-only version of the résumé content.
