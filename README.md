# automation-developer-hub

TODO: Description

## Configuration

Install OpenShift GitopsOperators.
TODO: install using sh script for OpenShift GitOps and use argo for Tekton and Devspaces

## Utils

### Execution environment image for Tekton

```sh
# from app repository root path
export IMAGE_VERSION=1.0.0

# build image
podman build -t testing-ee:$IMAGE_VERSION utils/testing-ee-image/.

# push to quay
podman tag testing-ee:$IMAGE_VERSION quay.io/demo-applications/testing-ee-image:$IMAGE_VERSION
podman push quay.io/demo-applications/testing-ee-image:$IMAGE_VERSION

# REMEMBER TO MAKE IMAGE PUBLIC
```

## To Do

```
└─ automation-developer-hub
   ├─ environment
   │  └─ setup-job.yaml
   │     ├─ line 19: TODO : Read CONFIGURATION using a configmap
   │     └─ line 27: TODO : create required repositories
   └─ README.md
      ├─ line 3: TODO : Description
      └─ line 8: TODO : install using sh script for OpenShift GitOps and use argo for Tekton and Devspaces
```
  