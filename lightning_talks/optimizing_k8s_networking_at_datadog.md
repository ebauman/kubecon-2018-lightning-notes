# Optimizing Kubernetes Networking at Datadog

## Challenges
- Throughput - trillions of data points daily
- Scale 1000-2000 node clusters
- Latency
- Topology

## Addressing this in Kubernetes
1. IPVS
    1. Native Load-Balancer
    2. Still a bit young
    3. More efficient than iptables
2. No briding
    1. Route on the host
    2. Specific NI plugins
    3. Better latency
    4. Less cpu usage
3. Native pod routing
    1. pods get standard IPs
    2. No overlay overhead
    3. cross-cluster is easier
    4. ...

## Native pod routing
1. On premises
    1. BGP
        1. Calico
        2. kube router
2. AWS
    1. Additiona IPs on ENIs
        1. AWS EKS CNI plugin
        2. Lyft CNI plugin
3. GCP
    1. IP aliases
        1. Specific controller config

