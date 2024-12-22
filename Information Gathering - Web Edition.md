
---

# Web Reconnaissance Cheat Sheet

Web reconnaissance is the initial step in a security assessment or penetration test. It involves gathering information about a target to identify vulnerabilities, security misconfigurations, and valuable assets.

## Goals of Web Reconnaissance

- **Identifying Assets**: Map domains, subdomains, and IP addresses.
- **Uncovering Hidden Information**: Discover directories, files, and entry points.
- **Analyzing the Attack Surface**: Assess open ports, services, and software vulnerabilities.
- **Gathering Intelligence**: Collect details about employees, emails, and technologies.

---

## Reconnaissance Types

|**Type**|**Description**|**Risk of Detection**|**Examples**|
|---|---|---|---|
|**Active Reconnaissance**|Direct interaction with the target (e.g., probes).|Higher|Port scanning, vulnerability scanning, network mapping|
|**Passive Reconnaissance**|No direct interaction, relies on public data.|Lower|Search engine queries, WHOIS lookups, DNS enumeration, web archive analysis|

---

## WHOIS

WHOIS retrieves domain and IP information, revealing details like ownership and contact information.

### Example Command:

```bash
whois example.com
```

---

## DNS

The **Domain Name System (DNS)** resolves domain names into IP addresses.

### Dig Commands:

```bash
# A record lookup
dig example.com A

# Zone transfer
dig @ns1.example.com example.com axfr
```

### DNS Record Types:

|**Record Type**|**Description**|
|---|---|
|**A**|Maps hostname to IPv4 address.|
|**AAAA**|Maps hostname to IPv6 address.|
|**CNAME**|Alias for another hostname.|
|**MX**|Mail server information.|
|**NS**|Authoritative name servers.|
|**TXT**|Arbitrary text information.|
|**SOA**|Administrative zone info.|

---

## Subdomain Enumeration

Subdomains can host hidden or unsecured services.

### Techniques:

|**Approach**|**Description**|**Examples**|
|---|---|---|
|**Active Enumeration**|Direct DNS interaction.|Brute-forcing, zone transfer|
|**Passive Enumeration**|Relies on public sources.|CT logs, search engines|

### Subdomain Brute-Forcing:

```bash
dnsenum example.com -f subdomains.txt
```

---

## Virtual Hosts

Virtual hosting enables multiple websites on one IP. Discover them with tools like **Gobuster**.

### Gobuster Example:

```bash
gobuster vhost -u http://192.0.2.1 -w hostnames.txt
```

---

## Certificate Transparency (CT) Logs

CT logs reveal SSL/TLS certificates, exposing subdomains.

### Fetch Subdomains with crt.sh:

```bash
curl -s "https://crt.sh/?q=%25.example.com&output=json" | jq -r '.[].name_value' | sed 's/\*\.//g' | sort -u
```

---

## Web Crawling

Web crawling maps a site’s structure and identifies sensitive areas (e.g., from `robots.txt`).

### Scrapy Example:

```python
import scrapy

class ExampleSpider(scrapy.Spider):
    name = "example"
    start_urls = ['http://example.com/']

    def parse(self, response):
        for link in response.css('a::attr(href)').getall():
            if any(link.endswith(ext) for ext in self.interesting_extensions):
                yield {"file": link}
            elif not link.startswith("#") and not link.startswith("mailto:"):
                yield response.follow(link, callback=self.parse)
``````

### Extract Links from Scrapy Output:

```bash
jq -r '.[] | select(.file != null) | .file' example_data.json | sort -u
``````

---

## Search Engine Discovery

Leverage search engines for **OSINT** with Google Dorks.

### Common Search Operators:

|**Operator**|**Description**|**Example**|
|---|---|---|
|**site:**|Restrict search to a site.|`site:example.com "admin"`|
|**inurl:**|Search term in URL.|`inurl:login`|
|**filetype:**|Limit to specific file types.|`filetype:pdf "confidential"`|
|**intitle:**|Term in page title.|`intitle:"index of"`|
|**cache:**|View cached page version.|`cache:example.com`|
|**"term"**|Search exact phrase.|`"internal error" site:example.com`|
|**OR**|Combine multiple terms.|`inurl:admin OR inurl:login`|
|**-**|Exclude terms.|`inurl:admin -wordpress`|

---

## Web Archives

### Features:

- **Historical Snapshots**: View past website versions.
- **Hidden Directories**: Find removed or hidden areas.
- **Content Changes**: Track changes in text, images, and links.

Use the [Wayback Machine](https://archive.org/web/) to explore archived versions of sites.

---