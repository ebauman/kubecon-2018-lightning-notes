# Day Two Kubernetes - Tools for Operability
### Bridget Kromhout & Zachary Deptawa, Microsoft
### @bridgetkromhout, @zdeptawa
--- 

*"Spoiler alert, I will not be live-tweeting this talk"*

--- 

## What is cloud?

Picking a cloud is about selecting the right level of abstraction for you, for your workloads, etc. 

It is okay to get to your desired level of abstraction! 

## What are containers?

"They are not real" - Jessie Frazelle

They are process isolation, resource utilization limits, etc. 

## What is Kubernetes?

Kubernetes is an open-source platform designed to automate deploying, scaling, and operating application containers.

K8s is a work in progress, so don't have tech FOMO! 

---

Microservices shuffle complexity, not solve it. - @zdeptawa

--- 

# kubernetes operability tooling (aka what we're talking about)
- Getting started with Terraform & managed k8s
- Managing configs with Helm & apps with Draft
- Event-driven scripting with Brigade & Kashti
- Packaging distributed apps with CNAB & Duffle

## Terraform

Deploy k8s clusters, pods, and services!

Has the concept of providers, so you can deploy nodes, etc. on different providers such as Azure, AWS, etc. 

You can write your own provider hook if one doesn't exist.

## Azure Kubernetes Service (AKS)

[several code examples about aks functions]

[shows a demo about using terraform with aks]

## Helm

### What is helm?
It is a package manager for k8s. 

*I'm so sorry if yaml upsets you, but there's going to be lots of it - Bridget Kromhout*

`helm rollback` 

*Helm rollbacks are a damn dirty lie - Bridget*

[helm.sh](helm.sh)

## Draft

Simple app development and deployment - into any k8s cluster

- Draft helps you to generate helm and k8s files based on autodetect of language

*Look into this!*

[draft.sh](draft.sh)

## Brigade

Run scriptable, automated tasks in the cloud - as part of your K8s cluster

You can use brigade to write pipelines, interwoven tasks, etc. 

[brigade](brigade.sh)

## CNAB

Cloud Native Application Bundle

CNABs facilitate the bundling, installing and managing of cloud-native apps - and their coupled services. 

## Duffle

## The future

Winter is coming. That is, kubernetes is being used by big companies. By your banks, airlines, etc. 

