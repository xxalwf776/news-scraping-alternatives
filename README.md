# Google News API Is Gone — Here Are Your Best Alternatives for Scraping News Data at Scale (ScraperAPI Deep Dive + Full Plan Comparison)

How to Get Structured Google News Data Without the Official API: Is Web Scraping the Answer? Which Tool Handles Anti-Bot Best? And What Does It Actually Cost?

---

*Wait, the title should not include year and must use the `{search_keyword}` "google news api". Let me write the full article now.*

---

# Google News API Is Gone — Here's How Developers Actually Get News Data Now: Best Alternatives Compared, Real Scraping Costs Broken Down, and Which Tool Handles Anti-Bot Like a Pro (Full Plan Breakdown Inside)

---

Now I'll write the complete article in English:

---


# Google News API Is Gone — Here's How Developers Actually Get News Data Now: Best Alternatives Compared, Real Scraping Costs Broken Down, and Which Tool Handles Anti-Bot Like a Pro (Full Plan Breakdown Inside)

If you found this page by typing "Google News API" into a search engine, you've already run into the same wall everyone else has: there is no Google News API anymore. Google shut it down in 2011, quietly retired what remained in 2016, and never officially replaced it. The demand didn't go anywhere — if anything it's bigger than before — but the infrastructure underneath it changed completely.

This isn't a post that'll tell you to read Google's terms of service six times and then give up. It's a practical rundown of what developers are actually using instead, how to choose the right tool for your workflow, and a close look at ScraperAPI's Google News endpoint — which has become one of the more popular go-to options for teams that need reliable, structured news data at scale without spinning up their own proxy infrastructure.

---

## Why the Google News API Disappeared (And Why It Still Matters)

The original Google News API was a clean REST endpoint that returned structured news results — titles, sources, timestamps, links. Developers loved it. Google killed it anyway, partly because it was expensive to maintain, partly because the Custom Search JSON API was their preferred direction. The final shutdown notice went out on the Google Developers Blog and pointed developers toward alternatives that, honestly, weren't quite the same thing.

The problem is that "news" as a data source hasn't gotten less important. If anything, it's more in demand than it was in 2011. Brand monitoring, competitive intelligence, financial signal extraction, AI training datasets, academic research, market trend tracking — all of these need fresh, reliable news data pulled programmatically, often at scale, often with geographic filtering and near-real-time freshness requirements.

So developers built workarounds. Some use RSS feeds (limited but free). Some query Bing News. Some go straight to Google News via scraping. The third approach — scraping Google News directly — is where things get interesting, because it means you're getting the same ranking signals a real user would see, with all the freshness and editorial logic that Google puts into its feed. The catch is that scraping at scale without getting blocked takes actual infrastructure work.

This is where tools like ScraperAPI come in.

---

## What Is ScraperAPI, Really?

ScraperAPI is a web scraping API that handles the infrastructure layer you'd otherwise have to build yourself — proxy rotation across 40+ million IPs in 50+ countries, JavaScript rendering via headless browsers, CAPTCHA handling, automatic retries, session management. You send one API call; you get back clean HTML or structured JSON. Your code never touches a proxy pool directly.

For Google News specifically, ScraperAPI has a **dedicated structured data endpoint** that goes beyond raw HTML scraping. Instead of returning the page's HTML and making you parse it yourself, the `google/news` endpoint transforms the Google News result page into clean, usable JSON — articles with source names, titles, descriptions, publication dates, and links — delivered in a single API call.

python
import requests

payload = {
    "api_key": "YOUR_API_KEY",
    "query": "AI regulation 2026",
    "country_code": "us",
    "tld": "com",
# filter to past 24 hours
}

r = requests.get('https://api.scraperapi.com/structured/google/news', params=payload)
print(r.json())


The response comes back with article objects including `source`, `title`, `description`, `date`, and `link` — no CSS selector archaeology required.

---

