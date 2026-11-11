---
title: "IPQualityScore Fraud Score Explained: How to Read fraud_score, proxy, and recent_abuse"
description: What a good IPQS Fraud Score is, the right order to read the report, and what proxy, vpn, recent_abuse, connection_type, and 20+ other fields mean.
keywords: IPQualityScore fraud score meaning, what is a good IPQS fraud score, IPQS recent_abuse, IPQS proxy flag, IPQS connection_type, IP fraud score, IP risk score, static residential proxy
author: GetIPProxy Team
series: The Static Residential Proxy Buyer's Guide
order: 6
date: 2026-11-11
lastmod: 2026-11-11
---

# IPQualityScore Fraud Score Explained: How to Read fraud_score, proxy, and recent_abuse

> **Who this is for:** Anyone using IPQualityScore (IPQS) to check a static residential IP, especially cross-border e-commerce sellers, media buyers, and teams checking IPs in bulk through the API.
> **What you'll learn:** What every field on an IPQS report means, the right order to read the report in, and how to decide whether an IP works for your use case.
> **Reading time:** about 15 minutes
> **Series:** Part 6 of 11 · Core path: fields

---

## Key takeaways

- The IPQS website divides the Fraud Score (`fraud_score`) into 0–39 low risk, 40–75 suspicious, 76–84 risky, 85–89 high risk, and 90–100 fraud. When buying, this series treats 0–39 as the low-risk range and reads it together with other fields.
- First check whether the report shows fields like `recent_abuse`, `proxy`, and `tor`. Go through each one to see whether it's `true` or `false`, then look at the score.
- `recent_abuse=true` means IPQS reported recent confirmed abuse. When you're choosing an IP for accounts, stores, or payments, treat it as a red light.
- `mobile` looks at the browser user agent. If a field is blank or says it requires a paid plan, record it as "not found." The same IP queried with different parameters can return different scores.
- IPQS is a third-party assessment, not any platform's internal score, and it doesn't measure connection speed. After checking IPQS, get a second opinion from ping0 or Scamalytics.

---

## What IPQS is and which questions it answers

IPQualityScore is a fraud detection provider that a large number of websites use to assess risk at sign-up, sign-in, and checkout. Its data comes mainly from **honeypots and fraud traps** it runs in more than 150 countries, which continuously capture fake sign-ups, account takeovers, bots, proxies, VPNs, and similar traffic.

It offers free web lookups (with a monthly free quota) and an API. The web lookup and the API don't return exactly the same fields, and some fields (which IPQS labels Enterprise Data Points) require a higher-tier paid plan.

**Good for answering:** Has this IP been abused? Recently? Is it identified as a proxy, VPN, or Tor? How risky does a major risk provider used across North America and Europe consider it?

**Not good for answering:** Whether the IP is *actually used* on home broadband (ping0 labels by actual use, which is a different definition), whether it's native or broadcast, or how fast the connection is.

![Sample IPQS web lookup report (2026-11-11)](images/ipqualityscore.png)

*The lookup time shown is 2026-11-11 22:35 (GMT+8), and the IP address is partially masked. The Fraud Score is 93, Proxy and VPN are both True, and Recent Abuse is False. Connection Type and Abuse Velocity show that a paid plan is required, so record those two as "not found" when you read the report.*

---

## Start with the score: the official fraud_score tiers

The IPQS Fraud Score (`fraud_score`) runs from 0 to 100. The higher the score, the higher the risk IPQS sees. Here are the tiers it publishes on its website.

| fraud_score | Risk level | IPQS's description |
|---|---|---|
| 0–39 | Low risk | Little to no evidence of fraud or abuse |
| 40–75 | Suspicious | Some signs of risk; may need further review |
| 76–84 | Risky | A higher likelihood of suspicious activity or abuse |
| 85–89 | High risk | Strong evidence tied to fraud |
| 90–100 | Fraud | A very high likelihood of fraud, abuse, automation, or malicious activity |

The IPQS website notes that most legitimate users' IPs have a Fraud Score below 40. The API documentation treats 75 and above as suspicious and recommends flagging or blocking traffic at 90 and above. When you're buying IPs, use this series' traffic-light rules of thumb.

**Why is your score different from someone else's?**

