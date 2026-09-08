# JellySin plugin catalog

One catalog for JellySin's independent Jellyfin 12 plugins. Add this repository URL
in Jellyfin's plugin repository settings:

```text
https://raw.githubusercontent.com/jellysin/catalog/main/manifest.json
```

The catalog includes [JellySin Last.fm 1.0.0](https://github.com/jellysin/jellyfin-plugin-lastfm/releases/tag/v1.0.0),
verified through a fresh Jellyfin 12 installation and restart checks. New versions
appear after their immutable release is verified and the resulting catalog pull
request is merged.

## Publication

An allowlist binds each plugin GUID to one public source repository and the
approved `.github/workflows/release.yml`. The updater runs at minutes 17 and 47
each hour and can also be dispatched manually. GitHub scheduled runs can be delayed;
this is a polling interval, not a publication latency guarantee.

Pinned shared tooling verifies the actual GitHub-signed provenance of all four
release artifacts against the repository, workflow, commit and tag. Releases must
be immutable. The ZIP's SHA-256, Jellyfin MD5, size, member paths, permissions,
file allowlist and CRC are checked before any catalog file changes.

The updater opens a PR using only this repository's GITHUB_TOKEN and explicitly
dispatches CI on its branch. Required checks and normal PR review/merge behavior
apply. No plugin repository gets write access to this catalog, and no release App
or personal access token is needed.

## Adding a plugin

Submit a PR adding a unique GUID, repository, and approved workflow to `plugins.json`.
Review the source repository and publication workflow before adding that trust.
The source must use the release metadata contract in
[plugin-tooling](https://github.com/jellysin/plugin-tooling). The Last.fm descriptor
is the first allowlisted plugin; no Last.fm-specific behavior exists in the updater.

Existing versions are immutable catalog history. Do not replace checksums, edit
download URLs, or remove old compatible versions to repair an upload. Publish a
new version instead. A failed verification leaves the entire catalog unchanged.

EUPL-1.2 covers this repository's source and documentation. See CONTRIBUTING.md.
