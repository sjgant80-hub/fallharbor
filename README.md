# FallHarbor

**Estate directory. Where sovereign AI-Native tools register and get discovered.**

FallHarbor is a package-registry-shaped directory for the AI-Native Solutions estate. The source of truth is a single JSON manifest checked into this repo. A browser UI reads that manifest and renders a searchable, filterable directory with fork lineage visualisation and peer-estate discovery.

- Live: https://sjgant80-hub.github.io/fallharbor/
- Manifest: [`manifest.json`](./manifest.json)
- Schema: [`schema.json`](./schema.json)

## What FallHarbor answers

- Which tools does this estate publish?
- Which forks from which? (lineage)
- What capabilities does each tool declare?
- Where is the source? Where does it run live?
- Who else is running a compatible sovereign estate? (peers)

## The manifest

Every estate publishes one `manifest.json` describing its operator, tools, and lineage. Full JSON Schema in [`schema.json`](./schema.json).

Minimum shape:

```json
{
  "$schema": "https://sjgant80-hub.github.io/fallharbor/schema.json",
  "version": "1.0",
  "operator": {
    "did": "did:key:z...",
    "name": "Your Estate Name",
    "hub": "yourdomain.com"
  },
  "lineage": {
    "root": "fallseed-doctrine",
    "generation": 2
  },
  "tools": [
    {
      "name": "YourTool",
      "slug": "yourtool",
      "category": "insight",
      "url": "https://you.github.io/yourtool/",
      "repo": "https://github.com/you/yourtool",
      "capabilities": ["reflection", "local-only"],
      "license": "MIT",
      "public": true,
      "shipped": "2026-07-06"
    }
  ],
  "provenance": {
    "issued": "2026-07-06T00:00:00Z",
    "issuer": "did:key:z...",
    "signature": null
  }
}
```

## Publishing your own estate

1. Fork this repo (or start fresh with the same layout).
2. Edit `manifest.json` with your operator DID, tools, and lineage. If your estate descends from another, set `lineage.root` to the ancestor and `generation` to your depth.
3. Optionally sign the manifest with [FallSignature](https://sjgant80-hub.github.io/fallsignature/). The signature slots into `provenance.signature`.
4. Publish via GitHub Pages. The `index.html` reads `./manifest.json` automatically.
5. Tell peer estates. Any FallHarbor deployment can add you to `peer_estates` and browse your directory inline.

## Fork lineage

The directory renders a lineage graph derived from every tool's `forks_from` field. Root tools (`forks_from: null`) sit at the top of their subtree. Downstream forks nest under their ancestor. The visualisation makes provenance debt visible: a tool with many downstream forks is load-bearing substrate for the estate.

## Peer estates

`peer_estates` is a list of other FallHarbor-compatible manifests. Each entry gives a DID, a manifest URL, and (optionally) a generation. The UI lists peers with links to their live directories. Empty on this deployment for now.

## License

MIT. The manifest format, schema, and UI are open. Fork them, publish your own, extend the format. The point is discoverability, not lock-in.