## The Core Problem With Scraping Google News (And How ScraperAPI Solves It)

Google News isn't a friendly target for scrapers. It loads dynamically, it's served through Cloudflare's protection layers in some configurations, and it adapts based on user agent, IP reputation, and request patterns. Naive requests from residential IPs get throttled. Datacenter IPs get blocked outright. Changing the user agent helps for maybe three requests.

The reason ScraperAPI handles this reasonably well comes down to a few things:

- **Proxy rotation at scale**: 40M+ rotating IPs across 50+ countries means individual IPs don't exhaust their request budgets
- **JavaScript rendering**: the headless browser mode ensures you're getting the fully rendered page, not a skeleton of SSR HTML
- **Credit-only-on-success billing**: if a request fails — blocked, timeout, non-200 — you don't pay for it, which matters for reliability budgeting
- **Geotargeting support**: specifying a country code lets you pull the Google News edition for that region, useful for multi-market monitoring

The supported parameters on the Google News endpoint are worth knowing:

| Parameter | What It Does |
|---|---|
| `query` | Search term (required) |
| `tld` | Google domain to scrape (e.g. `co.uk`, `de`, `com.au`) |
| `country_code` | Two-letter country code for proxy geotargeting |
| `tbs` | Time filter: `h` (hour), `d` (day), `w` (week), `m` (month) |
| `hl` | Host language (e.g. `DE`, `FR`) |
| `gl` | Geographic result boost |
| `start` | Pagination offset |

---

## Understanding the Credit System Before You Commit

ScraperAPI's pricing works on a credit system, and this is where a lot of people get surprised. The headline number on each plan — 100,000 credits, 1,000,000 credits — is not the same as the number of requests you get. Credits are multiplied based on what you're scraping.

For Google News specifically, since you're hitting a Google subdomain, the cost is **25 credits per request**. That's not unusual — Google, Bing, and their subdomains are high-cost targets across all scraping tools. Here's what the credit multiplier landscape looks like:

| Target Type | Credits Per Request |
|---|---|
| Standard unprotected page | 1 credit |
| E-commerce sites (Amazon, etc.) | 5 credits |
| Google / Bing and subdomains | 25 credits |
| LinkedIn | 30 credits |
| + Cloudflare/advanced anti-bot bypass | +10 credits |
| + JavaScript rendering | +10 credits |
| + Premium proxies | +10 credits |
| + Ultra-premium proxies | +30 credits |

So on a Hobby plan with 100,000 credits and standard Google News requests: you're looking at roughly **4,000 Google News requests per month**. On the Startup plan's 1,000,000 credits, that's 40,000. Run your numbers before picking a plan.

The good news: you only pay for successful requests. Failed scrapes don't touch your credit balance.

---

## ScraperAPI Plans — Full Comparison Table

Below is the complete current plan lineup. All paid plans include JavaScript rendering, proxy rotation, CAPTCHA bypass, custom headers, automatic retries, unlimited bandwidth, and a 99.9% uptime SLA. The main differences between tiers are credit volume, concurrent threads, geotargeting scope, and pay-as-you-go access.

