---
title: "ping0 Risk Score Explained: How to Read Native IP, Broadcast IP, and Shared Users Count"
description: A field-by-field guide to the ping0 report, based on ping0's own documentation, with what to check for your use case and rule-of-thumb score ranges.
keywords: ping0 risk score explained, ping0 native IP vs broadcast IP, ping0 shared users count, ping0 IP type residential IDC, how to read ping0 report, clean residential IP, static residential proxy
author: GetIPProxy Team
series: The Static Residential Proxy Buyer's Guide
order: 5
date: 2026-11-11
lastmod: 2026-11-11
---

# ping0 Risk Score Explained: How to Read Native IP, Broadcast IP, and Shared Users Count

> **Who this is for:** Anyone using ping0 to check a static residential IP, especially social media managers, cross-border e-commerce sellers, and agencies whose clients "only trust ping0."
> **What you'll learn:** What every field on a ping0 report means, which fields you must check and which you can skip, and how to decide whether an IP works for your use case.
> **Reading time:** about 15 minutes
> **Series:** Part 5 of 11 · Core path: fields

---

## Key takeaways

- Start with IP Type, Risk Score, native IP / broadcast IP, and Shared Users Count. To see whether the address range has changed recently, check the Autonomous System Number (ASN), organization, and registration country history.
- ping0 labels IP Type as Residential or IDC (datacenter) based on its read of how the IP range is used.
- The lower the Risk Score, the lower the risk ping0 sees. It calls under 15 "extremely clean," 15–25 "clean," and 25–40 "neutral." Before you buy, also look at the network type and other test results.
- ping0's Residential label also covers business broadband and campus networks. A Shared Users Count of 1–10 still doesn't tell you whether the vendor commits to making the IP dedicated.
- ping0 is a third-party assessment, not any platform's internal score. After checking ping0, get a second opinion from IPQS or Scamalytics.

---

## What ping0 is and which questions it answers

ping0.cc is one of the most popular all-in-one IP checkers among Chinese-speaking users. Web lookups are free (after a CAPTCHA), and it also offers a paid API.

Compared with other tools, it stands out in three ways:

1. **It labels IP type by actual use:** According to ping0, it manually labels every IP range to distinguish whether the IPs are actually used on home broadband or in a datacenter.
2. **Its geolocation comes from its own latency measurements:** It probes the target IP from nodes around the world, takes the location with the lowest latency as the IP's location, and gives a confidence score.
3. **It shows ownership history:** ASN, organization, and registration country history, plus BGP topology history, so you can see an IP's track record.

**Good for answering:** What kind of network does ping0 say this IP is on? Native or broadcast? Which tier do the Risk Score and Shared Users Count fall in? Has the ASN, organization, or registration country changed recently?

**Not good for answering:** How the IP scores for fraud under the risk systems widely used by platforms in North America and Europe (use IPQS for that), or how fast the connection is (test that separately).

![Sample ping0 report (English interface, with a probe time of 2026-11-08 23:56)](images/ping0.png)

*A sample ping0 report in English. The page shows a probe time of 2026-11-08 23:56, and the IP address is partially masked. Key fields include IP Location, ASN Owner, Organization, IP Type (here, Residential), Risk Score, Native IP, LLM Detection, Shared Users Count, and Use Cases.*

How to read the key fields in this report: the location is Los Angeles, US, with all three confidence bars full; IP Type is Residential; the Risk Score is 1%, which is "extremely clean"; it's a native IP; and the Shared Users Count is 1–10. The sections below explain what each field means and where its limits are.

---

## Every field, explained

Each field is covered in three steps (what it is → in plain terms → what it means for you) and rated by importance: ★★★ must-check / ★★ useful / ★ safe to skip.

### 1. IP Location ★★★

**What it is:** The country, state or province, and city where the IP is located, each with a confidence score from 0 to 100. The data comes from ping0's own active measurements: it probes the target IP from nodes around the world, and the location with the lowest latency is taken as the IP's location.

