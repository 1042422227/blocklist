# Repository instructions

## Purpose and layout

This repository is the canonical source for URLs that Phantom flags as malicious. `blocklist.yaml` contains blocked Solana sites, `eth-blocklist.yaml` contains Ethereum entries, `nft-blocklist.yaml` contains blocked NFT mints, and `whitelist.yaml` contains explicit exceptions. `build.js` generates the published JSON artifacts; `ci.js` validates required fields and keeps the disabled fuzzy list empty.

## Development commands

CI uses Node 16 and Yarn v1.

- `yarn install --frozen-lockfile` installs the committed dependencies.
- `node ./ci.js` validates the YAML lists.
- `yarn build` generates the blocklist JSON and content hashes.

## Contribution constraints

- Append new blocked URLs to the bottom of `blocklist.yaml` in the existing format.
- Store hostnames without protocol prefixes such as `https://`.
- Explain why a site should be blocked in the commit or pull request description; optional entry metadata may record the reason or requester.
- For a malicious subdomain of a legitimate base domain, add the quoted wildcard base domain to `whitelist.yaml` and the full malicious subdomain to `blocklist.yaml` as documented in `README.md`.
- Treat `blocklist.yaml` as production data: merges to `master` deploy it automatically.