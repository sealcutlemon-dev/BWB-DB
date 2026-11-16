# Evil Web Bots DB (`evil-web-bots-db.txt`)

A curated, **frequently updated** threat-intelligence database containing IP addresses and proxies verified as malicious—specifically focusing on **bad web bots**, automated cloud scrapers, and reconnaissance probes.

## Overview
* **verified**, the data is collected from live intrusion detection logs and manually verified against residential ISPs, university networks, and legitimate search crawlers to keep false positives near zero.
* **focus?** Cloud compute scrapers (AWS, Tencent Cloud, DigitalOcean, OVH, Hetzner, Scaleway), stripped User-Agent probes, and bad web bots in general.
* **format:** plain-text newline-delimited IP list (`evil-web-bots-db.txt`) with `#` comment headers for light-weight implementations into firewalls, reverse proxies, and custom security scripts.

## quick usage example

### curl
```bash
curl -sL -o evil-web-bots-db.txt https://github.com
```

### (`.htaccess`)
convert non-comment lines directly into `Require not ip` rules for instant blocking.