- The IPQS API supports a `strictness` parameter. IPQS says higher strictness levels run deeper checks but may also produce more false positives. You can also pass the browser user agent, language, and other details for evaluation.
- The web lookup and API calls with different parameters can return different scores.
- Scores change in real time as new abuse data comes in.

So **when you record a score, also record how you ran the lookup and the date.**

---

## The right order to read the report

When you get an IPQS report, first see which fields actually returned results, then read in this order:

1. **Confirm the lookup succeeded.** If a field is blank or says it requires a paid plan, record it as "not found."
2. **Start with the fields that have results.** Begin with `recent_abuse`, then `proxy`, `vpn`, `tor`, `active_vpn`, `active_tor`, and `bot_status`.
3. **Then look at the score:** use `fraud_score` to compare risk levels.
4. **Check the network and location.** Look at `connection_type`, the internet service provider (ISP), the Autonomous System Number (ASN), and the country and city in the report.
5. **Test on the target platform** and recheck periodically while you use the IP.

If you see `recent_abuse=true`, treat it as recent abuse first, even if the score is low. Whether an account passes review still depends on how the platform you sign in to judges it.

---

## Every field, explained

Each field is covered in three steps (what it is → in plain terms → what it means for you) and rated by importance: ★★★ must-check / ★★ useful / ★ safe to skip.

### Core score

#### fraud_score ★★★

**What it is:** The overall Fraud Score, from 0 to 100. According to IPQS, it's calculated from the IP, user agent, language, and any other variables you optionally pass in.

**In plain terms:** Read it as a risk score. The lower it is, the lower the risk IPQS saw on this lookup.

**What it means for you:**
- The IPQS website lists **0–39** as low risk. When buying, also check the fields below.
- **40–75** is a yellow light in this series' buying table. Check for recent abuse first, then decide based on what your work requires.
- **76 and above** counts as red in this series' buying table.
- The IPQS score and the ping0 Risk Score **use different scales and can't be converted.**

### Proxy detection

#### proxy ★★★

**What it is:** Whether the IP is suspected of being a proxy (including SOCKS, anonymous proxies, VPNs, Tor, and so on).

**In plain terms:** Whether IPQS spotted signs of a middleman on this IP.

**What it means for you:**
- You are in fact using the static residential IP over a proxy protocol, but `proxy` tells you whether **IPQS has identified this exit IP as a proxy.** It's not unusual for residential proxy IPs to be flagged `proxy=true`.
- If your team explicitly requires `proxy=false` when buying, check this field first, then compare scores among the addresses that meet the requirement.
- `proxy=false` only means IPQS didn't identify it at the time of the check. It doesn't mean other tools, or later checks, will reach the same conclusion.

#### vpn ★★

**What it is:** Whether the connection is suspected of being a VPN. IPQS says this can include datacenter IP ranges that could become active VPNs at any time; when `vpn=true`, `proxy` is always true as well.

**What it means for you:** `vpn=true` on a residential IP is a warning sign. It may have been grouped into a VPN- or datacenter-related IP range.

#### tor ★★

**What it is:** Whether the connection is suspected of being Tor, including formerly active Tor nodes; when `tor=true`, `proxy` is always true as well.

**What it means for you:** A static residential IP should never show `tor=true`. If it does, ask for a replacement right away.

#### active_vpn / active_tor ★

**What it is:** Whether the IP is identified as a **currently active** VPN service or Tor exit.

**What it means for you:** Use it to confirm current status. Note that `active_vpn=false` doesn't cancel out `vpn=true`; the latter may reflect how the IP range is classified, or historical signals.

### Abuse history

#### recent_abuse ★★★

**What it is:** Whether the IP has had confirmed abuse on the IPQS network **in the last few days.** The types of abuse IPQS lists include confirmed chargebacks, account takeover attempts, compromised devices, fake applications or sign-ups, identity theft, and bot attacks.

**In plain terms:** You're looking at the abuse IPQS has confirmed over the last few days.

**What it means for you:**
- When you're buying an IP for accounts, stores, or payments, treat `recent_abuse=true` as a red light.
- `recent_abuse=false` means IPQS didn't report recent confirmed abuse on this lookup. If the field isn't shown, record it as "not found."

#### abuse_velocity ★★

**What it is:** How often the IP takes part in abuse on the IPQS threat network: high, medium, low, or none.