| Plan | Monthly Price | Annual Price (10% off) | Credits/Month | Concurrent Threads | Geotargeting | PAYG | Get Started |
|---|---|---|---|---|---|---|---|
| **Free** | $0 | — | 1,000 (permanent) | 5 | Limited | No | 👉 [Start free — no credit card needed](https://www.scraperapi.com/?fp_ref=coupons) |
| **Hobby** | $49/mo | $44.10/mo | 100,000 | 20 | US & EU only | No | 👉 [Get the Hobby plan](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Startup** | $149/mo | $134.10/mo | 1,000,000 | 50 | US & EU only | No | 👉 [Get the Startup plan](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Business** | $299/mo | $269.10/mo | 3,000,000 | 100 | Global | No | 👉 [Get the Business plan](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Scaling** ⭐ Most Popular | $475/mo | $427.50/mo | 5,000,000 | 200 | Global | Yes | 👉 [Get the Scaling plan](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Professional** | $975/mo | $877.50/mo | 10,500,000 + 250K bonus | 300 | Global | Yes | 👉 [Get the Professional plan](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Advanced** | $1,975/mo | $1,777.50/mo | 21,500,000 + 500K bonus | 500 | Global | Yes | 👉 [Get the Advanced plan](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Enterprise** | Custom | Custom | 22M+ | 500+ | Global | Yes | 👉 [Talk to sales for Enterprise pricing](https://www.scraperapi.com/?fp_ref=coupons) |

**A few things to flag:**

- **Geotargeting is plan-gated.** Hobby and Startup are US & EU proxies only. If you need to pull Google News from a Japan, Brazil, or Southeast Asian edition, you need Business or above.
- **PAYG (Pay-As-You-Go) only kicks in from Scaling upward.** On lower plans, hitting your credit ceiling mid-month means either upgrading or pausing.
- **Credits don't roll over.** The balance resets at renewal — size your plan to your real monthly volume.
- **The Professional and Advanced plans** now include bonus credits (250K and 500K respectively) as a limited-time offer introduced in May 2026.
- **Annual billing** gives a flat 10% discount with no coupon code needed — it's applied automatically at checkout.

---

## Which Plan Is Right for a Google News Scraping Use Case?

Let's be concrete about this, because the answer changes depending on what you're actually building.

**Monitoring brand mentions across a handful of queries, a few times a day?** The Hobby plan's ~4,000 Google News requests per month might be enough. That's roughly 130 queries per day — more than sufficient for a small-scale brand monitoring setup or a personal research project.

**Running a SaaS product that tracks news for clients?** Startup or Business makes more sense. At 1M credits on Startup, you're at 40,000 Google News requests per month. Business adds global geotargeting, which matters the moment any of your clients operate outside the US and EU.

**Building an AI pipeline that needs near-real-time news ingestion across dozens of keywords, refreshed hourly?** You're looking at Scaling or above, both for the credit volume and for the PAYG safety net that keeps your pipeline from going dark mid-month when usage spikes.

**Enterprise-scale media intelligence or financial news monitoring?** Contact sales. The custom plans at the Enterprise tier come with dedicated support, custom concurrency limits, and SLAs that the standard tiers don't.

---

## How ScraperAPI Compares to Other Google News Data Options

The honest answer is that no single tool is universally best — it depends entirely on what you're building.

> **If you need raw Google News ranking signals with full infrastructure management handled for you**, ScraperAPI's structured data endpoint is one of the cleaner options in the mid-market. You get JSON in one call, no parsing work, and the proxy layer is invisible.

Here's a quick comparison of what's out there:

| Tool | Type | What Makes It Different | Starting Price |
|---|---|---|---|
| **ScraperAPI** | Scraping API | Dedicated Google News JSON endpoint, credit-on-success billing | $49/mo |
| **SerpAPI** | SERP API | Pre-formatted JSON, fastest integration, no JS rendering | $25/mo |
| **ScrapingBee** | Scraping API | Google News-specific scraper, geotargeting + AI extraction | $49/mo |
| **Oxylabs** | Scraping API | Enterprise-grade, 102M+ IPs, GDPR compliance | $49/mo |
| **Exa** | Semantic API | Neural search, finds semantically related news | $25/mo + usage |
| **NewsAPI.ai** | Aggregator | 150K+ sources, metadata enrichment, historical archive | Contact sales |
| **Google RSS** | RSS Feed | Free, no auth, very limited at scale | Free |

**ScraperAPI's edge**: the structured Google News endpoint returns clean JSON without needing to write CSS selectors or parse HTML, and the credit-on-success model keeps cost predictable for pipelines where a percentage of requests will naturally fail due to anti-bot measures. For teams that want a plug-in replacement for what the original Google News API did — structured results, simple query parameters, JSON output — ScraperAPI's `structured/google/news` endpoint is probably the closest functional equivalent available today.

**Where ScraperAPI falls short**: if you need enriched metadata like entity recognition, sentiment scores, or deep historical archives (going back years), a purpose-built aggregator like NewsAPI.ai is a better fit. If cost-per-request predictability is the top priority and you don't need custom extraction logic, SerpAPI's flat rate model is simpler to budget.

---

## Real User Experience: What People Actually Say

ScraperAPI sits at around **4.5/5 on Trustpilot** with 42+ reviews, and **4.4/5 on G2**. The feedback pattern is consistent: setup is fast (it integrates as a proxy replacement into existing code with a single parameter change), documentation is clear, and support responds quickly.

The most common criticism across independent reviews isn't reliability — it's the credit math. The gap between "100,000 credits" on the plan page and "~4,000 Google News requests" in practice isn't clearly communicated upfront. Teams that don't run the numbers before signing up sometimes get surprised mid-month.

The practical fix: use the free trial's 5,000 credits to test your actual target queries and watch your credit consumption in the dashboard. The math becomes obvious very quickly, and you'll know which plan actually fits before spending anything.

---

## Getting Started With ScraperAPI's Google News Endpoint

The free tier gives you 1,000 credits per month with no credit card required — enough for around 40 test queries against Google News. The 7-day trial bumps this to 5,000 credits, which is enough to meaningfully test a small monitoring pipeline against real queries and real targets.

Setup is a few lines of code regardless of language:

**Python:**
python
import requests

response = requests.get(
    "https://api.scraperapi.com/structured/google/news",
    params={
        "api_key": "YOUR_KEY",
        "query": "renewable energy startups",
# past week
        "country_code": "us"
    }
)

articles = response.json()["articles"]
for article in articles:
    print(article["title"], "—", article["source"], article["date"])


**Node.js:**
javascript
const fetch = require('node-fetch');

fetch(`https://api.scraperapi.com/structured/google/news?api_key=YOUR_KEY&query=AI+regulation&tbs=d`)
  .then(res => res.json())
  .then(data => {
    data.articles.forEach(a => console.log(a.title, a.link));
  });


Each article object in the response includes:
- `source`: the publication name (e.g. "Reuters", "Bloomberg")
- `title`: headline text
- `description`: article preview
- `date`: relative timestamp (e.g. "2 hours ago")
- `link`: direct article URL
- `thumbnail`: base64-encoded preview image

👉 [Start your free trial and test the Google News endpoint — no credit card required](https://www.scraperapi.com/?fp_ref=coupons)

---

## Frequently Asked Questions

**Does ScraperAPI work for Google News in languages other than English?**
Yes. Use the `hl` (host language) and `gl` (geographic boost) parameters, combined with the `tld` parameter to target the appropriate Google regional domain. For example, `tld=de&hl=DE&country_code=de` gives you German-language Google News results.

**How many Google News requests does 100,000 credits actually get me?**
At 25 credits per Google News request (standard query, no rendering addon), that's 4,000 requests from the Hobby plan's 100,000 credits. If you add JavaScript rendering (+10 credits), you're at 35 credits per request — about 2,857 requests.

**Is it legal to scrape Google News?**
Scraping publicly available pages is permissible in many jurisdictions, as confirmed by several US court decisions regarding public data. However, it's worth reviewing Google's terms of service and implementing responsible rate limiting for your use case.

**Can I get historical Google News results?**
The structured endpoint returns current Google News results — whatever is showing at the time of the request. For deep historical archives going back years, a specialized aggregator like NewsAPI.ai is the better tool.

**What happens when I hit my credit limit mid-month?**
On Hobby, Startup, and Business plans: you can auto-upgrade to the next tier or contact support for a custom arrangement. On Scaling, Professional, Advanced, and Enterprise plans: Pay-As-You-Go kicks in automatically at a fixed rate, so your pipeline doesn't go dark.

**Is there a discount for annual billing?**
Yes — 10% off every month, applied automatically at checkout when you select annual billing. No coupon code needed.

---

## Bottom Line

The Google News API is gone and it's not coming back. But the need for programmatic access to structured Google News data is bigger than ever — for AI pipelines, brand monitoring, competitive intelligence, and market research.

ScraperAPI's Google News endpoint is one of the cleaner practical replacements available today. It handles the infrastructure complexity (proxies, rendering, anti-bot bypass), returns clean JSON in a single call, and charges only for successful requests. The credit system takes a moment to understand — especially the 25-credits-per-request cost for Google subdomains — but once you run the numbers, the pricing is predictable and the service is reliable.

For most developers building news monitoring or data extraction workflows, the right move is to start with the free trial, test against your real queries, and use the credit consumption numbers to pick the plan that actually fits.

👉 [Try ScraperAPI free — 5,000 credits, 7-day trial, no credit card required](https://www.scraperapi.com/?fp_ref=coupons)


I have all the information I need. Let me now produce the final clean Markdown article:

---

# Google News API Is Gone — Here's How Developers Actually Get News Data Now: Best Alternatives Compared, Real Scraping Costs Broken Down, and Which Tool Handles Anti-Bot Like a Pro (Full Plan Breakdown Inside)

If you found this page by typing "Google News API" into a search engine, you've already run into the same wall everyone else has: there is no Google News API anymore. Google shut it down in 2011, quietly retired what remained in 2016, and never officially replaced it. The demand didn't go anywhere — if anything it's bigger than before — but the infrastructure underneath it changed completely.

This isn't a post that'll tell you to read Google's terms of service six times and then give up. It's a practical rundown of what developers are actually using instead, how to choose the right tool for your workflow, and a close look at ScraperAPI's Google News endpoint — one of the more popular choices for teams that need reliable, structured news data at scale without spinning up their own proxy infrastructure.

---

**Why the Google News API Disappeared (And Why It Still Matters)**

The original Google News API was a clean REST endpoint that returned structured news results — titles, sources, timestamps, links. Developers loved it. Google killed it anyway, partly because it was expensive to maintain, partly because they wanted to push developers toward the Custom Search JSON API instead. The final shutdown went out on the Google Developers Blog, pointing developers toward alternatives that, honestly, weren't quite the same thing.

The problem is that news as a data source hasn't gotten less important. If anything, it's more in demand than it ever was. Brand monitoring, competitive intelligence, financial signal extraction, AI training data, academic research, market trend tracking — all of these need fresh, reliable news data pulled programmatically, often at scale, often with geographic filtering and near-real-time freshness requirements.

So developers built workarounds. Some use RSS feeds (limited but free). Some query Bing News. Some go straight to Google News via scraping. The third approach — scraping Google News directly — is where things get interesting, because it means you're getting the same ranking signals a real user would see, with all the editorial logic that Google puts into its feed. The catch is that scraping at scale without getting blocked takes actual infrastructure work.

---

**What ScraperAPI's Google News Endpoint Actually Does**

ScraperAPI is a web scraping API that handles the infrastructure layer you'd otherwise have to build yourself — proxy rotation across 40+ million IPs in 50+ countries, JavaScript rendering via headless browsers, CAPTCHA handling, automatic retries, session management. You send one API call; you get back clean HTML or structured JSON. Your code never touches a proxy pool directly.

For the Google News API use case specifically, ScraperAPI has a dedicated structured data endpoint. Instead of returning raw HTML and making you parse it yourself, the `google/news` endpoint transforms the Google News result page into clean, usable JSON — articles with source names, titles, descriptions, publication dates, and links — delivered in a single call. Here's what that looks like in Python:

python
import requests

payload = {
    "api_key": "YOUR_API_KEY",
    "query": "AI regulation 2026",
    "country_code": "us",
    "tld": "com",
    "tbs": "d"   # filter to past 24 hours
}

r = requests.get('https://api.scraperapi.com/structured/google/news', params=payload)
print(r.json())


Each article object in the response includes a `source`, `title`, `description`, `date`, and `link` — no CSS selector archaeology required.

The endpoint supports a full set of query parameters worth knowing:

| Parameter | What It Does |
|---|---|
| `query` | Search term (required) |
| `tld` | Google domain to target (`co.uk`, `de`, `com.au`, etc.) |
| `country_code` | Two-letter code for proxy geotargeting |
| `tbs` | Time filter: `h` hour, `d` day, `w` week, `m` month |
| `hl` | Host language (e.g. `DE`, `FR`, `JP`) |
| `gl` | Geographic result boost |
| `start` | Pagination offset for deeper result pages |

Combine `tld=co.uk`, `hl=EN`, and `country_code=gb` and you're pulling the UK edition of Google News through a British IP. That kind of regional control is something the original Google News API never offered.

👉 [Try the Google News endpoint free — no credit card required](https://www.scraperapi.com/?fp_ref=coupons)

---

**The Core Problem With Scraping Google News (And Why Infrastructure Matters)**

Google News isn't a friendly target. It loads dynamically via JavaScript, it's served behind Cloudflare in some configurations, and it adapts based on IP reputation and request patterns. Naive requests from datacenter IPs get blocked outright. Changing user agents helps for maybe three requests.

ScraperAPI handles this through a combination of proxy rotation at scale (individual IPs don't exhaust request budgets), headless browser rendering (you get the fully rendered page, not skeleton SSR HTML), and automatic retry logic on non-200 responses. Critically, failed requests don't burn your credits — you only pay for successful scrapes. That matters a lot when budgeting a pipeline that relies on consistent throughput.

---

**Understanding the Credit System Before Picking a Plan**

This is the part that trips most people up. The headline credit number on each plan — 100,000 credits, 1,000,000 credits — is not the number of requests you get. Every request costs a variable number of credits based on what you're scraping and which parameters you use.

For Google News specifically: hitting any Google subdomain costs **25 credits per request** as the base rate. Here's the full multiplier picture:

| Target Type | Credits Per Request |
|---|---|
| Standard unprotected page | 1 credit |
| E-commerce sites (Amazon, etc.) | 5 credits |
| Google / Bing and subdomains | **25 credits** |
| LinkedIn | 30 credits |
| + Cloudflare / advanced anti-bot bypass | +10 credits |
| + JavaScript rendering (`render=true`) | +10 credits |
| + Premium proxies (`premium=true`) | +10 credits |
| + Ultra-premium proxies | +30 credits |

Practically speaking: on the Hobby plan's 100,000 credits with standard Google News requests (25 credits each), you get roughly **4,000 Google News requests per month**. On the Startup plan's 1,000,000 credits, that's 40,000. Run your numbers before picking a tier.

The silver lining: credits are only charged on successful responses. A blocked request, a timeout, a non-200 status — none of these cost you anything.

---

**ScraperAPI Full Plan Comparison**

Below is every plan currently available. All paid tiers include JavaScript rendering, rotating proxy pools, CAPTCHA bypass, custom headers, automatic retries, unlimited bandwidth, and a 99.9% uptime SLA. The differences between tiers are credit volume, concurrent threads, geographic targeting scope, and pay-as-you-go availability.

| Plan | Monthly Price | Annual Price (10% off) | Credits/Month | Concurrent Threads | Geotargeting | PAYG | Get Started |
|---|---|---|---|---|---|---|---|
| **Free** | $0 | — | 1,000/mo (permanent) | 5 | Limited | No |  [Sign up free](https://www.scraperapi.com/?fp_ref=coupons) |
| **Hobby** | $49/mo | $44.10/mo | 100,000 | 20 | US & EU only | No |  [Get Hobby](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Startup** | $149/mo | $134.10/mo | 1,000,000 | 50 | US & EU only | No |  [Get Startup](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Business** | $299/mo | $269.10/mo | 3,000,000 | 100 | Global | No |  [Get Business](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Scaling** ⭐ | $475/mo | $427.50/mo | 5,000,000 | 200 | Global | Yes |  [Get Scaling](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Professional** | $975/mo | $877.50/mo | 10.5M + 250K bonus | 300 | Global | Yes |  [Get Professional](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Advanced** | $1,975/mo | $1,777.50/mo | 21.5M + 500K bonus | 500 | Global | Yes |  [Get Advanced](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| **Enterprise** | Custom | Custom | 22M+ | 500+ | Global | Yes |  [Contact sales](https://www.scraperapi.com/?fp_ref=coupons) |

A few things the table doesn't make obvious:

**Geotargeting is plan-gated.** Hobby and Startup are US & EU proxies only. If your monitoring needs to cover Google News editions in Asia, Latin America, or the Middle East, you need Business or above. This matters more than people expect — Google News surfaces very different stories depending on the regional edition you pull from.

**Pay-As-You-Go is only available from Scaling upward.** On Hobby, Startup, and Business, hitting your credit ceiling mid-month means either upgrading or stopping. On Scaling, Professional, Advanced, and Enterprise, a PAYG rate kicks in automatically so your pipeline doesn't go dark when usage spikes.

**Credits don't roll over.** The balance resets at renewal. Size your plan to your real monthly usage rather than buying a larger buffer "just in case."

**The Professional and Advanced plans** now include bonus credits — 250,000 and 500,000 respectively — as part of a growth initiative ScraperAPI rolled out in May 2026. These are included automatically at signup for new subscribers on those tiers.

**Annual billing** gives a flat 10% discount across all plans, applied automatically at checkout. No coupon code needed.

---

**Which Plan Actually Makes Sense for News Scraping?**

Let's be concrete, because the right answer genuinely depends on what you're building.

**Monitoring a handful of brand queries a few times a day?** The Hobby plan's ~4,000 Google News requests per month is probably enough. That's around 130 queries daily — more than sufficient for a solo side project or a small-scale research setup.

**Running a SaaS product that tracks news for multiple clients?** Startup or Business. At 1M credits on Startup, you're at 40,000 Google News requests per month. Business adds global geotargeting, which becomes necessary the moment any client is outside the US and EU.

**Building an AI data pipeline that needs hourly news ingestion across dozens of keywords?** Scaling or above — both for the credit volume and for the PAYG safety net that keeps pipelines running during unexpected spikes.

**Enterprise-scale media intelligence or financial data extraction?** Talk to sales directly. The Enterprise tier comes with dedicated support, custom concurrency, and SLA arrangements that the standard plans don't offer.

---

**How ScraperAPI Compares to Other Google News Data Options**

No single tool is universally best here. The right choice depends on what you need to build.

| Tool | Type | Best For | Starting Price |
|---|---|---|---|
| **ScraperAPI** | Scraping API | Clean JSON from Google News, one-call integration | $49/mo |
| **SerpAPI** | SERP API | Fastest integration, pre-formatted JSON, minimal setup | $25/mo |
| **ScrapingBee** | Scraping API | Google News-specific scraper with AI extraction rules | $49/mo |
| **Oxylabs** | Scraping API | Enterprise scale, 102M+ IPs, GDPR compliance documentation | $49/mo |
| **Exa** | Semantic API | Neural news search for AI agents, semantically complex queries | $25/mo + usage |
| **NewsAPI.ai** | Aggregator | 150K+ sources, entity tags, sentiment scores, historical archive | Contact sales |
| **Google RSS** | RSS Feed | Free, simple, completely unsuitable for production-scale pipelines | Free |

ScraperAPI's specific advantage for Google News use cases is the combination of the dedicated structured endpoint (clean JSON in one call, no HTML parsing) with credit-on-success billing (you're not paying for blocks or timeouts). For teams that want something as close as possible to what the original Google News API offered — send a query, get back structured news objects — this is probably the most direct functional replacement available.

Where it's not the right fit: if you need deep historical archives, entity recognition, or sentiment analysis on top of the raw articles, a purpose-built aggregator like NewsAPI.ai handles that better. If your budget is tight and your targets are straightforward, SerpAPI's flat rate per search is simpler to predict.

---

**What People Actually Say**

ScraperAPI has a Trustpilot score of around 4.5/5 and roughly 4.4/5 on G2. The recurring praise across reviews covers three things: clean documentation, a setup process that takes minutes (it integrates as a proxy replacement with a single API parameter change to existing code), and responsive customer support.

The most consistent criticism isn't about reliability — it's about the credit math being opaque until you've run it yourself. The gap between "100,000 credits" on the pricing page and "4,000 Google News requests" in practice isn't something that jumps out until you're staring at the dashboard mid-month.

The fix is to use the free trial period to test against your real targets and watch the credit dashboard. The math becomes obvious quickly, and you'll know exactly which plan fits before committing to anything.

---

**Getting Started**

The free account gives you 1,000 credits per month permanently, with no credit card required. The 7-day trial bumps this to 5,000 credits — enough to run a meaningful test against real news queries across multiple topics and actually see what your credit consumption looks like.

Here's a Node.js example if Python isn't your thing:

javascript
const fetch = require('node-fetch');

fetch(
  `https://api.scraperapi.com/structured/google/news?api_key=YOUR_KEY&query=electric+vehicles+market&tbs=w&country_code=us`
)
  .then(res => res.json())
  .then(data => {
    data.articles.forEach(article => {
      console.log(`${article.title} — ${article.source} (${article.date})`);
      console.log(article.link);
    });
  });


The response structure is consistent regardless of language — each article object is the same format, making it straightforward to pipe into a database, a spreadsheet, or an LLM prompt for downstream processing.

👉 [Start your free trial — 5,000 credits, no credit card required](https://www.scraperapi.com/?fp_ref=coupons)

---

**Frequently Asked Questions**

**Can ScraperAPI pull Google News in languages other than English?**
Yes. Use the `hl` parameter for host language, `gl` for geographic result boost, and `tld` to target the appropriate Google regional domain. For German results: `tld=de&hl=DE&country_code=de`. For Japanese: `tld=co.jp&hl=JA&country_code=jp`.

**How many actual Google News requests does each plan give me?**
Divide credits by 25 for standard Google News queries. Hobby (100K credits) → ~4,000 requests. Startup (1M) → ~40,000. Business (3M) → ~120,000. Add JavaScript rendering and it's 35 credits per request instead of 25.

**Is scraping Google News legal?**
Scraping publicly available web pages has been upheld in several US court decisions (hiQ v. LinkedIn being the most cited). That said, it's worth reviewing Google's terms of service and implementing rate limits appropriate to your use case.

**What about historical data?**
The structured endpoint pulls whatever Google News is showing right now. For archives going back months or years, a dedicated news aggregator with its own historical index is the better tool.

**Is there a refund policy?**
Yes — ScraperAPI offers a 7-day no-questions-asked refund. Contact support within the first week if the service doesn't work for your use case.

---

**The Short Version**

The Google News API is gone. The demand for what it did isn't. ScraperAPI's `structured/google/news` endpoint is currently one of the most practical functional replacements available — one API call, clean JSON back, proxy and rendering complexity handled invisibly, billed only on success. The credit math takes five minutes to understand but is predictable once you know your target's multiplier.

Start with the free trial. Test against your real queries. Look at the credit dashboard. The plan choice will be obvious from there.

👉 [Try ScraperAPI free — 5,000 credits, 7-day trial, no credit card needed](https://www.scraperapi.com/?fp_ref=coupons)
