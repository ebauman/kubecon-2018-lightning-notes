# Spawning Kubernetes in CI for Integration Tests
Marko Mudrinić - Loodse @xmudrii

How to spawn k8s instance?
- There are many tools that can do it, but most require systemd
- Usually CI tools have no access to systemd

## Enter kind
What is kind?
- A tool for running local k8s clusters using docker
- doesn't need systemd
- Only requires docker
- Comes with pre-built Docker image containing all dependencies
- Clusters are provisioned using `kubeadm`
- Customizable cluster provisioning process

`github.com/xmudrii/travis-kind`

^ there are examples of code here

-> Should we be using TravisCI, or is this possible in GitLab onprem? 

## Building Docker Images
- kind creates container with another Docker inside where K8s runs
- How to pass controller's image to Docker running inside kind's container?
- Option 1: run container registry and point kind's docker to it
- Option 2: sideload image
- Sample script for sideloading is available in jetstack/ci-manager ?

`sigs.k8s.io/kind`