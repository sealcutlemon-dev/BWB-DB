# Evil Web Bots DB (`evil-web-bots-db.txt`)

A curated, **frequently updated** threat-intelligence database containing IP addresses and proxies verified as malicious. specifically focusing on **bad web bots**, automated cloud scrapers, and reconnaissance probes.

## Overview
* **verified**, the data is collected from live intrusion detection logs and manually verified against residential ISPs, university networks, and legitimate search crawlers to keep false positives near zero.
* **focus?** Cloud compute scrapers (AWS, Tencent Cloud, DigitalOcean, OVH, Hetzner, Scaleway), stripped User-Agent probes, and bad web bots in general.
* **format:** plain-text newline-delimited IP list (`evil-web-bots-db.txt`) with `#` comment headers for light-weight implementations into firewalls, reverse proxies, and custom security scripts.

## quick usage example

### curl

# bash with linux utilities
```bash-linux
curl -s https://raw.githubusercontent.com/sealcutlemon-dev/BWB-DB/refs/heads/main/evil-web-bots-db.txt | grep -v '^#'
```


# standard curl, no linux utilities.
```bash
curl -s https://raw.githubusercontent.com/sealcutlemon-dev/BWB-DB/refs/heads/main/evil-web-bots-db.txt | findstr /V /B "#"
```


# powershell

```powershell
((iwr -Uri "https://raw.githubusercontent.com/sealcutlemon-dev/BWB-DB/refs/heads/main/evil-web-bots-db.txt" -UseBasicParsing).Content -split "`r?`n") | Where-Object { $_ -and $_ -notmatch '^#' }
```

### (`.htaccess`)
convert non-comment lines directly into `Require not ip` rules for instant blocking.

# turning it into `Require not ip` via bash and powershell

# bash

```bash
curl -sL https://github.com | sed -e '/^#/d' -e '/^$/d' -e 's/^/Require not ip /'
```

# powershell

```powershell
(Invoke-RestMethod https://raw.githubusercontent.com/sealcutlemon-dev/BWB-DB/refs/heads/main/evil-web-bots-db.txt) -split "`n" | Where-Object { $_ -and $_ -notmatch '^#' } | ForEach-Object { "Require not ip $_" }
```
