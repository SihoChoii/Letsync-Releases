# Letsync downloads

Public distribution repository for Letsync desktop builds and update metadata.
Application source is maintained separately in a private repository.

Testing, building, and packaging run on the maintainer's device. GitHub hosts
source, downloads, and update metadata; GitHub Actions is disabled in both
repositories. Publishing uploads the locally built archive through the GitHub CLI.

## Channels

| Channel | Branch | Update metadata | Downloads |
| --- | --- | --- | --- |
| Stable | `stable` (default) | [stable.json](https://raw.githubusercontent.com/SihoChoii/Letsync-Releases/stable/channels/stable.json) | [Latest stable release](https://github.com/SihoChoii/Letsync-Releases/releases/latest) |
| Beta | `beta` | [beta.json](https://raw.githubusercontent.com/SihoChoii/Letsync-Releases/beta/channels/beta.json) | [Releases, including prereleases](https://github.com/SihoChoii/Letsync-Releases/releases) |

Stable releases use versions such as `1.0.0`. Beta releases use versions such as
`1.0.0-beta.1` and are marked as prereleases. Beta publication leaves the stable
channel unchanged. Both channels start empty: a manifest's `version: null` and
empty `assets` array mean no release is available.

## Downloads and checksums

Download the archive matching your operating system and architecture from a
release's **Assets** list. Each release includes SHA-256 checksums. GitHub's
automatically generated source archives contain this distribution repository's
metadata; they are not the desktop app.

Current publishing produces one platform/architecture archive per version.
Builds are unsigned, and in-app automatic update installation is not configured.

## Update metadata

The canonical stable endpoint reads `channels/stable.json` from the `stable`
branch. The canonical beta endpoint reads `channels/beta.json` from the `beta`
branch. Use the links above; the other branch's copy may be stale.

Each manifest contains `schemaVersion`, `channel`, `version`, `tag`, `releaseUrl`,
`sourceCommit`, `publishedAt`, and `assets`. Each asset has `platform`, `arch`,
`name`, `url`, `sha256`, and `size` in bytes. Published release tags are `v<version>`.
These are release discovery manifests, not electron-updater metadata.

Maintainers publish from the matching branch of the source checkout with
`npm run release:publish -- --channel stable` or `--channel beta`, following the
private source repository's release guide. Keep application source and credentials
out of this repository.
