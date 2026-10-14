# Orova SEO Check for Claude Code

Ask your coding agent to "check SEO of example.com" and get a scored technical SEO report, backlinks and a shareable link, with no API key and no signup.

## What you get

- **90+ checks in 12 groups**: access and HTTP, security headers, head and meta, content, images, social sharing, structured data, international, crawlability, sample pages, speed, links.
- **PageSpeed** results for mobile and desktop, including Core Web Vitals (LCP, CLS, TBT).
- **Backlinks** from a 133M-domain Common Crawl graph: referring domains, domain rank, top linking domains.
- **A shareable report link** on orova.vn for every scan, e.g. `https://orova.vn/en/seo-check?id=<id>`.

## Install

**Claude Code plugin**

```
/plugin marketplace add orova-vn/orova-seo-check
/plugin install orova-seo-check@orova
```

**skills CLI** (Claude Code, Codex and other agents)

```bash
npx skills add orova-vn/orova-seo-check
```

**Manual**

```bash
git clone https://github.com/orova-vn/orova-seo-check.git
cp -r orova-seo-check/skills/orova-seo-check ~/.claude/skills/
```

Requirements: Python 3.9+ (standard library only).

## Usage

In Claude Code (or any agent with the skill installed):

```
check SEO of example.com
who links to example.com? show the top referring domains
```

From the command line:

```bash
python3 skills/orova-seo-check/scripts/orova_seo.py check https://example.com
python3 skills/orova-seo-check/scripts/orova_seo.py backlinks example.com --limit 20
```

Add `--json` for raw JSON, `--locale vi` for a Vietnamese report link, `--timeout` to wait longer.

## Example output

```markdown
# SEO Check — example.com

Score: 91/100
Scanned: 2026-10-14T19:20:48+00:00 · 41152 ms

| Group | Score | Max |
|---|---:|---:|
| Access & HTTP | 13.4 | 14 |
| Security headers | 3.5 | 6 |
| ... | | |

## Failed checks

- Links & authority: Site has referring domains (`referring_domains`) — count=0

## Warnings

- Security headers: Strict-Transport-Security header is set (`hsts`)
- Speed: Largest Contentful Paint is within target (`lcp_ok`) — value=5.5 s

## Passed

73 checks passed.

Full report: https://orova.vn/en/seo-check?id=<id>
```

More real reports are in [examples/](examples/).

## Limits

- 5 scans per hour per IP. Re-checking a domain scanned in the last 24 hours returns the cached result and does not count.
- 30 backlinks lookups per hour per IP.
- A scan takes 30 to 90 seconds and covers the homepage plus a few sample pages, not a full crawl.
- Backlinks are domain-level data from Common Crawl and may miss small or new sites (they can show 0).

## How it works

The script calls the public Orova SEO Check API (`https://orova.vn/u/seo-check/...`): it submits the URL,
polls for the result every 3 seconds and renders Markdown. No crawler runs on your machine and nothing is sent
except the URL or domain you ask about. Set `OROVA_BASE_URL` or `--base-url` to point at another host.

Check codes and their meanings: [skills/orova-seo-check/references/checks.md](skills/orova-seo-check/references/checks.md).

## Built by Orova

[Orova](https://orova.vn) builds AI tools for marketing, sales and SEO teams.
[Orova SEO](https://orova.vn/en/seo) adds daily monitoring, Search Console insights and AI content tools on top of this check.
Documentation for all Orova modules is at [orova.vn/en/docs](https://orova.vn/en/docs).

## License

MIT. See [LICENSE](LICENSE).
