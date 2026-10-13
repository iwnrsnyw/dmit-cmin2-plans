# DMIT CMIN2: What the Eyeball Route Really Delivers, Which Plan Fits Your ISP, and When Paying More for CN2 GIA Stops Being Worth It

Most people typing "DMIT CMIN2" into a search box have already done the hard part of the research. They know they want a US West VPS with China-optimized routing, they've realised that "optimized" means nothing on its own, and they've landed on DMIT's Eyeball (EB) line — the one that runs China Mobile traffic over CMIN2 — as a candidate. What they don't have yet is a straight answer to three questions: what CMIN2 actually does for each of the three Chinese carriers, how the Eyeball plans compare against each other, and whether they should be paying for CN2 GIA instead.

That's what this covers. Pricing and specs below come from DMIT's current Los Angeles restock listings, cross-checked against several independently published plan tables and route traces. Where sources disagree, it's flagged rather than smoothed over, because a lot of the numbers floating around in forums are two or three platform generations old.

## CMIN2 is an ASN, not a marketing label

China Mobile International's second-generation backbone shows up in traceroutes as **AS58807**. It's the successor to the ordinary CMI path, and the practical difference is resource allocation: CMIN2 gets bigger international capacity and more direct routing, which is why it holds up better at 8–10pm when every other path to the US West is congested.

DMIT isn't the only provider buying it, but the reason CMIN2 keeps coming up in the same sentence as DMIT is that the company bought it *in addition* to the two other premium backbones:

- **CMIN2 (AS58807)** — China Mobile's premium international path
- **AS9929 / CUG VIP** — China Unicom Global's premium path, a clear step above the standard 4837 routing
- **CN2 GIA (AS4809)** — China Telecom's premium path

Those three define the entire product line. If you buy a cheap "Asia-optimized" VPS somewhere else, you're usually getting regular BGP that happens to land in Los Angeles.

## Where CMIN2 sits in DMIT's Los Angeles lineup

DMIT splits its LAX inventory into three network profiles, and the names are worth memorising because they show up in every plan name:

| Series | Network profile | China direction |
| --- | --- | --- |
| LAX.T1 (Tier 1) | International BGP | No China optimization |
| LAX.EB (Eyeball) | CMIN2 + AS9929 | Optimized, mobile-leaning |
| LAX.Pro (Premium) | CN2 GIA (AS4809) | Optimized, telecom-leaning |

So when someone writes "LAX.EB.TINY", they mean: Los Angeles datacenter, Eyeball routing, smallest configuration tier. The platform prefix is separate — current LAX stock has been cycling through AS3 (AMD EPYC 7003) and the newer AN4/AN5 generations (EPYC 9004/9005), and prices differ between them. The table further down reflects the AS3 restock figures that the recent listings agree on; if the cart shows a different number for a newer platform, the cart is right.

If you want to skip ahead and see what's in stock rather than read the whole thing: 👉 [check current DMIT Los Angeles stock and live pricing](https://www.dmit.io/aff.php?aff=12046).

## The routing, carrier by carrier

This is the part that gets oversimplified in forum posts, because "CMIN2 line" is only true for one of the three carriers in the return direction.

**China Mobile** gets the clean version. Outbound and return both ride CMIN2. Published route traces from Beijing, Shanghai and Guangdong test nodes show the path leaving DMIT's AS906, handing to AS58807 at Los Angeles, then entering China Mobile's AS9808 in Shanghai — usually one hop of international transit total.

**China Unicom** rides AS9929 (CUG VIP) on the return. A typical Beijing trace goes out through AS4837/AS10099 and comes back over 9929. That's the same premium Unicom path that providers charge extra for, so Eyeball is effectively bundling two carriers' top tiers.

**China Telecom** is the compromise. Return traffic is load-balanced between AS9929 and AS58807 rather than pinned to CN2 GIA. It's a good path, but it is not the GIA-optimized path, and that's the single biggest reason to consider Pro instead.

What that translates to in numbers: third-party traceroutes and reviews cluster in the **126–170 ms** range from mainland China, with nationwide averages landing around **163 ms**. For a Los Angeles endpoint that's about as good as it gets without paying CN2 GIA rates.

Two details that matter more than the headline latency:

> Traffic that exceeds the monthly allowance doesn't cut you off. The port drops to 4, 8 or 10 Mbps depending on the plan and the server keeps running as an unmetered connection. On the smallest tiers that fallback speed is genuinely slow, but it beats a suspended service.

> IPv6 is optimized too, not an afterthought — the same CMIN2 + CUG VIP return path applies.

## Every LAX Eyeball plan currently listed

These are the AS3-generation Eyeball plans as published in DMIT's recent Los Angeles restocks. All include 1 IPv4 plus an IPv6 /64, KVM virtualization and NVMe storage.

