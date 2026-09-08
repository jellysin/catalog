# Repository instructions

Read CONTRIBUTING.md before changing catalog publication or branch behavior.

- This repository is a catalog, not a plugin runtime or build-script copy.
- `manifest.json` is always a Jellyfin catalog array; initially it is empty.
- Keep the public catalog URL stable and preserve every published version.
- Review GUID, source repository and signer workflow together when changing `plugins.json`.
- Only verified, immutable public releases may add entries. Never weaken provenance validation.
- Pin shared Actions to full reviewed SHAs; update through Renovate PRs.
- Use only this repository's GITHUB_TOKEN. No cross-repository write token or release App.
- Catalog PRs change only the manifest; bot CI is explicitly dispatched.
- Default permissions are read-only; writes have explicit job scope and timeouts.
- Conventional Commit PR titles, squash merges, required CI with strict: false.
- Record failed or unavailable checks; never describe intended GitHub settings as verified.
