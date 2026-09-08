# Contributing

Create a feature branch from main and open a PR with a Conventional Commit title.
Squash merges are used. Required checks use `strict: false`, so branches need not
be rebased solely to satisfy a branch-up-to-date gate.

CI uses SHA-pinned shared tooling to validate plugin repository structure, plugin identities,
repository allowlisting, pinned Actions and policy documents. It also runs
actionlint. Locally, use a checkout of the exact tooling commit pinned in CI:

```sh
python ../release-helper/tools.py validate-catalog
python ../release-helper/tools.py check-policy
actionlint
```

Run these commands in `repo`. Local manifest updates also require GitHub CLI
for signature verification and a GITHUB_TOKEN/GH_TOKEN for
rate-limited API reads. It downloads data but never runs code from plugin archives.

The updater opens `automation/repository` as a PR, then explicitly dispatches CI.
It verifies the PR's repository, base, branch and generated head SHA before
requesting squash auto-merge for that exact commit. Required checks and review
rules still apply; the updater never uses a bypass or administrator merge.
GitHub may also place the PR-triggered run behind its bot-workflow approval gate.
A maintainer reviews and approves that run; a dispatched run alone may not clear
the required PR check. No extra App/PAT or synthetic check is used to evade it.
Do not write directly to main or bypass required checks. A failed update keeps
the previous manifest intact. Resolve the release or allowlist problem and retry
the updater; never replace an already published release asset.

Renovate handles helper Action pins separately. Only `github-actions` updates
for stable `jellysin/release-helper` tags enable squash auto-merge; they retain
full commit pins, the three-day minimum release age and required CI. They are
kept separate from unrelated Action updates. Renovate waits for its checks and
release-age requirement before merging instead of immediately enabling GitHub's
platform auto-merge. Helper commits without a stable
tag do not trigger these dependency updates, and other dependencies keep their
existing review behavior.

Source releases must have immutable releases enabled before publication. The
plugin repository trusts the approved release workflow, not arbitrary self-declared JSON.
Workflow and allowlist changes require careful review of the trust boundary.

Release-please collects merged changes into version and changelog PRs. Ordinary
main merges and release PR merges do not create tags or GitHub releases. Selecting
a version for tagging and publication requires a separate, explicit maintainer
action. This manifest repository has no GitHub release publication workflow.
Each plugin owns its own version and release process; accepting an approved plugin
release into `manifest.json` does not publish a release of this repository.
