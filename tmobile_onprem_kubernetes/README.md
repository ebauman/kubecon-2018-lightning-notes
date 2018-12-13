# How T-Mobile Built and Scaled K8s OnPrem

## T-Mobile Platform Engineering
- Started as a three-person team in May '16
    - Goal: Bring Cloud Foundry to the enterprise
- Now 25-strong supporting IT facing IaaS, CaaS & PaaS platforms wearing many hats
    - Infra Engineers
    - System Admins
    - Devs
    - Platform Admins
    - Product Managers
    - Customer Success Engineers
- Part of a larger organization supporting all On-Premises IT infrastructure for T-Mobile

They had a tough time finding people who were right for this team. They initially looked for CF engineers, but realized quickly that none exist. So they began hiring folks with the right aptitudes. 

## What we manage

- PaaS (Pivotal CF)
    - 12 customer facing foundations in two DCs
    - 34k app instances (containers)
    - 300M+ prod transactions/day
    - Associated hosted platform data svcs (mysql, rabbitmq, redis, gemfire)
- CaaS (K8s)
    - 24 clusters, both single and multi-tenant
        - Mix of open source and vendor deployment
    - 5 live applications
    - ~1m prod transactions/day
- IaaS (BOSH)
    - For platform and customer needs

## Business Impact of PaaS
- Speed to market
    - DevOps teams can onboard and push apps to production same day
    - Some teams went from 6 months dev to prod cycle to weeks
- Increased app perf and reliability
    - Average 43% reduction in app response time
    - 83% fewer incidents, resolved 67% faster
- Deployment agility
    - 10x increase in planned deployments
    - Daytime changes, blue/green deployments, canary testing
- Developer efficiency
    - Platform abstractions let developers focus on development
    - No longer need to manage OS patching, load balancing, certificates - all built into the platform
- Workload consolidation
    - In some cases 12x efficiency gain in HW footprint
    - Adjacent workloads benefit from proximity

*Apparently, they used to pile 100-some developers into a room for a weekend to deploy their tightly-coupled apps and services.*

## The CaaS gap

- No standard offering for teams to run containers
    - They have shadow docker instances 
- Not everything is a good fit for CF
    - Non-native containers
        - Vendor-supplied docker containers becoming more common
        - Lift & shift
    - Non-HTTP/HTTPS traffic management limited
    - No persistent storage
        - NFS volume services available for PaaS, *but a trap*
        - Platform data services met some, but not all application needs
- No platform orchestration
    - Complex/stateful application management needs to be external

## Why On-Premises?
- Data Center Gravity
    - Data
        - Beyond the Chandrasekhar limit? 
    - Network
        - Latency matters
    - Security
        - On-premises controls and patterns well understood
    - Organizational
        - Lack of public-cloud expertise
        - Most compliance
    - Cost
        - Strong economies of scale in data center - *if* we execute
        - Capex vs Opex
- Destiny
    - Own it
- Public cloud available
    - Public Cloud team offers K8S and many other services

## CaaS Requirements

- Platform team:
    - Highly available at every level
        - Control plane
        - Worker nodes
        - Authn/Authz
    - Automated deployment
        - Control plane (OpsMan/Bosh)
        - Cluster builds
    - No downtime lifecycle management
        - K8s upgrades
        - OS patching
        - Infra maintenance
    - LDAP integration
    - API configurability
    - Automated ops
- DevOps Team
    - Native K8s experience
    - Container orchestration
    - PaaS-like support experience
        - OOTB cert/load balancing
        - OS patching
        - INfra maintenance
        - Persistent storage
        - Single AZ
        - Cross AZ replication
        - Cross cluster replication
    - TCP ingress
        - Service type `LoadBalancer`

 