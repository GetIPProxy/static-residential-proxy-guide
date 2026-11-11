[English](README.md) | [简体中文](README.zh-cn.md)

# Static Residential Proxy Buyer's Guide: How to Find a Clean, Dedicated Residential IP

A **static residential proxy** gives you an exit IP that stays the same for the agreed term. Look the address up in an IP database and you'll usually see it labeled as residential broadband or an ISP network. So whether you sign in to your seller dashboard every day or rerun the same tests every few weeks, you keep going out through the same exit.

If you need the same exit over the long term, this guide shows you where to check an IP, how to read the reports, and which results make an IP right for your work.

```
What "clean" means  →  Which sites to check  →  Which fields to read  →  What each field means  →  How to choose for your use case
```

---

## Contents

| # | Article | What it covers |
|---|---|---|
| 01 | [What Is a Static Residential Proxy? What It Solves and What It Doesn't](docs/01-what-static-residential-ip-solves.md) | How it differs from rotating residential proxies, datacenter proxies, and VPNs; which use cases need one; and what to ask about IP sourcing and usage limits before you buy |
| 02 | [What Makes a Static Residential IP Clean? A Five-Dimension Model](docs/02-what-is-clean-ip.md) | The five things that make an IP "clean," and which ones matter most for your work |
| 03 | [ISP Proxy vs. Static Residential Proxy: What Native, Broadcast, Real Home Broadband, and Dedicated Mean](docs/03-proxy-ip-labels.md) | How to read product labels, and how to agree with the vendor before ordering on which checker to use and which results must pass |
| 04 | [IP Reputation Checkers Compared: Why Results Differ and Which One to Trust](docs/04-ip-checker-platforms.md) | What each IP checker can tell you, and how to cross-check when their results disagree |
| 05 | [ping0 Risk Score Explained: How to Read Native IP, Broadcast IP, and Shared Users Count](docs/05-ping0-field-guide.md) | How to read the Risk Score, native IP, and Shared Users Count |
| 06 | [IPQualityScore Fraud Score Explained: How to Read fraud_score, proxy, and recent_abuse](docs/06-ipqualityscore-field-guide.md) | How to read the Fraud Score (`fraud_score`), `proxy`, and `recent_abuse` |
| 07 | [Scamalytics and ipinfo Explained: A Second Opinion on IP Reputation](docs/07-scamalytics-ipinfo-guide.md) | How to recheck abuse history, network type, and ownership with another source |
| 08 | [What Is an ASN? How to Check Who's Behind an IP (US ISPs Explained)](docs/08-asn-and-isp.md) | How to look up an Autonomous System Number (ASN) and its history, and whether to specify an ISP when choosing an IP |
| 09 | [Choosing a Static Residential Proxy for Social Media, E-Commerce Stores, and Ad Accounts](docs/09-scenarios-accounts-stores.md) | How to decide whether an IP works for running social media accounts, stores, or ad accounts |
| 10 | [Static Residential Proxies for Local Businesses, Agencies, and Geo Testing](docs/10-scenarios-regions-teams.md) | How to verify the city a platform shows, check how a batch of IPs is spread across IP ranges, and log the exit for every test run |
| 11 | [After You Buy a Static Residential Proxy: Baselines, Leak Tests, Rechecks, and Troubleshooting](docs/11-long-term-maintenance.md) | How to set up, test for leaks, recheck, and renew after delivery, and where to start when something goes wrong |

---

## Where to start

| Who you are | Recommended reading |
|---|---|
| First-time buyer | 01 → 02 → 03 → 04 |
| Social media manager running overseas accounts long-term | 05, 06, 09, 11 |
| Cross-border e-commerce seller or authorized assistant | 05, 06, 08, 09 |
| Ad account manager or media buying team | 06, 07, 09 |
| Local business serving a specific city | 07, 08, 10 |
| Social media / e-commerce agency or overseas virtual assistant (VA) team | 05, 08, 10 |
| Localization or landing page regression tester | 07, 08, 10 |

---

## Core principles

1. **Judge whether an IP is "clean" on five counts:** type authenticity, geographic consistency, reputation history, exclusivity, and long-term stability.
2. **When results disagree, check with another source.** For location, compare several geolocation databases first, then see where the platform you actually use places the IP.
3. **Choose for the work in front of you.** For a local business, confirm the city first. If you need a dedicated IP, ask the vendor whether they'll assign the same IP to other customers.
4. **After delivery, save your first test results and the date.** That record is your **baseline.** If you recheck later with the same tools and method, you'll see exactly which item changed.
5. **When an account runs into trouble, check the exit and the account status separately.** Platforms may also look at your device, account profile, and activity history. If the platform notifies you, follow its process.

---

## About

This guide is written by the [GetIPProxy](https://getipproxy.com/) team. GetIPProxy offers dedicated static residential proxies you can renew long-term. When you shop, you can filter by [ping0 Risk Score](https://getipproxy.com/static-residential-proxies/clean-ips/) or [IPQualityScore Fraud Score](https://getipproxy.com/static-residential-proxies/clean-ips/ipqualityscore/).
