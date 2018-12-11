# Highly Available Kubernetes Clusters - Best Practices
Meaghan Kjelland & Karan Goel, Google

---

## What is high availability?

High SLO (service level objective). You have a certain level of availability that you have promised. 

The conversation now is how do we achieve that? 

## High Availability? Or Multi-Master?

Multi-master is *not enough*

Eliminating every single point of failure in each layer of the stack.

- Control plane
- Networking
- Application
- Persistence

## GKE

GKE has concepts of regions, and zones. 

Regions are geographical failure domains, so like Iowa, Los Angeles, etc. 

Zones are failure domains within regions. Different cooling, etc. 

## Talk has three sections

1. Application
    - webapp
2. Control plane
    - controller-manager
    - scheduler
    - apiserver
3. Data plane
    - etcd

## 01 Application HA

[this entire talk can be summed up as: run it across failure domains]

What is "it"? 

Yes. 