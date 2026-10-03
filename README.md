# Helix container releases

This repository publishes Helix release information and GHCR image references. Application source, build scripts, tests, and deployment configuration are maintained separately.

## Current release

**0.1.0-arm64.1** is a Linux ARM64 preview. The image is published on GHCR and anonymous access was verified.

```bash
docker pull --platform linux/arm64 ghcr.io/mycelpf/mycel_helix:0.1.0-arm64.1
docker run --rm --platform linux/arm64 ghcr.io/mycelpf/mycel_helix:0.1.0-arm64.1 helix --help
```

Use the immutable digest when pinning a deployment:

```text
ghcr.io/mycelpf/mycel_helix@sha256:f1a8a3098c28ca631f61a6fa5ec7b4a2e73a7ebe4d5c1d483b28e173828c8473
```

## Release evidence

[Release notes](https://github.com/mycelpf/mycel_helix/releases/tag/v0.1.0-arm64.1) and [verification evidence](releases/0.1.0-arm64.1/evidence.json) identify the image and checks performed.

The published image was pulled by digest and its CLI startup verified. Architecture, shared libraries, model cache, and certificate presence were also checked. These checks validate image packaging; they do not establish Kubernetes rollout, application journeys, or licensing behavior.

Customer content, credentials, and deployment licenses are supplied separately. Container images are the distribution format; there is no Homebrew package.
