# VIND Tutorial

### Prerequisites

- Docker 
- Kubectl
- Login to ghcr.io (docker login ghcr.io) - create and github token as password/

### Install VCluster CLI

```
# macOS
brew install loft-sh/tap/vcluster

# Linux
curl -L -o vcluster "https://github.com/loft-sh/vcluster/releases/latest/download/vcluster-linux-amd64" && \
sudo install -c -m 0755 vcluster /usr/local/bin && \
rm -f vcluster

# Windows
# Download from https://github.com/loft-sh/vcluster/releases
```

### Configure VCluster to use Docker as the driver

`vcluster use driver docker`

### Create a Kubernetes cluster

`sudo vcluster create test-cluster`

### Create a multi node kubernetes cluster

Step 1: Prepare the configuration using values.yaml

```
experimental:
  docker:
    nodes:
    - name: "worker-1"
      ports:
        - "9090:9090"
    - name: "worker-2"
      volumes:
        - "/tmp/data:/data"
      env:
        - "NODE_ROLE=worker"
```

Step 2: Verify the mount path exists (only if you are using volumes)

`mkdir -p /tmp/data`

Step 3: Create cluster

```
sudo vcluster create multi-node-cluster --values values.yaml
```

### VCluster commands

- `vcluster ls`