**What it means for you:** Read it together with the score. If it says a paid plan is required, that means you can't see it, not that the value is none.

#### bot_status ★★

**What it is:** Whether bots or non-human traffic have recently used this IP for automated fraud. IPQS says it provides stronger evidence that an IP is suspicious.

**What it means for you:** A static residential IP should be false. If it's true, the IP was recently used for automated activity and isn't suitable for account-based work.

#### frequent_abuser ★★ (Enterprise field)

**What it is:** IPs with ongoing abuse over 6 months or longer. IPQS says it separates IPs used for malicious activity over the long term from IPs briefly infected by malware or temporarily pulled into a botnet or residential proxy network.

**What it means for you:** Very useful when you can see it. If it's true, the problem is long-term, and we don't recommend using the IP.

#### high_risk_attacks ★★ (Enterprise field)

**What it is:** Whether the IP has been confirmed to take part in malicious attacks such as phishing, brute-force attacks, DDoS, credential stuffing and account takeover, scraping, or form spam.

**What it means for you:** If it's true, rule the IP out.

#### abuse_events ★ (Enterprise field)

**What it is:** Details about recent abuse events and proxy networks associated with the IP.

**What it means for you:** Useful for deeper investigation; most users won't see it.

### Network attributes

#### connection_type ★★★

**What it is:** The IP's connection type: Residential, Corporate, Education, Mobile, or Data Center.

**In plain terms:** The occupation box IPQS fills in.

**What it means for you:**
- Ideally, a static residential IP shows Residential.
- Data Center means IPQS thinks it belongs to a datacenter, which doesn't match what you'd expect from "residential." Cross-check it against other tools.
- IPQS gives the connection type here. ping0's IP Type is based on its read of how the IP range is used. If the two disagree, see the conflict cases in Part 4.

#### ISP / Organization / ASN ★★

