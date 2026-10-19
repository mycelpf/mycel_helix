# Helix container releases

This repository publishes Helix release information and GHCR image references. Application source, build scripts, tests, and deployment configuration are maintained separately.

## Current release

**0.1.1** is published on GHCR for Linux on x86_64 (`linux/amd64`) and ARM64 (`linux/arm64`) under one tag. Docker selects the matching platform; anonymous access was verified for both.

```bash
docker pull ghcr.io/mycelpf/mycel_helix:0.1.1
docker run --rm ghcr.io/mycelpf/mycel_helix:0.1.1 helix --help
```

Use the immutable digest when pinning a deployment. It covers both platforms:

```text
ghcr.io/mycelpf/mycel_helix@sha256:3d2a723bd991a597c3f7f32c2d51f55d3c433c34f741942af9b7b123af7180e5
```

| Platform | Image digest |
| --- | --- |
| linux/amd64 | `sha256:8b94a54c8b6787caaf7a4904ffbcfda89025d22bab291cbfa07b872a9fdca7f6` |
| linux/arm64 | `sha256:f79a33ea8f89e0cb7022a7fa1c7f826ea9b38228d25effa28258031832206f34` |

AWS App Runner runs x86_64 only and pulls from Amazon ECR; copy the `linux/amd64` image to ECR for it.

Raters imported with an earlier release must be imported again: 0.1.1 stores rater models in a new format.

## Release evidence

[Release notes](https://github.com/mycelpf/mycel_helix/releases/tag/v0.1.1) and [verification evidence](releases/0.1.1/evidence.json) identify the image and checks performed.

Each platform image was pulled by digest without credentials. Its CLI startup and licensing reader gate passed, a workbook was imported, published and rated through the Rule Runner API, and its file system contained no spreadsheet, environment or credential files. These checks validate image packaging and the Rule Runner path; they do not establish Kubernetes rollout or licensing behavior.

## Previous releases

| Version | Platforms | Evidence |
| --- | --- | --- |
| 0.1.0-arm64.1 | linux/arm64 | [evidence](releases/0.1.0-arm64.1/evidence.json) |

Customer content, credentials, and deployment licenses are supplied separately. Container images are the distribution format; there is no Homebrew package.
