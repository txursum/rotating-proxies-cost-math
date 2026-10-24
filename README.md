# rotating proxies unlimited bandwidth: What "Unlimited" Actually Means, Real Cost Math, and How to Pick a Plan Without Overpaying

Searching for rotating proxies with unlimited bandwidth usually means one of two things: you're tired of per-GB data caps eating your scraping budget, or you've been burned by an "unlimited" plan that throttled you into the ground. Here's the short answer before we go deeper: several proxy vendors genuinely sell unlimited-bandwidth rotating proxies — the catch is they bill by port instead, and they cap you on speed and concurrent connections. Meanwhile, if what you actually want is unlimited *scraping throughput* with rotating proxies handled for you, a scraping API like ScraperAPI takes a different route: bandwidth is unlimited on every plan, and you pay per request in API credits instead of per gigabyte or per port.

Which one fits you depends on whether you want raw proxies to plug into your own stack, or a managed endpoint that does rotation, retries, and CAPTCHA handling for you. Let's untangle both.

## Quick picks

> **In a hurry?** If your goal is large-scale scraping with rotating residential proxies and no data caps, ScraperAPI's **Hobby plan ($49/month, 100,000 credits)** is the practical starting point, and the free 7-day trial (5,000 credits, no credit card) lets you test your actual target sites before paying anything. 👉 [Check ScraperAPI's current plans and start the free trial](https://www.scraperapi.com/pricing?fp_ref=coupons)
>
> If you specifically need a raw proxy list with unlimited bandwidth on a fixed port, port-based sellers like RotatingProxies or Storm Proxies sell that model — details below, no links needed to understand the trade-offs.

## What "unlimited bandwidth" actually means when you buy rotating proxies

"Unlimited bandwidth" in this market has a specific meaning: no cap on total data transferred. You won't get an overage bill after transferring 500 GB. But unlimited always comes with *some* limit — vendors just move the cap somewhere else, usually to one of three places:

- **Connection speed.** Privateproxy.me explains this plainly: you pay for a fixed Mbps channel (say 200 Mbps) and can push as much traffic as that pipe carries. No per-GB charges, but your total volume is bounded by throughput.
- **Ports.** RotatingProxies sells a fixed number of "ports" (backconnect endpoints) at a flat rate, rotating to a fresh IP every five minutes. Bandwidth is uncapped on every port; the port count is your real quota.
- **Concurrency and device count.** Storm Proxies caps the number of computers that can access the proxies and the number of simultaneous threads per user, depending on the package.

This matters because most of the proxy industry has shifted to per-GB residential billing, where "unlimited" plans are now the exception rather than the rule. The vendors still advertising unlimited bandwidth rotating proxies are typically smaller-pool operations: RotatingProxies runs roughly 700,000 IPs, US/EU only, with a 24-hour money-back guarantee. That's a fraction of what large networks advertise, and it's a genuine trade-off — flat-rate predictability in exchange for a smaller IP pool and no city-level flexibility.

## ScraperAPI's approach: unlimited bandwidth, metered by request

ScraperAPI doesn't sell proxy lists at all. You send a target URL with your API key, and the service handles rotating proxy pools, automatic retries, CAPTCHA and anti-bot bypassing, and optional JavaScript rendering, then returns the HTML — or parsed JSON for supported targets like Amazon, Google Shopping, and Walmart. It's built for developers with existing scraper code that keeps getting blocked.

On bandwidth specifically, every plan — including the free tier — includes **Unlimited Bandwidth** alongside a 99.9% uptime guarantee. No plan charges by the gigabyte. What varies between plans is your monthly allowance of API credits, your concurrent thread count, and your geotargeting range.

Here's the full lineup as shown on the current pricing page:

| Plan | Monthly price | Annual (per month) | API credits / mo. | Concurrent threads | Get it |
| --- | --- | --- | --- | --- | --- |
| Free | $0 | — | 1,000 | 5 | [Start free](https://www.scraperapi.com/?fp_ref=coupons) |
| Hobby | $49 | $44.10 | 100,000 | 20 | [Get Hobby](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Startup | $149 | $134.10 | 1,000,000 | 50 | [Get Startup](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Business | $299 | $269.10 | 3,000,000 | 100 | [Get Business](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Scaling | $475 | $427.50 | 5,000,000 | 200 | [Get Scaling](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Professional | $975 | $877.50 | 10,500,000 | 300 | [Get Professional](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Advanced | $1,975 | $1,777.50 | 21,500,000 | 500 | [Get Advanced](https://www.scraperapi.com/pricing?fp_ref=coupons) |
| Enterprise | Custom | Custom | 22,000,000+ | 500+ | [Contact sales](https://www.scraperapi.com/?fp_ref=coupons) |

Annual billing takes about 10% off every paid tier. A few features that don't show up in the main table but affect real purchases:

- **Geotargeting:** Hobby and Startup are limited to US and EU locations. Country-level targeting outside those regions requires Business ($299) or higher.
- **Analytics retention:** Hobby and Startup only keep the last 30 days of dashboard analytics; Business and up keep everything.
- **Overage handling:** on Hobby through Professional, you can opt into auto-upgrade when credits run out. On Scaling, Professional, Advanced, and Enterprise, pay-as-you-go lets you keep scraping past your cap at a fixed per-credit rate up to a monthly spending cap you set — no hard block mid-job.
- **Credits don't roll over** month to month. If you scrape in quarterly bursts, you'll pay for idle months.

## The part most reviews skip: what a credit actually costs you

Every plan table shows credits, but almost nothing on page one of search results explains that a "credit" is not a page. This is the single biggest thing to understand before you pick a plan.

A standard page costs 1 credit. Then the multipliers start:

- **Amazon, Walmart, eBay:** 5 credits per request
- **Google and Bing** (all subdomains): 25 credits
- **LinkedIn:** 30 credits
- **Cloudflare, Cloudflare Turnstile, Datadome, PerimeterX, Akamai bypasses:** +10 credits per request when activated
- **`render=true` (JavaScript rendering):** +10 credits
- **`premium=true`:** +10 credits; **`ultra_premium=true`:** +30 (paid plans only)
- Combos stack as sets, not sums: `premium + render` is 25 total, and `ultra_premium + render` is 75

Do the math and the picture changes fast. Startup's headline price works out to about $0.000149 per credit — but a single scrape of a JS-rendered, protected Amazon page can run 20–30× that headline number, which is why one experienced reviewer's math shows 1,000,000 credits covering only 40,000–100,000 real Amazon pages with rendering enabled. The same reviewer notes that plain HTML is genuinely cheap: roughly $0.10–0.15 per 1,000 pages from Startup upward.

Two practical safeguards exist, and neither gets mentioned in most plan comparisons. First, the dashboard has a Domain Cost Estimator that tells you the exact credit cost of any URL before you scrape it, and there's also a cost-check API endpoint if you'd rather script it. Second, a `max_cost` parameter caps what any single request can consume — set it and you'll never get surprised by an expensive page.

Also worth knowing: ScraperAPI only charges for successful requests (HTTP 200 and 404). Requests that fail after retries don't burn credits. But if you cancel a request yourself before 70 seconds, it still counts.

If this pricing model clicks for you, it's worth testing against your real targets before committing: 👉 [Start the 7-day trial with 5,000 credits — no credit card required](https://www.scraperapi.com/?fp_ref=coupons)

## Which model fits your actual job

Port-based unlimited proxies and credit-based scraping APIs overlap less than their marketing suggests. A few honest scenarios:

**You want raw proxies for your own browser stack or custom tooling.** Port-based unlimited sellers fit here. You get a proxy endpoint, unlimited data on it, and full control over how requests are made. The trade-offs are structural: smaller IP pools (on the order of hundreds of thousands of IPs versus tens of millions), US/EU coverage on the flat-rate plans, and you handle rotation timing, retries, and CAPTchas yourself. If a target site hardens its defenses, that's your problem to solve.

**You're scraping standard e-commerce and search targets at 20,000–200,000 pages a month and don't want to maintain proxy infrastructure.** This is where a managed API earns its keep. ScraperAPI's default pool clears most requests on ordinary targets without needing the premium tier, and structured endpoints mean you don't rewrite your parser every time Amazon tweaks a page layout. The Hobby plan's 20 concurrent threads handle side-project volumes; anything production-grade at tens of thousands of pages daily will push you toward Startup or Business.

**Your targets are Google SERPs, LinkedIn, or heavily protected sites.** Be realistic about the bill before subscribing. At 25–30 credits per request plus bypass charges, credit-heavy plans burn fast. One review's concrete example: needing 1.1M credits when Startup only includes 1M, with no overage option below Scaling, means paying $299 for Business instead of $149 — a $150 jump from a 10% shortfall. If you're near a plan boundary, set `max_cost` and limit rendering to pages that genuinely need it.

**Your workload is spiky — one big crawl per quarter.** Credits expiring monthly hurts here. Either time your subscription around the crawl, or look at pay-per-request competitors: Decodo's Web Scraping API, for instance, starts at $0.09 per 1,000 requests with usage-based billing that scales down for occasional use.

For a managed-API workflow specifically, the decision point is simple: 👉 [Use the Domain Cost Estimator and plan comparison to match a plan to your real per-page cost](https://www.scraperapi.com/pricing?fp_ref=coupons)

## Limits worth knowing before you buy

No tool in this category is limitation-free, and the honest ones are documented rather than hidden:

- **No IP or ASN selection.** You control country, session stickiness, and IP tier (premium vs. ultra-premium) via parameters, but you can't pin specific IPs or ASNs. Session stickiness tops out around an hour, designed for single crawls — not for account operations or ad verification that need a consistent identity across days. If you need that, raw proxies are the better category.
- **Concurrency caps are hard.** Exceed your plan's thread limit and you get a 429 response. There's no charge for the rejected request — it's turned away, not queued — but your throughput ceiling is real. Hobby's 20 threads is a side-project ceiling, not a production one.
- **Protected domains can be slow.** Simple pages return in seconds; hard targets can take up to 60 seconds, which is why the docs recommend a 70-second client timeout. For volume, the Async API exists precisely for this.
- **Ultra-premium pool has a pricing floor.** Custom-discounted accounts face higher per-request credit costs on ultra-premium domains, to meet a minimum of $3 per thousand requests without rendering, $7 with rendered pages.

## FAQ

**Does "unlimited bandwidth" mean I can scrape infinitely?**
No. It means no data-transfer charges. Port-based plans cap you on ports, speed, or threads; credit-based APIs cap you on monthly credits, which translate to a finite number of pages depending on each page's multiplier.

**How many pages does 100,000 credits actually cover on the Hobby plan?**
Up to 100,000 standard HTML pages at 1 credit each. On Amazon it's about 20,000 pages; on Google it's 4,000. The multiplier, not the plan, decides your real page count.

**What happens if I exceed my plan?**
Concurrency overages return a 429 with no charge. Credit exhaustion pauses scraping until renewal unless you've enabled auto-upgrade (Hobby through Professional) or pay-as-you-go (Scaling and up).

**Is there a free way to test before paying?**
Yes. A 7-day trial with 5,000 credits needs no credit card, and a permanent free plan gives 1,000 credits per month with 5 concurrent connections — enough to validate your target URLs and real credit costs, not enough to run production jobs.

**Can I target countries outside the US and EU?**
Only from the Business plan ($299/month) upward. Hobby and Startup are restricted to US and EU locations.

## Where this leaves you

Match the billing model to your workload and the choice mostly makes itself. Flat-rate unlimited proxies (RotatingProxies, Storm Proxies, privateproxy.me and similar) make sense when you want raw endpoints, small predictable bills, and targets that don't fight back hard. A credit-based scraping API makes sense when you want rotation, bypassing, and parsing handled for you and your targets are mostly standard pages — just budget against your real per-page cost after checking the multiplier, not the credit count on the pricing page.

Two things to confirm before checkout: run your three or four most important target URLs through the cost estimator so you know your actual multiplier, and if you'll need country targeting outside the US and EU, start your comparison at Business rather than being surprised by the geotargeting restriction later. When you're ready, 👉 [compare all ScraperAPI plans and start the free 5,000-credit trial](https://www.scraperapi.com/pricing?fp_ref=coupons) — the trial costs nothing and answers the pricing question with your own data instead of anyone's review.