| Plan | vCPU | RAM | SSD | Port / monthly traffic | After quota | Price (monthly) | Order |
| --- | --- | --- | --- | --- | --- | --- | --- |
| LAX.EB.TINY | 1 | 2 GB | 20 GB | 2 Gbps / 1.5 TB | 4 Mbps unmetered | $10.90 | [See the EB.TINY plan](https://www.dmit.io/aff.php?aff=12046) |
| LAX.EB.Pocket | 2 | 2 GB | 40 GB | 4 Gbps / 3 TB | 4 Mbps unmetered | $16.90 | [See the EB.Pocket plan](https://www.dmit.io/aff.php?aff=12046) |
| LAX.EB.STARTER | 2 | 2 GB | 80 GB | 10 Gbps / 5 TB | 4 Mbps unmetered | $34.90 | [See the EB.STARTER plan](https://www.dmit.io/aff.php?aff=12046) |
| LAX.EB.MINI | 4 | 4 GB | 80 GB | 10 Gbps / 10 TB | 8 Mbps unmetered | $62.90 | [See the EB.MINI plan](https://www.dmit.io/aff.php?aff=12046) |
| LAX.EB.MICRO | 4 | 4 GB | 160 GB | 10 Gbps / 14 TB | 8 Mbps unmetered | $87.90 | [See the EB.MICRO plan](https://www.dmit.io/aff.php?aff=12046) |
| LAX.EB.MEDIUM | 6 | 8 GB | 160 GB | 10 Gbps / 30 TB | 10 Mbps unmetered | $199.90 | [See the EB.MEDIUM plan](https://www.dmit.io/aff.php?aff=12046) |

Billing is not monthly-only — DMIT offers quarterly, semi-annual and annual cycles on most plans, and the discount structure changes with the cycle. The per-month figures above are the monthly list prices, which is the honest way to compare them against each other.

Two things worth noticing in that table. First, EB.MINI and EB.MICRO have identical CPU and RAM but different disk and traffic allocations — the $25 gap buys 80 GB of extra SSD and 4 TB more monthly transfer, nothing else. Second, EB.STARTER is the awkward one: it costs exactly double EB.Pocket and doubles the disk and traffic, but RAM stays at 2 GB. If your workload is memory-bound rather than bandwidth-bound, that's a ceiling you'll hit before the traffic one.

## The annual restock tickets are a different product

Alongside the standard lineup, DMIT periodically releases limited annual Eyeball machines that sell out in hours. Third-party write-ups have documented them at these price points:

- **LAX.EB.WEE** — 1 vCPU, 1 GB RAM, 20 GB SSD, 1 TB/month, 1 Gbps: around $39.9/year
- **LAX.EB.CORONA** — 1 vCPU, 1 GB RAM, 20 GB SSD, 2 TB/month, 2 Gbps: around $49.9/year
- **LAX.EB.FONTANA** — 2 vCPU, 2 GB RAM, 40 GB SSD, 2.5 TB/month, 4 Gbps: around $100/year

Per gigabyte of memory these are the cheapest CMIN2 machines DMIT sells, and the trade-off is exactly what you'd expect: less RAM, lower port speed, and no guarantee of availability. They come back in waves. If the plan you want is out of stock, waiting is a legitimate strategy — but so is buying the standard EB.TINY, which costs more per year and is actually orderable today. 👉 [see what's currently in stock at DMIT](https://www.dmit.io/aff.php?aff=12046).

## Eyeball vs Premium vs Tier 1: the actual decision

**Pick Tier 1 only if your visitors aren't in China.** It runs international BGP with no China optimization, and the price reflects that — the annual WEE tier starts around $36.9/year. Buying T1 for a China-facing site and hoping is a common and expensive mistake.

**Pick Eyeball if China Mobile is your main audience.** You get CMIN2 both directions for mobile, real 9929 for Unicom, and a load-balanced premium path for Telecom. Under the same configuration the EB plans also carry noticeably more monthly traffic than Pro — TINY gives 1.5 TB against Pro's 1 TB, Pocket gives 3 TB against 1.5 TB. If you're moving large volumes and latency tolerance is measured in tens of milliseconds, EB wins on price-per-terabyte.

**Pick Premium if China Telecom is your main audience.** Pro returns over CN2 GIA (AS4809) for all three carriers, with outbound via GIA for Telecom, 9929 for Unicom and CMIN2 for Mobile. You pay for it: Pro.TINY starts around $10.90/month with less traffic than the EB equivalent, and the gap widens as configurations grow. The premium is worth it when your users are on Telecom broadband and you've seen what the shared return path does at peak. It isn't worth it for a personal proxy or a low-traffic side project.

A fair summary of the trade: Eyeball gives you two carriers at flagship quality and one at "very good". Premium gives you three at flagship quality and charges accordingly.

## What you're getting beyond the route

Network quality is the headline, but a few non-network details decide whether the machine is pleasant to live with.

**Hardware.** Every plan runs on AMD EPYC silicon with NVMe storage. The AS3 platform uses EPYC 7003; newer AN4/AN5 stock uses 9004/9005 parts. Published benchmarks put single-core Geekbench 5 scores in the 1400s on the newer generations and disk throughput above 1 GB/s in large-block tests — more than enough for a web app, a build runner or a mid-sized WordPress install. The platform generation matters more than the plan tier for raw CPU performance, so if benchmarks are your priority, ask which platform your chosen plan sits on before ordering.

**Payments.** Alipay, WeChat Pay, PayPal and credit cards all work, which removes most of the friction for buyers outside the US.

**IP replacement.** Widely discussed, inconsistently described. Some write-ups state one free swap every 15 days with a $5 charge beyond that; others say the free allowance is monthly. Treat it as "DMIT will replace a blocked IP under some condition" and confirm the current terms in your client area before you rely on it.

**Refunds.** Third-party guides cite a 3-day full-refund window (with traffic under roughly 30 GB) and pro-rated refunds up to 30 days. Same caveat — verify against the official terms, because refund policy is exactly the kind of thing that changes without a public announcement.

**Streaming and IP reputation.** Results vary by IP, and anyone promising you Netflix 4K on an EB machine is overselling. Test results that were published for EB IPv4 addresses showed Netflix, Disney+ and similar services *not* unlocking, while ChatGPT and TikTok generally worked. The IPv6 block behaved slightly differently again. If streaming unlock is your primary requirement, budget the time to test the actual IP you receive during the refund window.

## Promo codes: read the date before you type one

Every DMIT coupon list you'll find is a snapshot. The codes circulating in older write-ups carry date-stamped prefixes — launch codes for the EB line, Christmas campaign codes with a 2025 prefix — and date-stamped codes behave exactly like you'd expect. A few examples of the pattern, so you know what you're looking at when you find one: a launch-era quarterly-and-up discount code, a Christmas annual-recurring percentage code, and Tier 1 codes tied to a specific billing cycle.

The more reliable discount mechanism in practice is DMIT's own direct pricing. Several recent plan listings note built-in annual discounts applied automatically at checkout without a code — commonly a larger cut on the lowest tier and a smaller one on the rest. That's the number to compare across billing cycles.

Practical approach: build the order monthly first and see the base price, then switch the billing cycle to annual and watch what the cart does. Whatever the cart applies is real; whatever a forum post from last year claims may not be.

## Questions that come up before checkout

**Does China Telecom suffer on Eyeball?** Not badly. Return traffic for Telecom is load-balanced across AS9929 and CMIN2, both premium paths. It's less deterministic than Pro's dedicated GIA return, which shows up as slightly more variance at peak rather than a dramatic slowdown.

**Is 1.5 TB a month enough?** For a website, a development environment or light proxying, comfortably. For video relaying or a busy download node, no — and remember that once you exceed it you're at 4 Mbps, which is fine for a remote shell and painful for anything interactive.

**Can I upgrade later?** DMIT supports plan changes, but confirm how the change affects your renewal price. There have been documented cases where touching an existing service — upgrading it or changing the billing cycle — moved it onto current pricing. Machines bought earlier have kept their original renewal rates as long as the customer didn't modify them.

**Monthly or annual?** Pay monthly for the first cycle. The line quality is the thing you're buying, and it's worth one billing cycle of your own latency data before committing a year. That said, if you already know you're on China Mobile and have been unhappy with a standard-BGP US VPS, the annual EB tickets are the value play when they're in stock.

## The short version

CMIN2 is the China Mobile piece of a three-backbone bundle. On DMIT's Eyeball plans you get a genuine CMIN2 round trip for Mobile, proper 9929 for Unicom, and a load-balanced premium return for Telecom, plus more monthly traffic than the CN2 GIA Premium line at a lower sticker price. It's the right buy if Mobile is your biggest audience or you're moving a lot of data; Premium is the right buy if Telecom dominates your traffic and you want the return path nailed down rather than balanced.

The standard EB lineup starts around $10.90/month for 2 GB of RAM and 1.5 TB of transfer, and the limited annual tickets undercut that substantially when they're available. If you want to see what's actually orderable right now rather than what a forum post promised last season: 👉 [go straight to DMIT's current Los Angeles plans](https://www.dmit.io/aff.php?aff=12046).

One last piece of advice that applies to every provider selling premium routes: pull a traceroute from your own connection during peak hours before you renew anything. Regional routing differences between Beijing, Shanghai and Guangdong are real, and your own trace beats any plan comparison table — including this one.
