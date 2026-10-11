# PlayGTA5 browser experiment

This is the personal repository created for a future browser-hosted version of the local PlayGTA5 port.

## Current status

**Not playable from GitHub Pages yet.** This repository contains no game snapshot, no deployed site, and no cloud save backend. It does not include private save files.

The existing local install is about 20 GiB across 12,482 files. GitHub Pages has a 1 GiB published-site limit and a soft 100 GiB/month bandwidth limit. Its static hosting cannot persist a player's Story Mode writes to the server. GitHub Codespaces is a development environment with monthly included quotas (Free personal accounts: 120 core-hours and 15 GB-month storage); it is not a persistent game-hosting service.

References: [GitHub Pages limits](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits) · [included usage by plan](https://docs.github.com/en/billing/reference/product-usage-included).

## Save status

The local game now mirrors native save files to the Mac at `~/Games/PlayGTA5/saves` and to IndexedDB. On the tested Brave origin, `navigator.storage.persist()` was denied, so IndexedDB alone is best-effort. The Mac-local API is not reachable from another computer.

A true cross-device save needs a separate authenticated cloud backend. A public shared save would let visitors overwrite or inspect one another's progress, so this project will require user-scoped sync before any public game launch.

## Assets

Game binaries and user save data are intentionally not included in this repository. The game snapshot stays in the existing local installation.
