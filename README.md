# fluidsynth-ffmpeg

FluidSynth with FFmpeg, for rendering MIDI files to MP3, Opus, AAC and the other formats that FFmpeg encodes.

This image is the default image of [fluidsynth](https://github.com/randomcontainers/fluidsynth) (`ghcr.io/randomcontainers/fluidsynth:latest`), published under its own name. The contents are the same; the digests differ. It contains FluidSynth and FFmpeg, on Ubuntu or Alpine, for `linux/amd64` and `linux/arm64`.

These are unofficial builds, not affiliated with or endorsed by the upstream projects. Report problems with the image in [randomcontainers/fluidsynth](https://github.com/randomcontainers/fluidsynth/issues) and problems with a tool itself in that tool's own issue tracker.

## Quick start

```sh
docker run --rm --user "$(id -u):$(id -g)" -v "$PWD:/work" ghcr.io/randomcontainers/fluidsynth-ffmpeg -ni -F song.wav FluidR3_GM.sf2 song.mid
```

The examples in the [fluidsynth README](https://github.com/randomcontainers/fluidsynth#readme) work with this image too.

## Tags

`<version>` is the FluidSynth version.

| Tags | Base |
|---|---|
| `latest`, `<version>`, `ubuntu`, `<version>-ubuntu`, `<version>-ubuntu26.04` | Ubuntu 26.04 |
| `alpine`, `<version>-alpine`, `<version>-alpine3.24` | Alpine 3.24 |

`latest` and `<version>` are the Ubuntu 26.04 images. The images are currently built on Ubuntu 26.04 and Alpine 3.24. Tags without a distro version move to the next distro release when the project does; tags ending in `ubuntu26.04` or `alpine3.24` stay on that release and are no longer rebuilt once the project moves to the next one.

Only the tags of the FluidSynth version currently in [fluidsynth's package.yml](https://github.com/randomcontainers/fluidsynth/blob/main/package.yml) are rebuilt, exact-version tags included, so pin a digest when you need the same bytes every time. Tags of older versions stay as they were last built. The published tags and their digests are listed on the [package page](https://github.com/orgs/randomcontainers/packages/container/package/fluidsynth-ffmpeg).

## Platforms

`linux/amd64` and `linux/arm64`, both built natively on GitHub-hosted runners.

## Files and permissions

The working directory is `/work`. The image runs as UID 1000, and any other UID works too: `HOME` is then `/`, and caches go to `/cache`, which anyone can write to. How to get output files owned by you depends on how you run containers:

| Runtime | Flag |
|---|---|
| Docker on Linux (rootful), GitHub Actions | `--user "$(id -u):$(id -g)"` |
| Rootless Podman | `--userns=keep-id` |
| Rootless Docker | `--user 0:0` (root in the container is your user on the host) |
| Docker Desktop on macOS or Windows | none, file ownership is mapped for you |

## Contents

| Package | License | Repository |
|---|---|---|
| [FluidSynth](https://www.fluidsynth.org/) | `LGPL-2.1-or-later AND Apache-2.0 AND CC0-1.0 AND LicenseRef-Public-Domain` | [randomcontainers/fluidsynth](https://github.com/randomcontainers/fluidsynth) |
| [FFmpeg](https://ffmpeg.org/) | `GPL-3.0-or-later AND MPL-2.0 AND BSD-3-Clause AND Zlib AND Unlicense` | [randomcontainers/ffmpeg](https://github.com/randomcontainers/ffmpeg) |

## Verifying

Each image has a build provenance attestation from this repository's GitHub Actions run. The run uses the shared build workflow of [randomcontainers/ci](https://github.com/randomcontainers/ci), which signs the attestation, so name both repositories:

```sh
gh attestation verify oci://ghcr.io/randomcontainers/fluidsynth-ffmpeg:latest \
  --repo randomcontainers/fluidsynth-ffmpeg --signer-repo randomcontainers/ci
```

Images from `ghcr.io/randomcontainers/fluidsynth` are built in [randomcontainers/fluidsynth](https://github.com/randomcontainers/fluidsynth), so verify them with `--repo randomcontainers/fluidsynth --signer-repo randomcontainers/ci`.

## Updates

The images are rebuilt when a new image of a package above is published, for example after an upstream release. They are also rebuilt when the base image changes and at least every 7 days, so distro security fixes reach the current tags. The package repositories describe how each upstream release is picked up.

## Licenses

The image contents are licensed under `LGPL-2.1-or-later AND Apache-2.0 AND CC0-1.0 AND LicenseRef-Public-Domain AND GPL-3.0-or-later AND MPL-2.0 AND BSD-3-Clause AND Zlib AND Unlicense`. The version of each package is in `/usr/local/share/randomcontainers/<package>/version` and its license files are in `/usr/local/share/randomcontainers/<package>/licenses/`.

Corresponding source:

- FluidSynth: [randomcontainers/fluidsynth](https://github.com/randomcontainers/fluidsynth#licenses) has a `v<version>` release with the source of each FluidSynth version it builds.
- FFmpeg: [randomcontainers/ffmpeg](https://github.com/randomcontainers/ffmpeg#licenses) has a `v<version>` release with the source of each FFmpeg version it builds.

Ubuntu and Alpine packages keep their own licenses. The SBOM of each platform image lists them with their versions:

```sh
docker buildx imagetools inspect ghcr.io/randomcontainers/fluidsynth-ffmpeg:latest --format '{{ json .SBOM }}'
```

The files in this repository are available under the MIT license, see [LICENSE](LICENSE).

## Requesting a tool

To suggest another tool, use the [Request a tool](https://github.com/randomcontainers/.github/issues/new?template=tool-request.yml) form.

## This repository

The files here are generated from the `combos` section of `package.yml` in [randomcontainers/fluidsynth](https://github.com/randomcontainers/fluidsynth). Open issues and pull requests there.
