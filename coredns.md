# CoreDNS over gRPC: Reliable Service Discovery for Kubernetes

Yong Tang, MobileIron

`github.com/yongtang`

Maintainer, CoreDNs, Docker/Moby
Maintainer and SIG I/O Lead, TensorFlow

## CoreDNS
- Flexible DNS server witten in Go
- Plugin based architecture, easily extended
- Supports DNS, DNS over TLS, DNS over gRPc
- CoreDNS has a focus on service discovery
- Native K8s Integration (GA in k8s 1.11, default in 1.13)
- CNCF incubating project

## Service Discovery with DNS
- DNS is a nice and flexible indirection
- DNS is easy and simple, for Dev/DevOps/IT
- DNS has been there for a long time & part of the existing IT infrastructure
- Works with hybrid environments (in & out of k8s cluster)
- DNS is distributed in nature, scales really well

## DNS Limitations
- DNS (UDP) is not reliable and secure
- UDP performance could be misleading for DNS
- Jumbo frames not utilized (e.g. MTU 9001 vs 1500 on AWS)
- Hard to diagnose, no error code
- Service error vs. DNS infrastructure error

## CoreDNS over gRPC
- DNS/UDP over local host communications
- gRPC/TLS over cross host comunication
- Intermediate CoreDNS (cache) to Kubernetes api server

[ graphic ]

Pods comm to on-host coredns using udp

Nodes comm to API host using grpc, tls


- Front-end compatibility
    - Same DNS for service discovery
    - No implementation or configuration changes for appliations
- Reliable and secure back-end communications
- Scales well with layered caching

