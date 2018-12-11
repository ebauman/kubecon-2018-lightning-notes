# Front-end Application Deployment Patterns
Ross Kukulinski - Sr. Product Manager, Heptio
@rosskukulinski

---

## Customer Personas
1. Platform Engineer
2. Backend Architect
3. CIO
4. Web Developer

## Deployment Patterns

1. DO NOT edit files in production
2. Rolling update
3. Blue-green
    1. Requires double the compute resources as you need to have two versions running. 
4. Canary

### Rolling update

- Deployment with pods labeled as `app: my-app`
- The pods have a `pod-template-hash`, which is different based on changes to the pod template. 
- When a rolling update is executed, k8s stands up a new ReplicaSet, and spins up pods. When one pod is spun up in the new RS, another is terminated in the old set. 
^ This is the default behavior
- There are tunable knobs here, for max pods being deployed, or max pods unavailable at any given time

### How does rolling update work for a web app? 

If a web user requests a page (say index.html), there are embedded resources (css, js). 
When a user requests those resources, they may get resources from a v2 replicaset instead of v1. Then that's not good! 

### Blue-Green

```
app: my-app
version: blue
```

Now you can have two replicasets with different versions. Same app label, but different version label.

Blue-green deployment is good for HTML+JS+CSS. 

Caveat: You need double the compute resources to pull this off. 

### Canary

*recommendation: don't start with canary deployments*

podspec:
```
app: my-app
version: stable
```

However, service:
```
app: my-app
```

Thus, there can exist two replicasets where some requests go to the `version: stable`, and others go to `version: canary`. This is redirecting _some_ traffic to the canary. 

## Deployment recap
 [graphic on your phone]

## Workarounds

1. Ignore your problems! 

    If your app is not significantly utilized, perhaps you can tolerate these issues. If some users see issues, maybe that's tolerable for your business. 

2. Schedule maintenance window

    Again, this is dependent upon biz reqs

1. Versioned assets via CDN
    
    Instead of hosting your assets locally, put them into a CDN. Then have your assets served via that, and you eliminate the problems when users roll onto the new deployment. 

    Use *versioning* here so you can coordinate release of new asset versions to coincide with new app (html, whatever) releases. 

1. Session affinity

    ```
    kind: Service
    apiVersion: v1
    spec:
        selector: 
            app: my-app
        sessionAffinity: clientIP
    ```

    Caveat: sometimes your cloud load balancer will not send through the client IP

1. HTTP/2

    1. Single multiplexed connection
        - No sticky session policy required since there is only one TCP session opened here
    1. Binary protocol, instead of text based
    1. Reduced additional RTT

## Kubernetes Ingress

Ingress provides a way to route requests to Services based on the request host or path.

*This is Layer 7 Load Balancing*

There are many kinds: Nginx, Contour, Traefik, GCE, etc. 

### Heptio Contour

- Envoy as the data plane
- Co-development project Yahoo JP corp subsid.
- Dynamically updates without dropped connections
- Performance tested to millions of concurrent connections

### Ingress API is limited

- Only one Service per path
- Can't weight shift traffic across multiple Services
- Can't force http->http redirect
- Not safe for multi-team use <- What does that mean?

### Heptio Contour Ingress CRD

- Lets you do weighting
- Ingress session affinity types:
    - Cookie
    - Header
    - Source-IP hash
    - IngressRoute support not implemented yet! 
    - Nginx through cookie annotations
        - `nginx.ingress.kubernetes.io/affinity: cookie`

### Putting it all together
- Rolling vs Blue-Green vs Canary
- HTTP/2 and/or Session Affinity
- Learn what your cloud load provider supports
- Versioned static assets via CDN
- Use K8s Ingress
    - Heptio Contour? :) 