# CRDs aren't just for add-ons anymore
## Painting a picture of the future
### _Tim Hockin, Google_ @thockin

_This talk is forward looking_

CRDs gave birth to Operators, which are software components that manage something inside of a k8s cluster.

Custom abstractions to automate almost anything

CRDs now have admission controllers, which allow you to modify incoming requests. How? By webhooks, so you can validate, etc. Now there are also schemas. 

Doing these things make CRDs feel like 1st class members of the k8s api.

What are CRDs being used for?
- Add-ons
- Stateful orchestration (MySQL)
- Domain specific APIs (Istio)
- Higher levels of abstraction (e.g. kNative)

More recently:
- Storage Snapshots (integrates w/ PersistentVolumes)
- RuntimeClass
- CSI

CRDs are no longer 2nd class

## Vision

All new APIs should be CRDs, unless they can't be. 

Eventually: everything becomes a CRD.

** Underlying goal: There should be nothing that we (k8s) can do that you can't. **