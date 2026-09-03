# Freedom Date

A one-page retirement calculator that answers a single question: **what year can you stop working, and how much will you have when you do?**

Live: **https://dmarkel.github.io/retirementcalculator/**

Drag any number in the sentence, or type it. Everything on the page — the year, the lifetime chart, every panel — recomputes as you move.

## What it does

- **Finds the date, it doesn't assume one.** For every candidate retirement age it runs the money year by year to the end of the plan. The freedom date is the earliest age where the money survives — not a 25× rule of thumb.
- **Keeps compounding after you stop.** The portfolio earns its return every year of retirement too. Only what you spend leaves the account.
- **Works in today's dollars.** Returns are discounted by inflation, so a dollar on the chart always buys what a dollar buys now. A toggle switches everything to future dollars.
- **Shows what actually moves the date.** One change at a time — savings rate, spending, returns, inflation, starting balance — and how many years each one shifts things.
- **Doesn't hide a bad market.** Four return scenarios on one shared scale, with the age the money runs dry if it does.

## Optional: accounts and taxes

Off by default. Turn on **Split my savings into accounts** and the model gets more honest:

| | |
|---|---|
| **Brokerage & cash** | reachable at any age, no tax modelled |
| **401(k) / traditional IRA** | withdrawals grossed up for an effective tax rate; 10% penalty before 59½ |
| **Roth** | comes out clean |

Withdrawals sequence brokerage → 401(k) → Roth. Required minimum distributions start at **73 or 75** depending on birth year (SECURE 2.0), and anything an RMD forces out that you don't spend is reinvested in the brokerage account. Contributions land in the same proportions as the current balances.

This is what surfaces the **bridge problem**: retire at 52 and you need nine years of spending in the brokerage account before the retirement accounts open.

## What it ignores

Fees, healthcare before Medicare, home equity, state tax, capital-gains tax on the brokerage account, sequence-of-returns risk, and the Roth ladders and 72(t) withdrawals that can sidestep the early-withdrawal penalty. Returns are a steady real rate, which no real market has ever delivered.

**This is a model, not advice.**

## Running it

One file, no build, no dependencies.

```bash
python3 -m http.server 8000
```

Then open http://localhost:8000.

## Sharing a plan

Every input lives in the URL fragment, so a link carries the whole plan. "Copy my plan link" in the footer puts it on your clipboard.

"Reset the numbers" — next to the sentence — puts every input back to the example and clears the link. It greys out when you are already at the defaults.

## Design notes

- Type: Bodoni Moda (display), Archivo (text), IBM Plex Mono (data).
- Chart palettes were validated for colour-vision deficiency separation and contrast against both light and dark surfaces before being used.
- Light and dark are both selected palettes, not an automatic inversion.
- Respects `prefers-reduced-motion`; every control is keyboard-reachable; the full year-by-year schedule is available as a table.

## Licence

MIT
