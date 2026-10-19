# Personal website

The source of Eduard Dehelean's portfolio: a handful of hand-written HTML pages, one stylesheet and a font. No framework, no build step and no JavaScript beyond a one-line prerender hint.

## Layout

```
index.html              homepage with the project list
dox/ pocar/ ...         one page per featured project
css/style.css           the only stylesheet
fonts/                  EB Garamond, cut down to the letters the site uses (SIL Open Font License, see OFL.txt)
assets/                 resume
favicon.svg, 404.html
```

## Run it locally

```bash
python -m http.server 8000
```

Then open http://localhost:8000.

## Why it is fast

- Each page is a few kilobytes of HTML, and the stylesheet is shared and cached.
- Text appears straight away in Georgia while EB Garamond loads, then switches over (`font-display: swap`).
- The font is self-hosted and subset to Latin plus the Romanian letters, about 19 KB per style. The Romanian file only downloads on pages that use those letters.
- Links between pages are prerendered on hover in Chrome and Edge, and pages fade into each other instead of flashing white.

## Changing the font subset

The font files come from the `@fontsource/eb-garamond` package and were cut down with fontTools:

```bash
pyftsubset eb-garamond-latin-400-normal.woff2 --unicodes="U+0020-007E,U+00A0-00FF,U+2013-2014,U+2018-201A,U+201C-201E,U+2022,U+2026,U+2032-2033,U+20AC,U+2122,U+2190-2193" --layout-features="kern,liga,onum,lnum" --flavor=woff2 --desubroutinize --output-file=fonts/eb-garamond-400-normal.woff2
```

Use the same ranges as the `unicode-range` lines in `css/style.css`.
