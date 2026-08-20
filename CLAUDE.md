# Count the Cost

Pricing and quoting calculators for trades and service businesses. Sold as
downloads on Etsy under the Count the Cost brand.

Tagline: "Know your numbers before you build."

## Repo shape

One folder per tool under `tools/`. Each tool is a single HTML file named the
way a buyer should see it on their desktop, because that filename is what they
download.

```
tools/cleaning-price-quote-calculator/cleaning-price-quote-calculator.html
```

Listing copy, screenshots, and pricing notes go in the tool's folder next to
the HTML.

## The reference build

`tools/cleaning-price-quote-calculator/` is the reference. Start every new
calculator by copying it, then strip out the cleaning-specific parts. Do not
re-derive the brand tokens, the layout, or the quote sheet from scratch.

What carries over verbatim:

- The `:root` token block. Core four are ink `#111318`, blue `#2864FF`,
  white `#F7F8FA`, slate `#667085`. Archivo Black for the lockup, Archivo for
  display, Inter for body.
- The tally-mark SVG lockup and the dark sticky brandbar.
- The sticky result bar: big recommended price, margin chip, then cost, profit,
  and per-hour stat tiles.
- The gear panel for assumptions the owner can edit and save.
- The print-to-PDF customer quote, which shows the buyer's own branding and
  none of the internal cost math.

## Rules

- One file per tool. Markup, styles, and script all inline.
- Works offline from `file://`. Google Fonts is the only external request, and
  every stack falls back to system fonts when it fails.
- Mobile first. Most people open these on a phone standing in someone's kitchen.
- No backend, no accounts, no analytics. State lives in `localStorage` only.
- Vanilla JS. No jQuery, no React, no build tooling.

The full standards live in the `felipe-html-conventions` and
`etsy-html-products` skills. Follow those. This file covers what is specific
to Count the Cost.

## Conventions the reference build sets

- `localStorage` keys are `<tool>_data_v1` and `<tool>_seen_v1`. Bump the
  version suffix when the saved shape changes so old data cannot break a load.
- First open loads a realistic sample job, so the tool shows working numbers
  instead of zeros. A dismissible "Start here" banner explains it.
- Every user-facing number runs through `pos()` so a blank or negative input
  can never poison the math.
- Anything the customer sees goes through `escapeHtml()`.
- Warning notes are text a person would say out loud. "Thin margin. Most
  cleaners aim for 30% or more." Not "Warning: margin below threshold."

## Pricing engine

Cost-plus, gross up for the card fee, then floor at the minimum:

```
serviceCost  = labor + supplies + travel + overhead
servicePrice = serviceCost / (1 - margin - feeShare)
listPrice    = servicePrice + add-on charges
net          = max(listPrice - discount, minimum)
total        = net + tax
```

Tax passes through and is never counted as profit. The processing fee is
charged on the taxed total and comes out of the owner's pocket, so it is a
real cost against margin. Margin is capped at 95% or the price runs away.

## Preview

```
python3 -m http.server 8000
```

Or open the HTML file directly and refresh after each change.

## Iterating

Commit every version that works. Small commits, plain messages that say what
changed for the user, like "add markup slider" or "fix tax rounding on
multi-line quotes". Git history is the version history, so no
`calculator-v4-final.html` files.

Big or risky changes go on a branch off `main`.

## Before shipping a change

Run the `build-critique-loop` skill. Then check by hand:

- Opens from `file://` with no console errors
- Works at 375px wide
- Numbers still correct with 0, blank, and huge inputs
- Print preview of the customer quote still fits one page
- Existing saved data from the previous version still loads

## Tools

| Tool | Status |
| --- | --- |
| Cleaning Price & Quote Calculator | Selling on Etsy |
| Contractor Quote Calculator | In progress, v1.1 |
