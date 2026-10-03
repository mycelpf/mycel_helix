# Helix container releases

Helix is distributed here as a Linux ARM64 container for laptop and Kubernetes validation. This repository contains release documentation and deployment examples; application source is maintained separately.

The current release is **0.1.0-arm64.1**, an ARM64 preview. No Homebrew installation is needed. Container registry publishing is pending; use the downloadable image archive below.

## Download and verify

With Docker running, download the archive and its checksums:

```bash
gh release download v0.1.0-arm64.1 --repo mycelpf/mycel_helix \
  --pattern 'helix-*.tar.gz' --pattern 'checksums.txt'
shasum -a 256 -c checksums.txt
docker load -i helix-0.1.0-arm64.1-linux-arm64.tar.gz
docker run --rm --platform linux/arm64 mycelpf/mycel_helix:0.1.0-arm64.1 helix --help
```

The loaded image is `mycelpf/mycel_helix:0.1.0-arm64.1`. It is a local image tag, not a published Docker Hub image. The intended registry address is `ghcr.io/mycelpf/mycel_helix`; do not attempt a registry pull until a release explicitly confirms publication.

## Validate in Kubernetes

Use a cluster with ARM64 nodes. Import the loaded image into its container runtime before applying the example. For a kind cluster:

```bash
kind load docker-image mycelpf/mycel_helix:0.1.0-arm64.1 --name YOUR_CLUSTER
kubectl apply -f examples/kubernetes/laptop.yaml
kubectl -n helix-preview rollout status deployment/helix --timeout=300s
kubectl -n helix-preview port-forward service/helix 7373:7373
```

For minikube, use `minikube image load mycelpf/mycel_helix:0.1.0-arm64.1` instead of the kind command. Other clusters require their own image import procedure. The example uses `imagePullPolicy: Never` so it cannot accidentally pull a different image from a registry.

In another terminal, check `curl --fail http://localhost:7373/health`.

This example is for laptop validation: authentication bypass is enabled, the Service is ClusterIP, and there is no public ingress. Do not expose it publicly. It uses one replica and a persistent volume; the cluster needs a default storage class. Application readiness also requires your knowledge content, storage-engine bundle, database connection, and production authentication configuration. A successful health probe alone does not validate policy CRUD or licensing.

## Release contents and verification

The image contains the Helix binary, embedded UI, embedding model cache, native libraries, and trusted certificates. Customer content, credentials, and deployment licenses are not bundled into the image.

See [release evidence](releases/0.1.0-arm64.1/evidence.json) for the image identity and checks performed. Binary startup, native libraries, model cache, certificate presence, and archive architecture were verified. Kubernetes rollout is an example to run locally; it has not been executed as part of this release.
