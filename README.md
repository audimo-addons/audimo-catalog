# audimo-catalog

The default catalog of community Audimo addons.

Audimo treats catalogs like Cydia/Sileo repos: the user adds catalog
sources by URL, and Audimo merges addons across every configured
source. There's no built-in "official" list — fresh installs ship
empty. This repo is **one** option a user might add.

## Use it

In Audimo: **Addons → Catalog Sources → Add Source**

Paste:

    https://raw.githubusercontent.com/audimo-addons/audimo-catalog/main/catalog.json

The Catalog section below will populate with the addons listed in
[`catalog.json`](./catalog.json), and you can install / uninstall
each with one click.

Adding a source means trusting whoever publishes it. Audimo SHA256-
verifies addon binaries against per-addon manifests, but the catalog
file itself is whatever this repo serves.

## Make your own

Fork this repo (or write a new file from scratch) and publish your
own `catalog.json` somewhere fetchable. Then anyone can add your URL
the same way.

The schema (`schema_version: 1`):

```json
{
  "schema_version": 1,
  "name": "your repo name",
  "description": "what's in this catalog",
  "homepage": "https://...",
  "updated_at": "2026-05-05T00:00:00Z",
  "addons": [
    {
      "id": "your-addon-id",
      "name": "Display Name",
      "description": "What it does",
      "author": "you",
      "homepage": "https://github.com/you/your-addon",
      "icon_url": "",
      "manifest_url": "https://github.com/you/your-addon/releases/latest/download/manifest.json"
    }
  ]
}
```

`manifest_url` is the per-release manifest published by your addon's
build pipeline (see `audimo-streamers` for an example shape — it
lists `binaries[<platform>]` entries with URL + SHA256).

## Adding an addon to this catalog

Open a PR against [`catalog.json`](./catalog.json) with your addon's
entry. The audimo-addons project reviews for safety and obvious quality
problems, but isn't a gatekeeper for taste — community addons live
or die on their own.

If you'd rather not depend on audimo-addons's review cadence, publish your
own catalog and have users add it directly.
