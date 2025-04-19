# KCNA-note
Yes I did KCNA after CKAD CKA and CKS

Select information for fields such as name, namespace or status of a Kubernetes object
'''bash
kubectl get RESSOURCE --filed-selector foor.bar=baz
kubectl get pods --field-selector status.phase=Running
'''

In Kubernetes, namespaces provides a mechanism for isolating groups of resources within a single cluster.

Container Runtime Interface 
The CRI is a plugin interface which enables the kubelet to use a wide variety of container runtimes, without having a need to recompile the cluster components.

CoreDNS has been the default name Domain Name System (DNS) since K8s 1.3

The TTL-after-finished controller is only supported for Jobs. You can use this mechanism to clean up finished Jobs