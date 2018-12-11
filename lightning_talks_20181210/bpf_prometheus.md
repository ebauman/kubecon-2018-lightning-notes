# Monitoring K8s with BPF and Prometheus
Jonathan Perry, Flowtune

## Why do you want flow monitoring data? 

1. You can get a complete picture of your application architecture
2. "Do I have a service dependency I don't know about?"
3. Discover unhealthy interactions, even upstream
3. Can help monitor costs for public cloud deployments, esp when doing cross-AZ stuff

## Getting Flow Data

(see screenshot on phone)

## How to get data efficiently?

*Use eBPF*

Check out the notes for this one. This seems a bit intimidating to do.
We should probably stand up and check out Prometheus. 