**In plain terms:** Most databases look up the address on file; ping0 sends someone to knock on the door and see where the IP actually is.

**What it means for you:**
- The higher the confidence, the more reliable the location. If city-level confidence is low, don't take the city at face value.
- ping0 says **location accuracy drops when the target IP blocks ping or is offline.**
- Disagreeing with other geolocation databases is common. Go with what most sources say, and treat the location the target platform shows as the final word (see Part 4).

### 2. ASN and ASN Owner ★★

**What it is:** Which network currently announces the IP range this IP belongs to, and which organization that ASN is registered to.

**In plain terms:** An ASN is like a network's ID number. Once you have the number, you can look up which organization uses it.

**What it means for you:**
- The ASN tells you about **network ownership**. It says nothing about how clean the IP is or how good the connection is.
- Don't assume a particular ASN is "safer." Whether you need to specify an ASN depends on whether your work explicitly requires one.
- Part 8 covers ASN types, history, and the differences between the major US ISPs in detail.

### 3. Organization ★★

**What it is:** The company or organization the IP belongs to. It's usually the same as the ASN Owner, but it can be a subsidiary or a customer.

**What it means for you:** It mainly helps you judge where the IP comes from and how it's used. Checking the organization history for frequent changes tells you more than the current value alone.

### 4. IP Type ★★★

**What it is:** ping0 uses only two categories: **Residential** and **IDC**. Its official definition: "IDC IP" refers specifically to IPs dedicated to datacenters, and every other IP is labeled "Residential."

**In plain terms:** This is the occupation box ping0 fills in for the IP, and it doesn't go by the company name on the badge. It goes by where the person actually shows up to work every day.

**What it means for you:**
- Some databases label the network as an internet service provider (ISP), while ping0 labels the same IP IDC. ping0 gives an example: an ISP's IPs can also be used on datacenter servers.
- **Residential doesn't necessarily mean home broadband.** ping0 states plainly that every IP that isn't a datacenter IP is labeled Residential, including business broadband and campus networks.
- **Accuracy is about 95%.** ping0 explains that because IPs change every day, IPs that changed recently and haven't been relabeled yet may be off. To spot this, check the "first seen" dates in the ASN and organization tables. Recent entries suggest the ownership or status may have just changed.

### 5. LLM Detection ★

**What it is:** An AI-based check ping0 runs on IPs labeled Residential to tell whether they're actually business broadband. ping0 says the model is fine-tuned from qwen2.5-0.5b.

**What it means for you:** Only look at it if you specifically need to separate residential broadband from business broadband. For most kinds of work, treat it as a reference.

### 6. Risk Score ★★★

**What it is:** How risky the IP is; the higher the number, the higher the risk. ping0 uses big data to monitor whether an IP is involved in scanning, brute-force attacks, crawling, attacks on other hosts, sending spam, or acting as a malware command-and-control (C&C) server, and scores it on how often and how frequently those behaviors occur.

ping0's official tiers:

| Risk Score | Level | Color on the page |
|---|---|---|
| Under 15 | Extremely clean | Dark green |
| 15–25 | Clean | Green |
| 25–40 | Neutral | Yellow-green |
| 40–50 | Slight risk | Yellow |
| 50–70 | Elevated risk | Orange |
| Above 70 | Extreme risk (can be blocklisted outright) | Red |

ping0's documentation calls anything under 50 "safe" and recommends blocklisting IPs above 70. The traffic lights below follow this series' buying rules of thumb.

**In plain terms:** The Risk Score is like a score based on the records on file. A low score means ping0 found low risk on this check.