**What it is:** The network provider associated with the IP, the operating organization (which may be the ISP's parent company or a subsidiary), and the Autonomous System Number currently announcing the IP.

**What it means for you:**
- Use them to check network ownership. The three may not match exactly, so read them together.
- The ASN is a clue to network ownership, **not a grade of cleanliness or connection quality.** Part 8 covers ASNs in depth.

#### host ★

**What it is:** The IP's hostname (from reverse DNS), if it has one.

**What it means for you:** If the hostname clearly points to a server or hosting provider, it's worth checking further. But plenty of IPs have no hostname or only a generic one. That's common, so don't read too much into it.

### Sharing and network environment (Enterprise fields)

#### shared_connection ★★

**What it is:** Whether the IP is likely used by more than a few users at the same time, such as mobile networks, corporate egress points, libraries, coffee shops, hotel lobbies, dorms, hospitals, and corporate VPNs.

**In plain terms:** IPQS's call on whether the IP "has roommates."

**What it means for you:** If you're buying a dedicated IP and see `shared_connection=true`, also check ping0's Shared Users Count, and ask the vendor to confirm whether the same address has been assigned to other customers.

#### dynamic_connection ★

**What it is:** Whether the IP is dynamically assigned, meaning the user may be assigned a different IP before long.

**What it means for you:** `true` means IPQS thinks the connection uses dynamic assignment. Whether the exit you bought changes during the agreed term, and whether you keep the address on renewal, still comes down to the purchase terms.

#### trusted_network ★

**What it is:** Whether the IP belongs to an enterprise network or corporate access point with low abuse rates and strict security.

**What it means for you:** Mainly relevant for corporate networks; residential IPs generally aren't affected.

#### security_scanner ★

**What it is:** Whether the IP is a scanner or endpoint belonging to a trusted security vendor (such as Tenable or Qualys).

**What it means for you:** Residential IPs are generally false here; you can skip it.

### Other fields

#### is_crawler ★

**What it is:** Whether the IP is a verified crawler for a search engine or well-known service (such as Google or Bing).

**What it means for you:** Residential IPs are generally false here; you can skip it.

#### mobile ★ (often misread)

**What it is:** IPQS defines it as **"whether this user agent is a mobile browser."** If you don't pass a user agent with the lookup, it's always false.

**What it means for you:** **It describes the browser, not the IP.** Don't use it to decide whether an IP is on a mobile network; for that, check whether `connection_type` is Mobile.

#### country_code / region / city / zip_code / timezone / latitude / longitude ★★

**What it is:** The country, state / region, city, ZIP code, time zone, and coordinates inferred from the IPQS database.

**What it means for you:**
- Use them to confirm the IP matches your target region. IPQS notes that an IP may map to several ZIP codes within a city and recommends analyzing nearby, similar ZIP codes.
- City-level location often varies between databases; cross-check using the method in Part 4.
- The time zone lets you check whether your device's time zone setting matches the IP (Part 11).

#### request_id / success / message ★

**What it is:** The request ID and request status.

**What it means for you:** They say nothing about IP quality, but keep the request_id if you need to ask IPQS about a particular result.

---

## Common misreadings at a glance

| Misreading | What it actually means |
|---|---|
| "A low score means there's no problem." | Check `recent_abuse` first. If it shows `true`, treat it as red when buying |
| "I'm using a proxy, so `proxy=true` doesn't matter." | `proxy` tells you whether IPQS flagged this exit as a suspected proxy. If your team has a buying requirement for this field, choose by that requirement |
| "`mobile=false` means it's not a mobile network." | `mobile` describes the browser user agent; check `connection_type` for mobile networks |
| "The field says a paid plan is required, so there's no risk." | Record it as "not found." Only a `false` result lets you treat that item as not detected |
| "My score doesn't match what the vendor told me, so someone must be faking it." | Different query parameters or lookup times can both produce different scores |
| "A low IPQS score means the platform will trust me." | IPQS isn't the internal score of any e-commerce, social media, or ad platform |
| "A low IPQS score means my livestream won't lag." | IPQS doesn't measure bandwidth, latency, or connection quality |

---

## Reading the fields together: when to use an IP and when to replace it

The table below gives this series' buying recommendations, combining the IPQS website tiers with the fields in the report.

| Combination | Verdict | Notes |
|---|---|---|
| fraud_score 0–39 + `proxy=false` + `recent_abuse=false` | 🟢 Green | These three meet this table's recommendation; then check type, location, and the purchase terms |
| fraud_score 0–39 + `proxy=true` + `recent_abuse=false` | 🟡 Yellow | Identified as a proxy; be careful with account-based work |
| fraud_score 40–75 + `recent_abuse=false` | 🟡 Yellow | Confirm with ping0 and Scamalytics, then decide based on your work |
| `connection_type=Data Center` | 🟡 / 🔴 | Doesn't match what you'd expect from residential; treat as red if most other tools also say datacenter |
| `vpn=true` | 🟡 / 🔴 | Treat as red for account-based work |
| fraud_score ≥ 76 | 🔴 Red | Ask for a replacement |
| `recent_abuse=true` | 🔴 Red | Ask for a replacement, whatever the score |
| Any of `tor=true`, `bot_status=true`, `frequent_abuser=true`, `high_risk_attacks=true` | 🔴 Red | Ask for a replacement |

---

## Which fields matter for your use case

| Reader | Must check | Can relax | Watch out for |
|---|---|---|---|
| A: Social media managers running accounts long-term | `fraud_score`, `proxy`, `recent_abuse`, `connection_type` | City-level location | IPQS doesn't test upload bandwidth; test connection quality separately for livestreaming and short-form video |
| B: Cross-border e-commerce sellers | `recent_abuse`, `proxy`, `fraud_score`, country / state | City-level accuracy (depends on the platform) | The location should match your store details; rule out `recent_abuse=true` |
| D: Ad account managers and media buying teams | `fraud_score`, `recent_abuse`, `abuse_velocity`, `proxy` | City-level location | Where ads run is set by targeting in the ad account and has nothing to do with the IP |
| C: Local businesses serving a specific city | Country / state / city, `connection_type` | A score anywhere in the low-risk range is fine | For the city, go by what most databases say and what the target platform shows |
| E: Agencies and overseas VA teams | `proxy`, `recent_abuse`, ASN, `shared_connection` (if visible) | City accuracy for individual IPs | Well suited to bulk checks through the API; record query parameters consistently |
| F: Testers running long-term checks in a fixed region | Country / city, `connection_type` | Score | What matters is that nothing changes over time; use the same query parameters when you recheck |

---

## When IPQS and ping0 disagree

The two use different data sources, definitions, and scales, so disagreements are common:

- **IPQS says Residential, ping0 says IDC.** The two fields use different classifications. See how other IP checkers label it, and check the "first seen" dates in ping0's history tables.
- **IPQS scores high, but ping0's Risk Score is very low.** Check IPQS's `recent_abuse` first. If it shows `true`, treat it as red. If it shows `false` or the field wasn't found, you can check the risk score and blocklists on Scamalytics. When buying, still judge by the score ranges in the table above.

For the full method for handling conflicts, see [Part 4](04-ip-checker-platforms.md).

---

## Your second opinion

Whatever IPQS says, confirm with at least one other independent source:

- **For reputation history,** use Scamalytics. It shows a Fraud Score, a risk level, and hits on public blocklists such as Spamhaus and Firehol.
- **For type and ownership,** use ipinfo. Look at the ASN type and privacy detection (VPN, proxy, hosting, residential proxy).
- **For actual use and history,** use ping0. Look at IP Type, native / broadcast, Shared Users Count, and ownership history ([Part 5](05-ping0-field-guide.md)).

[Part 7](07-scamalytics-ipinfo-guide.md) walks through Scamalytics and ipinfo in detail.

---

## Don't want to test IPs one by one?

By now you should be able to look at an IPQS report and work through it in the right order to decide whether an IP suits your work. In practice, though, testing and ruling out IPs one at a time takes a lot of time, and the IPQS free quota is limited.

If your work explicitly goes by IPQS results, browse GetIPProxy's [clean residential proxies by IPQualityScore Fraud Score](https://getipproxy.com/static-residential-proxies/clean-ips/ipqualityscore/). Every IP on the page was filtered to meet the same conditions: a fraud_score in IPQS's 0–39 low-risk range, not flagged as a proxy or bot, and no recent abuse reports. Scores of 0–20 are labeled "Ultra-Clean IP" and 21–39 "Clean IP" (these are GetIPProxy's buying categories, not official IPQS tiers). <!-- REVIEW: confirm the English tier labels used on the GetIPProxy page --> That matches the green-light conditions in the table above.

IPQS scores change as new data comes in. After delivery, check again with Scamalytics or ping0, and save the screenshots and the date. Use them for comparison when you recheck later (see Part 11 for how).

---

## FAQ

**Q: Why do the free IPQS lookup and the API give different results?**
They show different fields, and the API lets you set parameters such as `strictness`, which can change the score. When you compare results, use the same lookup method.

**Q: Is a fraud_score of 0 completely safe?**
No. A score of 0 only means there are almost no risk signals within the data IPQS can observe. Also check fields like `proxy` and `connection_type`, and confirm with another tool. A platform's judgment of an account also involves the device, account profile, and behavior.

**Q: Can I still use a residential IP with `proxy=true`?**
First check whether your team agreed on `proxy=false`. If that's a requirement, choose by it. If not, look at recent abuse, network type, and location to decide whether the IP meets your needs.

**Q: Will the IPQS score change after I buy?**
Yes. Changes in abuse data, when you run the check, or your query settings can all change the score. Save your first result when you receive the IP, then recheck the same way (Part 11).

**Q: Can I convert an IPQS score into a ping0 Risk Score?**
No. They use different data sources and scales, so read each one by its own tiers.

---

## What to read next

- [Part 5: ping0 report, field by field](05-ping0-field-guide.md)
- [Part 4: IP checkers compared](04-ip-checker-platforms.md)
- [Part 7: Scamalytics and ipinfo, your second opinion](07-scamalytics-ipinfo-guide.md)
- [Part 9](09-scenarios-accounts-stores.md) and [Part 10](10-scenarios-regions-teams.md): decide by use case

---

> This is Part 6 of *The Static Residential Proxy Buyer's Guide*, written by the [GetIPProxy](https://getipproxy.com/) team. IPQS field definitions follow IPQS's official documentation. Sources checked November 11, 2026. Test results change over time.

**Sources**
- [IPQS IP Fraud Score Checker: score ranges](https://www.ipqualityscore.com/ip-fraud-score-risk-checker)
- [IPQS Proxy Detection API: response parameters](https://www.ipqualityscore.com/documentation/proxy-detection-api/response-parameters)
- [IPQS Proxy Detection: overview and request parameters](https://www.ipqualityscore.com/documentation/proxy-detection/overview)
