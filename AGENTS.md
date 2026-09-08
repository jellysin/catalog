# Repository instructions

Read CONTRIBUTING.md before changing plugin repository publication or branch behavior.

- This repository publishes the shared Jellyfin plugin manifest.
- `manifest.json` is always an array in Jellyfin's plugin repository format; initially it is empty.
- Keep the public plugin repository URL stable and preserve every published version.
- Review GUID, source repository and signer workflow together when changing `plugins.json`.
- Only verified, immutable public releases may add entries. Never weaken provenance validation.
- Pin shared Actions to full reviewed SHAs; update through Renovate PRs.
- Use only this repository's GITHUB_TOKEN. No cross-repository write token or release App.
- Plugin repository PRs change only the manifest; bot CI is explicitly dispatched.
- Manifest and stable release-helper Action updates may squash auto-merge only after required checks; never bypass bot workflow approval or branch protection.
- Default permissions are read-only; writes have explicit job scope and timeouts.
- Conventional Commit PR titles, squash merges, required CI with strict: false.
- Release automation collects version/changelog PRs only; tags and GitHub releases require a separate explicit maintainer action.
- Record failed or unavailable checks; never describe intended GitHub settings as verified.
