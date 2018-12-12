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

- Add pod labels as to where the pods are going to live (e.g. AZ)
- Add anti-affinity labels so the pods don't start in AZs they don't belong to

## 02 Control Plane HA

- apiserver
    - apiserver is completely stateless, so all master nodes can run it active-active. LB in front of it, and you're done
- scheduler & controller-manager
    - within k8s, a locking system exists so that scheduler and controller manager instances have only one active at a time. active-passive
- configuring leader election
    ```
    --leader-elect
    --leader-elect-lease-duration
    ...
    ```

- Managing the control plane
    - unsolved problems
        - health checking
        - failure recovery
        - upgrades without downtime
    - options to explore:
        - hosted solution
        - managed instance groups
        - build your own monitoring server
        - k8s itself! 