**What it means for you:**
- **The Risk Score has no direct connection to whether an IP is residential.** ping0 states plainly that a residential IP used for scanning or brute-forcing will score high, and a datacenter IP with no malicious record can score very low. So read it together with IP Type; one can't stand in for the other.
- For most kinds of work, there's little difference between extremely clean (under 15) and clean (15–25). If your work has no explicit maximum score, you don't need to chase the lowest number.
- The ping0 Risk Score and the IPQS fraud_score **use different scales and can't be converted.**

### 7. Native IP / Broadcast IP ★★★

**What it is:** ping0 compares the registration country with the country it detects. If they match, the page shows **native IP**. If they don't, the page shows **broadcast IP**.

ping0's explanation: most residential broadband IPs are native, and some local datacenter providers' IPs are native too. Some multinational providers, for easier management, buy large IP blocks and announce them for use in different countries; those are broadcast IPs.

**In plain terms:** A native IP is registered locally and lives locally. A broadcast IP is registered out of state but lives locally.

**What it means for you:**
- A local datacenter IP can also show as native. Check IP Type first, and if you need real home broadband, ask the vendor where the exit is connected.
- A broadcast IP's location is more likely to differ between tools, and it may change when databases update. **For work that needs a stable city-level location (local businesses, localization testing), a broadcast IP usually isn't a good fit.**
- Check the registration country history table. If the registration country has changed, confirm that the current registration country matches the country ping0 shows.

### 8. Shared Users Count ★★★

**What it is:** ping0's estimate, based on data it found over the past 12 months, of how many unique users are linked to the IP. The page shows it in five tiers.

