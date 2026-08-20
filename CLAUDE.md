# Count the Cost — Contractor Quote Calculator

Single-file HTML tool. Contractors enter job costs and get a quote they can
actually charge.

## What this repo is

One tool, one file. `index.html` holds the markup, styles, and script. No
build step, no npm, no framework. A buyer downloads the file, double-clicks
it, and it works with no internet connection.

## Rules

- Everything stays in `index.html`. No external CSS, JS, fonts, or CDN links.
- It has to work offline, opened straight from the filesystem via `file://`.
- Mobile first. Most people open these on a phone.
- No backend, no accounts, no analytics. State lives in `localStorage` only.
- Vanilla JS. No jQuery, no React, no build tooling.

The full standards live in the `felipe-html-conventions` and
`etsy-html-products` skills. Follow those. This file only covers what is
specific to Count the Cost.

## Preview

```
python3 -m http.server 8000
```

Then open http://localhost:8000. Or just open `index.html` in the browser and
hit refresh after each change.

## Iterating

Commit every version that works. Small commits, plain messages that say what
changed for the user, like "add markup slider" or "fix tax rounding on
multi-line quotes". The git history is the version history, so no
`calculator-v4-final.html` files.

Big or risky changes go on a branch off `main`.

## Before shipping a change

Run the `build-critique-loop` skill. Then check by hand:

- Opens from `file://` with no console errors
- Works at 375px wide
- Numbers still correct with 0, blank, and huge inputs
- Print or PDF output still looks right, if the tool has one

## TODO

Fill in once the current build lands: the actual pricing inputs, the markup
and overhead math, and where the numbers came from.
