# About this fork

A personal fork of [kalkih/mini-media-player](https://github.com/kalkih/mini-media-player), installed through Home
Assistant's Marketplace on one instance. Upstream has no `hacs.json`, and the Marketplace refuses every version without
one ("missing the hacs.json file required for installation"). This fork adds it and re-releases upstream's own builds.
Its `main` is upstream's newest release tag plus the changes listed below. Upstream's README still applies.

## Rules for changes

- **Nothing is sent upstream.** Changes stay upstream-shaped, one per commit.
- **Upstream's code is what runs.** A release attaches the `mini-media-player-bundle.js` upstream built for the release
  tag `main` is on; the fork builds nothing.
- **Work happens on `fork/*` branches**, merged into `main` by pull request in this repository.

## Upstream, releases and the Marketplace

- **Upstream sync:** `.github/workflows/fork-sync.yml` runs daily at 10:17 UTC. When upstream publishes a release `main`
  doesn't have, it merges that release's tag into `main`, pushes and releases. A merge that conflicts or changes workflow
  files (which the workflow's token may not push) opens or updates one issue labelled `upstream-sync`; nothing is pushed.
- **Release:** `.github/workflows/fork-release.yml`, run by the sync or by hand. It tags `main`
  `oliviacpu-YYYY.MM.DD[.N]` and creates a GitHub Release titled `<upstream tag>-oliviacpu.<YYYYMMDD>[.N]` with
  upstream's bundle for that tag attached.
- **Install:** Marketplace → custom repository `oliviacpu/mini-media-player` (Dashboard). It installs to
  `www/community/mini-media-player` and adds the dashboard resource. Updates are by hand in the Marketplace.

## Changes in this fork

Newest first.

### `hacs.json` (2026-11-21)

- **What it adds:** `hacs.json` naming the card and its file, `mini-media-player-bundle.js`.
- **Cause:** the Marketplace requires `hacs.json` at every version it installs, and upstream never had one, so after
  the card was uninstalled it could not be installed again.
