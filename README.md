# PlayGTA5 browser project

Personal project for a browser-hosted version of the existing PlayGTA5 port.

## Required deployment target

The finished version must run independently of the owner's Mac:

- no local server, computer, files, or browser profile may be needed after deployment;
- game delivery, web frontend, and cross-device save service must be GitHub-hosted;
- each player's saves must be private and isolated, with safe synchronization across devices;
- never expose the owner's current save in the public repository.

**This target is not implemented yet.** There is no playable GitHub Pages site or cloud save service in this repository.

## Current technical limits

The local game snapshot is about 20 GiB across 12,482 files. GitHub Pages has a 1 GiB published-site limit, so the full snapshot cannot be published as a Pages site. Pages is static hosting and cannot itself accept authenticated Story Mode save writes. GitHub Codespaces is a development environment, not an always-on game host.

The previous Vercel deployment was disabled with HTTP 402 after the approximately 21 GiB deployment exceeded that account's 10 GiB Hobby deployment-storage allowance. Cloudflare was not signed in during the latest deployment check. No other asset host or persistent save backend is configured.

A GitHub-only design still needs a viable GitHub asset-delivery path for the game data and a secure, user-scoped save-write architecture. A static Pages frontend alone cannot provide both. Until these are implemented and tested, this repository does not provide a working game link.

References: [GitHub Pages limits](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits) · [GitHub included usage by plan](https://docs.github.com/en/billing/reference/product-usage-included).

## Local installation and saves

The existing local Mac install is separate from this repository. Its launcher and Mac-local save mirror are useful for local play, but the finished public deployment must not depend on them. The local Brave IndexedDB persistence request was denied, so browser storage alone is best-effort.

No game binaries, native save files, browser data, or private save hashes are stored in this repository. See [DEPLOYMENT-STATUS.md](DEPLOYMENT-STATUS.md) for the latest verified status.
