# Review scraper pricing: what 1,000 reviews cost, which ScraperAPI plan covers it, and why a Cloudflare-guarded page bills 11 credits (full plan table)

A review scraper's bill is set by how many requests it takes to land one review, and that number depends on the review site's defences rather than the plan's headline price. On ScraperAPI a plain page costs 1 credit, bypassing Cloudflare adds 10, and JavaScript rendering adds another 10. Capterra serves up to 25 reviews per page, so 1,000 Capterra reviews is roughly 40 requests, or 440 to 840 credits. At the Hobby plan's $49 for 100,000 credits, that lands between **$0.22 and $0.41 per 1,000 reviews**, before you write a line of parsing code.

Below are the current plan tiers and what each one unlocks, the credit multipliers that decide your real cost, how per-request pricing compares with per-record review scrapers from Apify and Bright Data, and the overage rules that catch people in month two.

> **Most readers should start on Hobby: $49/month for 100,000 credits and 20 concurrent threads.** That covers about 4,700 page loads that need both bot bypass and rendering, or roughly 119,000 reviews at 25 per page. Test on the 5,000-credit, 7-day trial first, which needs no card. Move up to Business ($299) only when you need country-level targeting outside the US and EU.
>
> 👉 [See the Hobby plan and what 100,000 credits buy](https://scraperapi.com/pricing?fp_ref=coupons)

## ScraperAPI plans: credits, threads and the two tiers that unlock country targeting

Every tier runs on the same API; what changes is the monthly credit allowance, the concurrency ceiling and the geotargeting scope. Hobby and Startup cap geotargeting at the US and EU. Country-level targeting starts at Business.

| Plan | API credits / month | Concurrent threads | Geotargeting | Price | Get started |
| --- | --- | --- | --- | --- | --- |
| Free | 1,000 | 5 | — | $0 | [Free plan](https://scraperapi.com/pricing?fp_ref=coupons) |
| Hobby | 100,000 | 20 | US & EU | $49/mo | [Hobby plan](https://scraperapi.com/pricing?fp_ref=coupons) |
| Startup | 1,000,000 | 50 | US & EU | $149/mo, or $134.10/mo billed annually ($1,609.20/yr) | [Startup plan](https://scraperapi.com/pricing?fp_ref=coupons) |
| Business | 3,000,000 | 100 | Country-level | $299/mo | [Business plan](https://scraperapi.com/pricing?fp_ref=coupons) |
| Scaling | 5,000,000 | 200 | Country-level | $475/mo, or $427.50/mo billed annually ($5,130/yr) | [Scaling plan](https://scraperapi.com/pricing?fp_ref=coupons) |
| Professional | 10,500,000 | 300 | Country-level | See plan page | [Professional plan](https://scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | 21,500,000 | 500 | Country-level | See plan page | [Advanced plan](https://scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | 22,000,000+ | 500+ | Country-level | See plan page | [Enterprise plan](https://scraperapi.com/pricing?fp_ref=coupons) |

Two things in that table matter more than the others for review work. The first is thread count: 20 threads on Hobby is fine for a few thousand pages a month and painful for a 40,000-page historical backfill. The second is geotargeting. If you're pulling reviews from a localized Trustpilot or Capterra domain and need the request to leave from that country, Hobby and Startup won't do it.

The trial is separate from the Free plan: 5,000 credits over 7 days, $0, no card required, and it converts to a paid plan or drops you onto the free tier when it ends.

👉 [Start the 5,000-credit, 7-day trial without a card](https://scraperapi.com/signup?fp_ref=coupons)

## The credit multipliers that decide your review scraper bill

ScraperAPI charges credits per request, and the cost of one request depends on the target and the parameters you send. This is the published rate card:

| Request type | Credits | Notes |
| --- | --- | --- |
| Standard page | 1 | Per request |
| Amazon, Walmart, eBay | 5 | Per request |
| Google, Bing (incl. subdomains) | 25 | Per request |
| LinkedIn | 30 | Per request |
| Bot-protection bypass | 10 | Cloudflare, Cloudflare Turnstile, DataDome, PerimeterX/HUMAN, Akamai |
| JS rendering (`render=true`) | 10 | Per request |
| Premium proxy (`premium=true`) | 10 | Per request |
| Screenshot | 10 | Per request |
| Premium proxy + rendering | 25 | Per request |
| Ultra premium | 30 | Paid plans only |
| Ultra premium + rendering | 75 | Paid plans only |
| Geotargeting, sessions, device type, output format, auto parsing | 0 | No extra cost |

The bypass line is additive. A Capterra review page sits behind Cloudflare, so the request carries the 10-credit bypass on top of the 1-credit page cost, and if the reviews only appear after JavaScript runs, another 10 goes on. That's how a page that looks like 1 credit becomes 11 or 21.

Put against a realistic workload:

| Scenario | Credits per page | Pages for 1,000 reviews | Total credits | Hobby cost | Startup cost |
| --- | --- | --- | --- | --- | --- |
| Static review page, no protection | 1 | 40 | 40 | ~$0.02 | ~$0.01 |
| Cloudflare-guarded page (Capterra-style) | 11 | 40 | 440 | ~$0.22 | ~$0.07 |
| Cloudflare + JS rendering | 21 | 40 | 840 | ~$0.41 | ~$0.13 |

The 40-page figure assumes 25 reviews per page, which is Capterra's usual page size. Sites that paginate 10 reviews at a time double or triple the request count for the same 1,000 records, and nothing in the pricing table warns you about that.

The per-credit rate falls as you climb: $0.00049 on Hobby, $0.000149 on Startup, roughly $0.0001 on Business, about $0.000095 on Scaling. At higher volumes the per-credit rate you buy at matters more than the per-page multiplier, which is why the same 840 credits cost three times more on Hobby than on Startup.

Two official tools help before you commit: the Domain Cost Estimator in the dashboard gives the exact credit cost for any URL, and `max_cost` caps what a single scrape is allowed to burn.

## How that compares with per-record review scrapers

Apify's Capterra actor bills per review written to the dataset: **$0.89 per 1,000** on the free tier, falling to $0.79 on Bronze, $0.69 on Silver and $0.59 on Gold, with Apify's normal platform usage credits applied separately. Its five-platform actor, which pulls G2, Capterra, TrustRadius, Gartner and Trustpilot into one schema, runs $4.99 per 1,000 on the free tier down to $3.99 on Gold. New accounts get $5 in platform credits, about 1,400 records on the five-platform actor.

|  | ScraperAPI | Apify Capterra actor | Apify five-platform actor |
| --- | --- | --- | --- |
| Billing unit | Credits per request | Per review record | Per review record |
| Cost per 1,000 reviews | ~$0.22–$0.41 in credits on Hobby, plus your parser | $0.89 free tier, down to $0.59 | $4.99 free tier, down to $3.99 |
| Output | Page in your chosen format; auto parsing costs no extra credits | Review-level fields | Unified schema plus per-platform extras |
| Platforms | Any URL you send | Capterra only | G2, Capterra, TrustRadius, Gartner, Trustpilot (opt-in) |
| Blocking handled | Yes, at +10 credits per request | Yes, Unblocker proxy required | Yes |
| Free allowance | 5,000 credits for 7 days, then 1,000/month | $5 in platform credits | $5 in platform credits |

A 5× to 20× gap looks decisive until you check what's included. Apify sells finished records with the parsing maintained for you. ScraperAPI sells page fetches, and the $0.22 to $0.41 figure leaves out the parser you write and repair whenever Capterra reshuffles its markup. If you already have a scraping codebase and a working parser, the per-request model wins on price. If you don't, the parsing work is the product you're actually buying.

Bright Data's reviews scraper sits somewhere in between. Its page describes 5,000 free monthly credits worth about $7.50, no card required, renewing on the 1st and not rolling over; once they're gone, requests error out until you deposit funds or the credits renew. Billing is per successfully delivered record with proxies, rendering, concurrency and delivery included. That page carries a 2022 date, so treat the free-credit terms as indicative and confirm them before you budget on them.

## What you get back, and the parsing work the price hides

Apify's Capterra actor returns `review_id`, six separate ratings (overall, ease of use, customer service, features, value for money, likelihood to recommend), reviewer name, job title, industry, company size and time using the product, validation status and method (LinkedIn, business email, proof of link), pros, cons, general comments, advice to others, chosen and switching reasons, and an incentive flag. The five-platform actor adds per-platform extras: G2's validated reviewer badges and review source, TrustRadius feature ratings and ROI data, Gartner's market and vendor names, Trustpilot's review language, likes, company replies and verification level.

The incentive flag and the validated-reviewer flag are the two fields that change what your analysis can claim. Filtering paid reviews out of a competitor comparison, or weighting by verification, needs data most scrapers never collect.

A free Puppeteer script for Google Maps shows the other end of the spectrum. It returns `reviewId`, name, rating, text, date, likes, images, profile picture, profile URL, owner response and a scrape timestamp. That covers sentiment counting and response-rate tracking. It cannot separate an incentivized review from an organic one, because Google doesn't expose that field at all.

On ScraperAPI the page comes back in your chosen format with auto parsing listed at no extra credit cost, and the field mapping is yours to define. For a single site you'll revisit monthly, that's a few hours of work. Across five review platforms with different layouts, the maintenance load is the real expense.

## Where review scraping breaks without a proxy layer

Capterra runs Cloudflare. Apify's own documentation states that datacenter and residential proxies get stuck on the challenge page and that its Unblocker proxy is required, which is why that actor ships with Unblocker as the default. This is the practical case for paying a provider instead of running headless Chrome on a cheap VPS: the challenge page, not the parsing, is where most homegrown review scrapers die.

Google Maps has a different failure mode. The open-source route comes with its own warnings: Google throttles aggressive scraping, businesses with 1,000+ reviews take several minutes to finish, and selector changes break extraction when the HTML shifts. Its author recommends the official Places API for commercial use and says plainly that the tool isn't built for real-time monitoring or thousands of businesses a day.

ScraperAPI handles both obstacles through the credit system rather than separate products: bypass for Cloudflare, DataDome, PerimeterX, Akamai and Turnstile at 10 credits, rendering for JavaScript-heavy pages at 10, sessions and geotargeting at no extra charge.

👉 [Run a Cloudflare-guarded review page through the bypass](https://scraperapi.com/pricing?fp_ref=coupons)

## Overage, rollover and renewal: the terms that change the monthly cost

Credits reset monthly and don't roll over, so an unused allowance is gone. When you hit the ceiling, scraping pauses until renewal by default. Auto-upgrade, which moves your account to the next plan automatically, is available on Hobby, Startup, Business, Scaling and Professional. Pay-as-you-go, which keeps you on your current plan at a fixed per-credit rate up to a monthly cap you set, starts at Scaling. Annual plans can renew early for a fresh batch of credits.

That split matters for budgeting. On Hobby, a viral review spike or a competitor's product launch means waiting for the reset or accepting an upgrade, with nothing in between. If your review volume is spiky by nature, either size the plan for the peak or start at a tier where pay-as-you-go exists.

👉 [Check which plans include pay-as-you-go overage](https://scraperapi.com/pricing?fp_ref=coupons)

## Is scraping reviews legal?

Every vendor in this category pushes the question to the user. Apify's actor page says it collects only data Capterra already displays to any visitor, never touches private reviewer accounts, and leaves responsibility for Capterra's terms of service and local law with you. Bright Data says it handles only publicly available data, cites GDPR, CCPA, SOC 2 and ISO 27001 controls, and mentions a compliance team reviewing use cases.

Neither position transfers the obligation. Reviews contain personal data (names, job titles, company size, sometimes photos), and if you store that in a dataset covering EU residents, you need a lawful basis for it independent of how you collected the page.

## FAQ

**How many credits does 1,000 reviews take?**
Divide 1,000 by the reviews per page, then multiply by the per-request credit cost. Capterra at 25 per page is 40 requests: 40 credits on an unprotected page, 440 with Cloudflare bypass, 840 with bypass and rendering.

**Is the free plan enough to test a review scraper?**
1,000 credits is about 90 bypassed pages or 45 bypassed-and-rendered ones, enough to confirm your selectors against the live site and no more. The 7-day, 5,000-credit trial is the better test window.

**Do unused credits roll over?**
No. The allowance resets each month, and running out pauses scraping until renewal unless auto-upgrade or pay-as-you-go is active on your plan.

**Can I target a country outside the US and EU?**
Country-level geotargeting starts at Business ($299/month). Hobby and Startup are limited to US and EU.

**Why does my own scraper get a challenge page on Capterra?**
Cloudflare blocks datacenter and residential proxy traffic on that domain. Apify's documentation is explicit about needing an unblocker, and ScraperAPI prices the bypass at 10 credits per request.

## Which setup fits your case

One Capterra or G2 product page, refreshed monthly: Hobby at $49 is more capacity than you need, but it's the cheapest paid tier and 100,000 credits covers years of that workload.

Five review platforms and a normalized schema you don't want to maintain: Apify's five-platform actor at $4.99 per 1,000 is expensive next to raw credits and cheaper than the engineering time to replicate it.

High volume with an existing parser: Startup's $149 for 1,000,000 credits works out to about $0.13 per 1,000 rendered, protected reviews, and Scaling drops the per-credit rate further. Country-level targeting, if you need it, pushes you to Business.

Zero budget and comfortable with Puppeteer: the open-source Google Maps script is genuinely useful for a one-off pull. Budget for proxies, rate-limit delays and selector repairs, because that's where the "free" option spends its money.

Before you pay, run 200 pages of your real target through the trial and check the Domain Cost Estimator for the exact per-URL cost. The multiplier on your specific review site decides the plan, and it's rarely 1 credit.

👉 [Compare every plan and credit allowance on ScraperAPI's pricing page](https://scraperapi.com/pricing?fp_ref=coupons)