| Tier | What it usually means |
|---|---|
| 1–10 | Very few linked users (but this doesn't prove the IP is dedicated; see below) |
| 10–100 | A moderate number of linked users |
| 100–1000 | A fairly large number of linked users |
| 1000–10000 | Usually means the IP is shared by a large number of users |
| 10000+ | Usually means the IP is shared by a large number of users |

ping0 specifically notes that an IP shared by many people is usually a **public proxy or VPN** IP. Also, because NAT is so widely used in mainland China, ping0 **doesn't show Shared Users Count for mainland China IPs** by default.

**In plain terms:** Shared Users Count is roughly how many people have lived in this house over the past year. The more people, the more it looks like a shared rental or a motel.

**What it means for you:**
- A result of 1–10 only tells you ping0 estimates few linked users. A result of 1000–10000 or a higher tier means ping0 has seen a lot of linked users, so ask the vendor how the address is allocated before you buy.
- If your work needs a dedicated IP, make "the same IP will not also be assigned to other customers" a condition of the purchase. Use Shared Users Count as supporting evidence.
- Some in the Chinese-speaking technical community believe a WebRTC leak on the visitor's side, or visiting ping0 repeatedly from the same exit, may affect this number. That's community speculation, not an official statement, but it's a useful reminder: **rule out WebRTC leaks before you check, check once, and don't keep refreshing.**

### 9. Use Cases ★

**What it is:** ping0's judgment of which use cases suit the IP, based on its location, IP Type, and risk index.

**What it means for you:** ping0 says this assessment is **based on accumulated experience, isn't absolutely accurate, and real-world performance in your actual work should be the final test.** Glance at it, but don't base decisions on it. Parts 9 and 10 of this series give more specific methods by use case.

### 10. ASN history, organization history, and registration country history ★★★ (the most overlooked)

**What it is:** Three history tables recording which ASNs and organizations the IP has belonged to, and how its registration details at the RIR have changed. Every entry has a "first seen" date.

ping0's reasoning: **residential broadband IPs usually stay with the same ASN and organization for a long time and rarely change. When the ASN, organization, or registration details change often, the IP's ownership is unstable, and it's usually called a "dirty" IP.**

**In plain terms:** These three tables are the IP's employment history and change-of-address record. Someone with a clear, steady history has an easier time passing a background check.

**What it means for you:**
- This is the most direct evidence of **long-term stability,** and it's the part most people never look at.
- A recent entry suggests the ownership may have just changed, in which case ping0's IP Type label may not have caught up yet.
- An IP range can be announced by more than one ASN at the same time. If you see several entries in a table, check the "first seen" dates first, then check whether it has switched back and forth recently.

### 11. Same-datacenter providers / customers and BGP topology history ★

**What it is:** The first shows companies in the same datacenter and on the same line as the IP (not in the same IP range). The second records snapshots of changes to the IP's BGP network topology (ping0 says recording began on February 7, 2026).

**What it means for you:** These are fairly technical and mainly useful to experienced users analyzing where the network comes from. Most users can skip them.

### 12. CDN tag ★

**What it is:** CDN or reverse proxy IPs ping0 has identified, such as "CloudFlare reverse proxy IP" or "Akamai CDN IP."

**What it means for you:** Residential IPs generally don't carry these tags. If one shows up, the IP very likely isn't the residential IP you think it is, and you should check with the vendor.

---

## Known limits: what ping0 can and can't do

1. **It's a third-party assessment, not a platform's internal score.** E-commerce, social media, and ad platforms don't disclose their data sources. ping0's conclusions are a useful reference, not the platform's verdict.
2. **IP Type is about 95% accurate** (per ping0), and IPs that changed recently may be off.
3. **Residential includes business broadband, campus networks,** and other non-datacenter IPs.
4. **Shared Users Count is an estimate,** and a low number doesn't prove much.
5. **IP Location depends on latency measurement,** so accuracy drops for IPs that block ping or are offline.
6. **The algorithm isn't public.** Its accuracy is debated in the community, and some users report wrong city locations for certain IPs. That's why this series always recommends cross-checking ping0's conclusions against other tools.

---

## How to use ping0 the right way

1. **Confirm the exit first:** Use a tool like ip.me to confirm your current exit is the IP you mean to test, and turn off or rule out WebRTC leaks.
2. **Check once, screenshot, note the date:** Don't keep refreshing from your production exit.
3. **Start with the four core fields:** IP Type, Risk Score, native / broadcast, and Shared Users Count.
4. **Then check the three history tables:** Focus on the "first seen" dates and how often things change.
5. **Cross-check:** At minimum, confirm the risk information with IPQS or Scamalytics, and confirm the location with other geolocation databases (Part 4).

---

## Which fields matter for your use case

| Reader | Must check | Can relax | Watch out for |
|---|---|---|---|
| A: Social media managers running accounts long-term | IP Type, Risk Score, Shared Users Count | City-level location | If you need it dedicated, read the purchase terms first; use Shared Users Count only as supporting evidence |
| B: Cross-border e-commerce sellers | IP Type, Risk Score, native / broadcast, location (country / state) | City-level accuracy (depends on the platform) | Check the platform's and your team's location requirements first, then confirm the country or state in the report |
| D: Ad account managers and media buying teams | Risk Score, IP Type | City-level location | Beyond the Risk Score, also check IPQS for recent abuse |
| C: Local businesses serving a specific city | Location (including confidence), native / broadcast, registration country history | A Risk Score anywhere in the "clean" tier is fine | Broadcast IPs usually aren't a good fit |
| E: Agencies and overseas VA teams | IP Type, Shared Users Count, ASN and its history | City accuracy for individual IPs | When buying in bulk, check whether many IPs sit in the same ASN or IP range |
| F: Testers running long-term checks in a fixed region | Location, IP Type, the three history tables | Risk Score | What matters is that nothing changes over time; compare against history when you recheck |

---

## Rule-of-thumb ranges

The table below is based on ping0's official tiers and documentation. These are **rules of thumb,** not official standards or any platform's pass line:

| Field | 🟢 Green | 🟡 Yellow | 🔴 Red |
|---|---|---|---|
| Risk Score | ≤ 25 | Above 25 and no higher than 50 | > 50 |
| IP Type | Residential | Shows IDC, but most other tools identify it as residential / ISP | Shows IDC, and most other tools also identify it as datacenter |
| Native / broadcast | Native IP | Broadcast IP (for work that only needs country-level location) | Broadcast IP (for work that needs city-level location) |
| Shared Users Count | Shows 1–10; whether it's dedicated still depends on the purchase terms | Shows 10–100 | Shows 100–1000 or a higher tier |
| History tables | Stable long-term, no recent changes | One recent change | Frequent recent changes; the registration country has changed |
| CDN tag | None | — | A CDN / reverse proxy tag appears |

**How to use it:** Look for red first; a red light usually means asking for a replacement. If there's no red, decide whether any yellow is acceptable for your work (see the use case table in the previous section).

---

## Don't want to test IPs one by one?

By now you should be able to look at a ping0 report and decide whether an IP's Risk Score, IP Type, native status, and Shared Users Count fit your work. In practice, though, the most time-consuming part of buying is testing and filtering IPs one at a time.

If you'd rather skip that step, browse GetIPProxy's [clean residential proxies by ping0 Risk Score](https://getipproxy.com/static-residential-proxies/clean-ips/). For each location, the page lists the Risk Score range based on ping0's assessment, the cleanliness tier (Ultra-Clean IP / Clean IP), and the ASN. <!-- REVIEW: confirm the English tier labels used on the GetIPProxy page --> The inventory is drawn only from native residential IPs and doesn't include broadcast residential. When you choose, compare against the ranges above.

Risk Scores change over time. After delivery, check again with IPQualityScore or Scamalytics, and save the screenshots and the date. You can compare against them when you recheck later (see Part 11 for how).

---

## FAQ

**Q: ping0 says IDC. Does that mean I can't use the IP?**
Not necessarily. First see what other tools say. If most of them identify it as residential / ISP, it's a difference in definitions (ping0 looks at actual use, other tools look at ownership), and it's a yellow light. Then check the "first seen" dates in the history tables; for an IP that changed recently, ping0's label may not have caught up. But if your client or team goes by ping0, simply follow ping0's verdict.

**Q: Is there a big difference between a Risk Score of 5 and a Risk Score of 20?**
Both fall within ping0's clean range (under 15 is extremely clean, 15–25 is clean). For most kinds of work, the difference is small. IP Type, Shared Users Count, and history stability deserve more attention than chasing the lowest score.

**Q: Does a Shared Users Count of 1–10 prove I'm the only one using the IP?**
No. ping0 says it's an estimate, and a low number may just mean limited observed data. It's only circumstantial evidence. "Dedicated" should be written into the purchase terms as a commitment from the vendor.

**Q: Is a native IP always home broadband?**
ping0 labels an address native when its registration country matches the country ping0 shows, and a local datacenter IP can qualify. If you need real home broadband, check IP Type too, and ask the vendor where the exit is connected.

**Q: My client only trusts ping0 and won't look at other tools. What should I do?**
Ask the client which ping0 fields they care about and what counts as passing for each. You can also run the IP through IPQS and save the result. If an account runs into trouble later, use that record to check the exit, then look at the device, account profile, and activity history (see "Three things a clean IP can't do" in Part 2).

---

## What to read next

- [Part 6: IPQualityScore report, field by field](06-ipqualityscore-field-guide.md): confirm the risk from a different angle
- [Part 4: IP checkers compared](04-ip-checker-platforms.md): what to do when ping0 disagrees with other tools
- [Part 8: ASNs and ISPs](08-asn-and-isp.md): a closer look at ASNs and ownership history
- [Part 9](09-scenarios-accounts-stores.md) and [Part 10](10-scenarios-regions-teams.md): decide by use case

---

> This is Part 5 of *The Static Residential Proxy Buyer's Guide*, written by the [GetIPProxy](https://getipproxy.com/) team. ping0 field definitions follow [ping0's official FAQ](https://ping0.cc/ip/faq). Sources checked November 11, 2026. Test results change over time.
