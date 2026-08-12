# tank3-releases

Sparkle update hosting for [Tank](https://github.com/tankernauts/tank3) (the
tank3 Mac app). This repo is not source code -- it exists only so the
in-app updater has stable, unauthenticated URLs to check.

`tank3` itself is a private repo, and Sparkle's in-app updater has no way
to authenticate, so update hosting has to live somewhere public. This repo
is that somewhere:

- **`appcast.xml`** (repo root, served via [GitHub
  Pages](https://tankernauts.github.io/tank3-releases/appcast.xml)) is the
  signed Sparkle feed every built Tank.app checks (`SUFeedURL`). It's
  regenerated and pushed here by `tank3`'s `release.yml` workflow on every
  release run -- never edited by hand.
- **[Releases](https://github.com/tankernauts/tank3-releases/releases)**
  hosts each release's signed, notarized, stapled `Tank.dmg` as an asset.
  The appcast's enclosure URL points at
  `releases/latest/download/Tank.dmg`, GitHub's own flat alias for "the
  newest published release's asset of this name" -- so the feed never
  needs to know a specific release tag.

Publishing is automated: `tank3`'s release workflow pushes here using a
token scoped to this repo only (`TANK3_RELEASES_PUBLISH_TOKEN`, held in
`tank3`'s `release` GitHub Environment). See `tank3`'s
`docs/release-packaging.md` ("Sparkle update hosting") for the full design
and wiring.
