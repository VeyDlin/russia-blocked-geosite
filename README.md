# russia-blocked-geosite

Automated build of **GeoSite** files containing domains blocked by Roskomnadzor, for traffic routers and Proxy/VPN applications (v2ray, xray, sing-box, mihomo, and others).

The build runs automatically **every 6 hours**, so the links in the [Download](#download) section always point to the latest version.

## Table of contents

- [Data sources](#data-sources)
- [File formats](#file-formats)
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


## Available categories

`geosite.dat` contains **all** categories from [@v2fly/domain-list-community](https://github.com/v2fly/domain-list-community/tree/master/data) (`google`, `discord`, `youtube`, `twitter`, `meta`, `openai`, and hundreds more), plus the additional categories of this project:

| Category | Description |
| --- | --- |
| `geosite:ru-blocked` | Domains blocked in Russia (`antifilter-download-community` + `re:filter`) |
| `geosite:ru-blocked-all` | **All known** blocked domains (`antifilter-download` + `antifilter-download-community` + `re:filter`). At least 700k domains — **use with caution** |
| `geosite:ru-available-only-inside` | Domains available only from inside Russia |
| `geosite:antifilter-download` | All domains from `antifilter.download` (nearly 700k — **use with caution**) |
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

**A `remote` rule-set subscribes to the URL of a single `.srs` file** (using `ru-blocked` as an example):

- GitHub: `https://raw.githubusercontent.com/VeyDlin/russia-blocked-geosite/release/sing-box/geosite-ru-blocked.srs`
- jsDelivr: `https://cdn.jsdelivr.net/gh/VeyDlin/russia-blocked-geosite@release/sing-box/geosite-ru-blocked.srs`

```json
{
  "route": {
    "rule_set": [
      {
        "type": "remote",
        "tag": "ru-blocked",
        "format": "binary",
        "url": "https://cdn.jsdelivr.net/gh/VeyDlin/russia-blocked-geosite@release/sing-box/geosite-ru-blocked.srs",
        "download_detour": "proxy"
      }
    ]
  }
}
```

> To use another rule, replace `geosite-ru-blocked.srs` with the name of the category you need (see [Available categories](#available-categories)).

For local (offline) use, all rules are also packaged as an archive — download and reference each file as a `local` rule-set: [sing-box.zip](https://raw.githubusercontent.com/VeyDlin/russia-blocked-geosite/release/sing-box.zip) · ["Russia only"](https://raw.githubusercontent.com/VeyDlin/russia-blocked-geosite/release/sing-box-ru-only.zip)

### Plain-text domain lists

The [`release`](https://github.com/VeyDlin/russia-blocked-geosite/tree/release) branch holds raw domain lists (`.txt`, one domain per line):

The same curated set is available both as sing-box `.srs` rule-sets and as plain `.txt` lists:

- **Blocked / RU:** `ru-blocked` · `ru-blocked-all` · `ru-available-only-inside` · `antifilter-download` · `antifilter-download-community` · `refilter`
- **Ads & Windows:** `category-ads-all` · `win-spy` · `win-update` · `win-extra`
- **Popular services:** `google` · `youtube` · `discord` · `twitter` · `meta` · `openai` · `telegram` · `twitch` · `github` · `cloudflare` · `netflix` · `spotify` · `tiktok` · `reddit` · `signal` · `steam` · `apple` · `microsoft` · `amazon`

Example: `https://raw.githubusercontent.com/VeyDlin/russia-blocked-geosite/release/ru-blocked.txt`

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
