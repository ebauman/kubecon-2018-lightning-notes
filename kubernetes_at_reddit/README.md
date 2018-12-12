# Kubernetes at Reddit: An Origin Story
Greg Taylor - EM, Reddit Infrastructure
u/gctaylor

---

## 2016 - The Infrastructure Team

- Provisioned and configured all infrastructure
- Operated most of our system
- Responded to most incidents

## Mid-2016 and onward: The Great Embiggening

- Grown from ~20 engineers to >200

## Determining the path forward

They decided to pick apart the monolith and turn it into an SOA. 

## Growing pains

- Problem: Eng teams too dependent upon infra team
    - Service provisioning
    - Ongoing operation
    - Debugging and performance work
- Short-term "solution": Train and deputize infrastructure-oriented teams
    - Allows for more self-sufficiency
    - *Only possible for some teams*

## Service ownership

A service owner at reddit is empowered and expected to:
- Develop their service from start to finish
- Deploy their service early and often
- Operate their service

## InfraRedd

> Mission: A service owner should be able to develop, deploy, and operate their service. *Regardless of engineering background.*

## Develop: Consistency in service

Regardless of language/toolset, the "shape" of each service should be consistent:
- RPC protocol
- Secrets fetching
- Metrics
- Tracing
- Log output format

Baseplate: https://baseplate.readthedocs.io

## Develop Service creation

Auto-generate starter material:

- Service sources
    - Python/go/node service stub
    - Dockerfile
    - CI configs
- Helm charts
    - Friends don't let friends write YAML!

## Develop: "Local" development

Development is facilitated by [Skaffold](https://github.com/GoogleContainerTools/skaffold).

Major considerations:
- Accessible to those without deep kubernetes experience
- As similar to production as possible
- Re-use our standard Charts + images
- *Must not exhaust standard dev laptop's resources*

## Deploy: Test, builds, deploys

- CI runs through Drone
    1. Tests
    1.  Artifact builds
- Spinnaker handles our deploys
    1. Standardized pipeline templates
    1. Renders Helm charts
    1. Applies rendered YAML
    1. Uses V2 Kubernetes provider

## Deploy: Standard staging/production flow

1. Developer pushes to canonical repo

1. Tests and builds run in CI

1. One of two flows are offered:
    1. CI triggers a deploy
    1. Eng manually triggers a deploy

## Operate: Explicitly defined expectations

- Service owner
    - Learn some kubernetes basics
    - Deploy and operate own services
- Infrastructure team
    - Keep the k8s clusters running
    - Provision AWS resources, caches, DBs
    - Suppoer and advise Product Users

## Operate: Paint-by-numbers

Enabling service ownership for all backgrounds:
- Take the guesswork out
- Document all the things
- You want to do X? Here's a guide for that
- Must be supported by training!

## Operate: Service owner permissions
- Service owners auth via OpenID Connect
- RBAC policies are group-based
- Namespace per service
- Service owners have full access to their namespace(s).

## Operate: Guardrails
Things that prevent or minimize damage:
- Resource limits and Network Policies
    - Built into K8s
- Throttling and circuit breaking
    - Envoy + Istio
- Object and Image policies
    - Open Policy Agent
- Finely scoped RBAC
    - Open Policy Agent

## Operate: Oh no!

Something exploded!

- Service owner:
    1. Paged for service incident
    1. Diagnoses + resolves issues
    1. Can summon Infra if needed
- Infrastructure team:
    1. Paged for cluster issues
    1. Those *never* happen. Yep.

*Blameless postmortems are very important*

## Operate: Observe, Diagnose, Resolve

Obeservability by *default*:

- Metrics
    - Wavefront
- Altering
    - PagerDuty
- Tracing
    - Zipkin
- Exception/error tracking
    - Sentry
- Central logging and analysis