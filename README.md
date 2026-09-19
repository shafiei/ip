# IP Toolkit

A lightweight, browser-based IP address lookup tool that combines the functionality of **my-ip** and **ip-whois** in a single page.

It detects your public IP address on load and lets you look up registration and network information for any IPv4 or IPv6 address — including the assigned organization, network range, and abuse contact when available.

> This project is the successor to [`my-ip`](https://github.com/shafiei/my-ip) and [`ip-whois`](https://github.com/shafiei/ip-whois).

## Features

- 🌐 Detect your public IPv4/IPv6 address automatically
- 🔎 Look up any IPv4 or IPv6 address
- 🏢 Show the registered organization / network owner
- 📡 Display network and registry information
- 🚨 Extract abuse contact details when available
- 🔗 Shareable deep links such as `?ip=8.8.8.8`
- 📋 Copy the current lookup URL with one click
- 🧾 Inspect raw API responses
- 📱 Responsive layout
- 🌙 Automatic dark mode via `prefers-color-scheme`
- ♿ Keyboard-friendly focus states, reduced-motion support, and ARIA live feedback
- 🧩 No framework, build process, backend, or package installation required

## How it works

The application runs entirely in the browser.

1. On page load, it requests the visitor's public IP and basic IP information from **ipwho.is**.
2. When an IP address is searched, the app queries **RDAP** to retrieve registry data.
3. RDAP bootstraps the request to the authoritative Regional Internet Registry (RIR), with an ARIN endpoint available as a fallback.
4. The response is parsed in the browser and presented as structured information instead of embedding a third-party WHOIS page.

No application server is required.

## APIs

| Purpose | Service | Endpoint | API key |
| --- | --- | --- | --- |
| Public IP + IP information | ipwho.is | `https://ipwho.is/` | No |
| Registry / registration data | RDAP | `https://rdap.org/ip/{ip}` | No |
| Registry fallback | ARIN RDAP | `https://rdap.arin.net/registry/ip/{ip}` | No |

> Both services impose rate limits on free/public usage. For higher-traffic deployments, consider adding a small proxy and caching RDAP responses.

## Privacy

This is a client-side application, but lookup requests are sent from the browser to the external APIs listed above. Do not treat the project as an offline or zero-third-party-data tool.

## Deep links

You can open a specific lookup directly by adding the IP address to the URL:

```text
https://your-domain.example/?ip=8.8.8.8
```

The **Copy link** action generates a URL in the same format so a lookup can be shared with someone else.

## Project structure

The project intentionally stays small:

```text
.
├── index.html
├── icon.png
└── README.md
```

There is no build step and no dependency installation. The main application is contained in `index.html`.

## Deploy with GitHub Pages

Because the application is static, it can be deployed directly from GitHub Pages.

1. Create or use a repository for this project.
2. Push `index.html` and the accompanying assets.
3. Open **Settings → Pages**.
4. Deploy from the `main` branch and the repository root.

## Why this repository exists

The original projects had separate responsibilities:

- [`my-ip`](https://github.com/shafiei/my-ip) focused on showing the visitor's own IP address.
- [`ip-whois`](https://github.com/shafiei/ip-whois) focused on IP WHOIS / registration lookups.

**IP Toolkit** combines those two workflows into one interface so a user does not need to switch between separate pages or projects.

### Changes from `my-ip`

- Replaced the original HTTP lookup flow with HTTPS-based `ipwho.is` requests.
- Reduced the page's external UI dependencies by moving the styling into the page.
- Added visible error and fallback states instead of relying only on console errors.
- Integrated registry lookup into the same page.

### Changes from `ip-whois`

- Replaced the APNIC `jwhois.pl` iframe approach with RDAP lookups.
- Uses RDAP JSON responses so registry data can be parsed and displayed as structured fields.
- Validates IPv4 and IPv6 input before sending a lookup request.
- Extracts abuse-contact information from RDAP entity data when available.

### Shared improvements

- One search field and one unified interface
- Deep-link support
- Copyable lookup URLs
- Responsive design
- Dark mode
- Accessibility-focused interaction details
- Raw API response inspection

## Roadmap

Possible future improvements:

- Reverse DNS lookup
- Domain WHOIS / RDAP lookup
- Reputation / blocklist checks
- Bulk IP lookup from logs or pasted text
- Better caching and an optional proxy for higher traffic

## Related repositories

- [`my-ip`](https://github.com/shafiei/my-ip) — original public-IP page
- [`ip-whois`](https://github.com/shafiei/ip-whois) — original IP WHOIS lookup page

Those repositories are kept as historical predecessors of this project. New development should happen here.

## License

See the repository's `LICENSE` file for licensing information.
