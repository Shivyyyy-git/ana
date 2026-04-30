# Personal site — Anastasia Tahou

Plain HTML + CSS, no build step. Open `index.html` in a browser, or serve the
folder over HTTP for clean URLs.

## Local preview

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

## Layout

```
index.html                       home
resume.html                      résumé (HTML)
anastasia-tahou-resume.pdf       résumé download (LinkedIn-exported PDF)
anastasia-tahou-resume.docx      résumé source (Word)
about.html                       long-form bio
404.html                         not-found page
projects/
  index.html                     project list
  _template.html                 copy to create a new project page
  example-project.html           delete or replace
writing/
  index.html                     post list
  _template.html                 copy to create a new post
  hello-world.html               delete or replace
assets/
  css/style.css                  single shared stylesheet
  favicon.svg
  img/                           put images here
```

## Adding a project

1. Copy `projects/_template.html` to `projects/<slug>.html`.
2. Edit the title, description, and body.
3. Add a card to `projects/index.html` linking to the new file.

## Adding a post

1. Copy `writing/_template.html` to `writing/<slug>.html`.
2. Edit the title, date, and body.
3. Add an `<li>` at the **top** of the list in `writing/index.html`.

## Updating the résumé

The canonical source is `anastasia-tahou-resume.docx` (Word). When it changes:

1. Replace the .docx in the repo root.
2. Re-export to PDF (LinkedIn export, Word "Save as PDF", or any tool) and
   replace `anastasia-tahou-resume.pdf`.
3. Update the corresponding sections in `resume.html` so the on-page version
   matches the downloads.

To extract the .docx text on a machine without `pandoc`:

```sh
unzip -p anastasia-tahou-resume.docx word/document.xml \
  | python3 -c "import sys,xml.etree.ElementTree as ET; \
    ns={'w':'http://schemas.openxmlformats.org/wordprocessingml/2006/main'}; \
    r=ET.fromstring(sys.stdin.read()); \
    [print(''.join(t.text or '' for t in p.iter('{%s}t'%ns['w'])).strip()) \
     for p in r.iter('{%s}p'%ns['w'])]"
```

Or with `pandoc` (cleaner): `pandoc anastasia-tahou-resume.docx -o resume.html`.

## Customising the look

All styles live in `assets/css/style.css`. The palette is defined as CSS
custom properties at the top of the file:

```css
--bg:     #fafaf7;   /* page background */
--ink:    #1a1a1a;   /* body text */
--muted:  #6b6b6b;   /* dates, secondary text */
--accent: #d4502e;   /* links, current-page indicator */
--rule:   #e6e3dc;   /* hairlines */
```

Change those five values to re-skin the site.

## Hosting

The site is pure static files, so any static host works:

- **GitHub Pages** — enable Pages on the branch in repo settings.
- **Vercel / Netlify** — connect the repo, no build command, output dir `.`.
- **S3 / Cloudflare Pages / anywhere else** — upload the folder.

## Print

`resume.html` has a print stylesheet that hides the nav/footer and tightens
spacing. `Cmd/Ctrl + P` produces a clean one-page PDF.
