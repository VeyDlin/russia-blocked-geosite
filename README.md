# russia-blocked-geosite

Automated build of **GeoSite** files containing domains blocked by Roskomnadzor, for traffic routers and Proxy/VPN applications (v2ray, xray, sing-box, mihomo, and others).

The build runs automatically **every 6 hours**, so the links in the [Download](#download) section always point to the latest version.

## Table of contents

- [Data sources](#data-sources)
- [File formats](#file-formats)
  - [Domains are not enough for Telegram](#domains-are-not-enough-for-telegram)
- [Available categories](#available-categories)
- [Download](#download)
  - [GeoSite `.dat` — v2ray / xray / mihomo](#geosite-dat--v2ray--xray--mihomo)
  - [sing-box `.srs`](#sing-box-srs)
  - [Plain-text domain lists](#plain-text-domain-lists)
- [Related projects](#related-projects)
- [Acknowledgements](#acknowledgements)


## Data sources

**Roskomnadzor block lists:**

| Source | Description |
| --- | --- |
| [antifilter.download](https://antifilter.download/) | Full list of blocked domains |
| [community.antifilter.download](https://community.antifilter.download/) | Community-maintained list |
| [re:filter](https://github.com/1andrevich/Re-filter-lists) | Filtered list of blocked domains |

**Additional lists:**

| Source | Description |
| --- | --- |
| [@v2fly/domain-list-community](https://github.com/v2fly/domain-list-community/tree/master/data) | Large set of domains grouped by service, company, and category |
| [AdGuard DNS Filter](https://github.com/AdguardTeam/AdguardSDNSFilter) | Advertising domains |
| [Peter Lowe's list](https://pgl.yoyo.org/adservers/serverlist.php) | Advertising domains |
| [WindowsSpyBlocker](https://github.com/crazy-max/WindowsSpyBlocker) | Windows domains (telemetry, updates, and more) |

**IP ranges:**

| Source | Description |
| --- | --- |
| [core.telegram.org/resources/cidr.txt](https://core.telegram.org/resources/cidr.txt) | Telegram IP ranges, published by Telegram itself |
| [RIPEstat](https://stat.ripe.net/) | Prefixes announced by Telegram's own networks — AS62041, AS62014, AS59930, AS44907, AS211157 |

Domains from [@runetfreedom/russia-domains-list](https://github.com/runetfreedom/russia-domains-list) are also included in the build.
**If you want to suggest new domains or categories, do it there.**


## File formats

The same set of categories is published in three formats — pick the one that fits your client:

| Format | File | Used by |
| --- | --- | --- |
| **GeoSite** | `geosite.dat` | v2ray, xray, mihomo (clash.meta), and compatible clients. Contains **all** categories in a single file, referenced by name — `geosite:ru-blocked` |
| **sing-box rule-set** | `geosite-*.srs` | sing-box. Each category is a separate binary `.srs` file |
| **Plain-text list** | `*.txt` | Raw domain list, one per line. For manual use and other tools |

A trimmed **"Russia only"** variant is also published (`geosite-ru-only.dat` and the `sing-box-ru-only/` directory) — it contains only the blocked-domain list, without foreign categories.

### Domains are not enough for Telegram

Domain rules only match traffic that resolves a name first. The Telegram client, once connected, talks to its MTProto datacenters by IP, so a domain-only rule-set silently misses most of the session. The build therefore also publishes IP rules:

| File | Contents |
| --- | --- |
| `geoip-telegram.srs` | Telegram IP ranges only |
| `telegram-full.srs` | Telegram domains **and** IP ranges in one rule-set |
| `ru-blocked-full.srs` | `ru-blocked` domains **and** Telegram IP ranges |
| `ru-blocked-all-full.srs` | `ru-blocked-all` domains **and** Telegram IP ranges |

> IP ranges exist in the sing-box files only. The v2ray `geosite.dat` format stores domains and nothing else, so `geosite.dat` cannot carry them — for v2ray / xray / mihomo, pair a category with a separate geoip source.


## Available categories

`geosite.dat` contains **all** categories from [@v2fly/domain-list-community](https://github.com/v2fly/domain-list-community/tree/master/data) (`google`, `discord`, `youtube`, `twitter`, `meta`, `openai`, and hundreds more), plus the additional categories of this project:

| Category | Description |
| --- | --- |
| `geosite:ru-blocked` | Domains blocked in Russia (`antifilter-download-community` + `re:filter` + `telegram`) |
| `geosite:ru-blocked-all` | **All known** blocked domains (`antifilter-download` + `antifilter-download-community` + `re:filter` + `telegram`). Around 1.5M domains — **use with caution** |
| `geosite:ru-available-only-inside` | Domains available only from inside Russia |
| `geosite:antifilter-download` | All domains from `antifilter.download` (around 1.5M — **use with caution**) |
| `geosite:antifilter-download-community` | All domains from `community.antifilter.download` |
| `geosite:refilter` | All domains from `re:filter` |
| `geosite:category-ads-all` | All advertising domains |
| `geosite:win-spy` | Windows telemetry and tracking domains |
| `geosite:win-update` | Windows update domains |
| `geosite:win-extra` | Other Windows domains |


## Download

All links below always point to the latest version. Three mirrors are available: **GitHub** (`raw.githubusercontent.com`), **jsDelivr**, and **Fastly + jsDelivr**.

### GeoSite `.dat` — v2ray / xray / mihomo

| File | GitHub | jsDelivr | Fastly |
| --- | --- | --- | --- |
| `geosite.dat` | [download](https://raw.githubusercontent.com/VeyDlin/russia-blocked-geosite/release/geosite.dat) | [download](https://cdn.jsdelivr.net/gh/VeyDlin/russia-blocked-geosite@release/geosite.dat) | [download](https://fastly.jsdelivr.net/gh/VeyDlin/russia-blocked-geosite@release/geosite.dat) |
| `geosite.dat.sha256sum` | [download](https://raw.githubusercontent.com/VeyDlin/russia-blocked-geosite/release/geosite.dat.sha256sum) | [download](https://cdn.jsdelivr.net/gh/VeyDlin/russia-blocked-geosite@release/geosite.dat.sha256sum) | [download](https://fastly.jsdelivr.net/gh/VeyDlin/russia-blocked-geosite@release/geosite.dat.sha256sum) |
| `geosite-ru-only.dat` | [download](https://raw.githubusercontent.com/VeyDlin/russia-blocked-geosite/release/geosite-ru-only.dat) | [download](https://cdn.jsdelivr.net/gh/VeyDlin/russia-blocked-geosite@release/geosite-ru-only.dat) | [download](https://fastly.jsdelivr.net/gh/VeyDlin/russia-blocked-geosite@release/geosite-ru-only.dat) |

### sing-box `.srs`

Each category is published as a separate `.srs` rule-set file. Names match the categories with a `geosite-` prefix — for example, `geosite-ru-blocked.srs`, `geosite-google.srs`.

**A `remote` rule-set subscribes to the URL of a single `.srs` file** (using `ru-blocked-all` as an example):

- GitHub: `https://raw.githubusercontent.com/VeyDlin/russia-blocked-geosite/release/sing-box/geosite-ru-blocked-all.srs`
- jsDelivr: `https://cdn.jsdelivr.net/gh/VeyDlin/russia-blocked-geosite@release/sing-box/geosite-ru-blocked-all.srs`

```json
{
  "route": {
    "rule_set": [
      {
        "type": "remote",
        "tag": "ru-blocked-all",
        "format": "binary",
        "url": "https://cdn.jsdelivr.net/gh/VeyDlin/russia-blocked-geosite@release/sing-box/geosite-ru-blocked-all.srs",
        "download_detour": "proxy"
      }
    ]
  }
}
```

> To use another rule, replace `geosite-ru-blocked-all.srs` with the name of the category you need (see [Available categories](#available-categories)).

#### Rule-sets that include Telegram IP ranges

Four more files live in the same directory and are referenced exactly the same way — only the file name changes: `geoip-telegram.srs`, `telegram-full.srs`, `ru-blocked-full.srs`, `ru-blocked-all-full.srs` (see [Domains are not enough for Telegram](#domains-are-not-enough-for-telegram)).

To route Telegram fully, either take the combined file on its own:

```json
{
  "type": "remote",
  "tag": "telegram-full",
  "format": "binary",
  "url": "https://cdn.jsdelivr.net/gh/VeyDlin/russia-blocked-geosite@release/sing-box/telegram-full.srs",
  "download_detour": "proxy"
}
```

…or keep domains and addresses apart and list both `geosite-telegram.srs` and `geoip-telegram.srs` in the same routing rule.

For local (offline) use, all rules are also packaged as an archive — download and reference each file as a `local` rule-set: [sing-box.zip](https://raw.githubusercontent.com/VeyDlin/russia-blocked-geosite/release/sing-box.zip) · ["Russia only"](https://raw.githubusercontent.com/VeyDlin/russia-blocked-geosite/release/sing-box-ru-only.zip)

### Plain-text domain lists

The [`release`](https://github.com/VeyDlin/russia-blocked-geosite/tree/release) branch holds raw domain lists (`.txt`, one domain per line):

The same curated set is available both as sing-box `.srs` rule-sets and as plain `.txt` lists:

- **Blocked / RU:** `ru-blocked` · `ru-blocked-all` · `ru-available-only-inside` · `antifilter-download` · `antifilter-download-community` · `refilter`
- **Ads & Windows:** `category-ads-all` · `win-spy` · `win-update` · `win-extra`
- **Popular services:** `google` · `youtube` · `discord` · `twitter` · `meta` · `openai` · `telegram` · `twitch` · `github` · `cloudflare` · `netflix` · `spotify` · `tiktok` · `reddit` · `signal` · `steam` · `apple` · `microsoft` · `amazon`

Example: `https://raw.githubusercontent.com/VeyDlin/russia-blocked-geosite/release/ru-blocked.txt`

Telegram's IP ranges ship as a text file too — `geoip-telegram.txt`, one CIDR prefix per line.

> Need a category that isn't in this set? It's still inside `geosite.dat` — all ~1800 v2fly categories ship there.


## Related projects

- [@runetfreedom/russia-v2ray-rules-dat](https://github.com/runetfreedom/russia-v2ray-rules-dat) — unified source of geo files for v2ray / xray / sing-box
- [@runetfreedom/russia-blocked-geoip](https://github.com/runetfreedom/russia-blocked-geoip) — geoip file generation
- [@runetfreedom/russia-v2ray-custom-routing-list](https://github.com/runetfreedom/russia-v2ray-custom-routing-list) — routing rules for various clients
- [@runetfreedom/geodat2srs](https://github.com/runetfreedom/geodat2srs) — geoip / geosite.dat to sing-box `.srs` converter


## Acknowledgements

- [@runetfreedom/russia-blocked-geosite](https://github.com/runetfreedom/russia-blocked-geosite) — the original project this repository is based on
- [@runetfreedom](https://github.com/runetfreedom) — for the build tooling and domain lists
- [antifilter.download](https://antifilter.download/) — for blocked-domain data and a community to keep it updated
- [re:filter](https://github.com/1andrevich/Re-filter-lists) — for filtered blocked-domain data
- [@Loyalsoldier/v2ray-rules-dat](https://github.com/Loyalsoldier/v2ray-rules-dat) — for the original idea behind the upstream project
