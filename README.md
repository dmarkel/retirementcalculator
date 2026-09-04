# Freedom Date

A one-page retirement calculator that answers a single question: **what year can you stop working, and how much will you have when you do?**

Live: **https://dmarkel.github.io/retirementcalculator/**

Drag any number in the sentence, or type it. Everything on the page — the year, the lifetime chart, every panel — recomputes as you move.

## What it does

- **Finds the date, it doesn't assume one.** For every candidate retirement age it runs the money year by year to the end of the plan. The freedom date is the earliest age where the money survives — not a 25× rule of thumb.
- **Keeps compounding after you stop.** The portfolio earns its return every year of retirement too. Only what you spend leaves the account.
- **Works in today's dollars.** Returns are discounted by inflation, so a dollar on the chart always buys what a dollar buys now. A toggle switches everything to future dollars.
- **Prices the levers.** An exchange rate under the hero: months sooner per $1,000 of retirement spending you drop, per extra point of income saved, per $10,000 invested today — and what one more year of work adds to the pot.
- **Charges for health cover before Medicare.** The biggest surprise cost of stopping early, on top of your spending, in every retired year up to 65.
- **Knows the difference between income that keeps up and income that doesn't.** Social Security holds its buying power, matching the real cost-of-living rise. A pension only does if you say so — leave the switch off, as most private pensions warrant, and it decays every year after it starts. On a $42,000 pension that switch alone is worth two years of freedom.
- **Grows your pay, if you say so.** An optional switch: give it the raise you actually expect ("3% a year") and it tells you what that is worth against inflation. A 2% raise against 2.6% inflation is a pay cut, and the model charges you a year of freedom for it.
- **Lets you name your own date.** The age in the headline is editable — drag it and the whole page re-runs for the age you actually plan to stop, with the earliest possible date still one click away. Pick one too early and it tells you the year the account empties.
- **Estimates Social Security if you don't know your number.** A built-in calculator that runs the real 2026 formula — bend points, the 90/32/15 factors, the taxable maximum, and the penalty or credit for claiming early or late — and shows every step rather than just an answer.
- **Pins a plan so you can argue with it.** Freeze the current plan and it stays on the chart as a dashed ghost while you move everything else, with the gap called out under the date: "3 years earlier than your pinned plan, 2029".
- **Shows what actually moves the date.** One change at a time — savings rate, spending, returns, inflation, starting balance — and how many years each one shifts things.
- **Tests the date against real history.** Not a smooth average — the actual returns of 1928–2024, in the order they happened. See below.

## Tested against history

A steady 7% a year has never happened to anyone. What ruins early retirements isn't a low average return, it's a **bad first decade** — two people with the same lifetime average can end up thirty years apart depending on the order the years arrive.

So the plan is re-run on real markets. For every starting year from 1928 onward, it takes the actual annual returns of the S&P 500 (with dividends) and 10-year US Treasuries, blends them to your stock/bond mix, rebalances once a year, discounts by that year's real CPI, and runs the same saving, spending and stopping age through them.

The date itself still comes from your steady-return assumption — that is what "on your assumptions" means at the top of the page. History then judges it, and the page says so in the same breath rather than burying the caveat:

> **32 of 40** histories where the money lasted — **80%** — and the ones that failed all began in the 1950s.

And because "80%" is not an answer anyone can act on, the panel prices the alternative. Each extra year of work, and what it buys:

> Stop at 49 → **85%**  ·  50 → **94%**  ·  51 → **97%**  ·  52 → **100%**

The headline stays a single date and says what it rests on — "on your assumptions" — and leaves the judgment to the panel rather than arguing with itself in the hero.

The chart shows the middle half and the middle eight-tenths of those histories as bands, every failure as its own red line, and your steady-return assumption as a dashed line so you can see how optimistic or cautious it was against what actually happened.

**Data**: annual total returns for the S&P 500 and 10-year Treasuries plus CPI, 1928–2024, from [Damodaran at NYU Stern](https://pages.stern.nyu.edu/~adamodar/New_Home_Page/datafile/histretSP.html). Verified against the source's cumulative growth of $100 over the full period (S&P geometric mean 9.95% vs the source's 9.94%; Treasuries 4.50% vs 4.50%).

### And a thousand futures that never happened

Thirty-three overlapping windows is a small sample, and the count jumps a few points whenever the date moves. So the same history is also resampled in contiguous **8-year blocks** — crashes keep their real size, a bad decade stays a bad decade, but the orderings are ones history never got around to. A thousand of them, scored beside the real count:

> **40 / 40** histories where the money lasted · **93%** of 1,000 simulated futures

When the two agree, that's reassuring. When they diverge, the shuffle has usually found an ordering worse than anything on record — which is the point of running it.

The draws are seeded, so the same thousand futures are reused on every pass. Move a slider and the number changes because the plan changed, not because the dice were re-rolled.

**Caveat**: the windows overlap heavily. A 58-year plan only fits into 97 years of data 40 times, and neighbouring runs share most of their years. It's a stress test, not a probability.

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

Fees, ACA premium subsidies (which can cut the health-cover bill sharply at low reported income), home equity, state tax, capital-gains tax on the brokerage account, and the Roth ladders and 72(t) withdrawals that can sidestep the early-withdrawal penalty. The projected date still rests on a steady real return; only the history panel varies it.

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
