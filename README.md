# Agency MCP Bridge — releases

Signed builds of the Agency MCP Bridge WordPress plugin. Build artifacts only; the
source lives in a private repository.

## What is here

- `manifest.json` — the current release: version, package URL, SHA-256, and a signature.
- Release assets — the plugin ZIP for each version, attached to its tag.

## Why this repository is public

WordPress sites download updates without credentials. A private repository would mean
putting a token on every client site, which is worse than publishing build artifacts.

Publishing them costs nothing in safety, because **the manifest is signed**. Every install
carries the public half of a key whose private half never leaves the release machine, and a
build that does not verify against it is not installed. Anyone can read this code; nobody
can substitute it.

## Verifying a release by hand

```bash
curl -sO https://raw.githubusercontent.com/barbatjuan/agency-mcp-bridge-releases/main/manifest.json
jq -r .sha256 manifest.json
curl -sL "$(jq -r .package manifest.json)" | sha256sum
```

Those two hashes must match. If they do not, do not install it, and treat this host as
compromised until proven otherwise.

## Reporting something

Found a problem in the plugin? Open an issue here. Do not post anything from a live site:
URLs, credentials, or customer data.
