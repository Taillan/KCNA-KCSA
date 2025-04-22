# KCNA-note
Yes I did KCNA after CKAD CKA and CKS

# Ressources
https://app.exampro.co KCNA Free tier have class and Exam
ALl is there : https://notes.kaiwalyakoparkar.com/kcna/

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

In Kubernetes, controllers are control loops that watch the state of your cluster, then make or request changes where needed. Each controller tries to move the current cluster state closer to the desired state.

The cloud controller manager lets you link your cluster into your cloud provider's API, and separates out the components that interact with the cloud platform from components that only interact with your cluster.

EndpointSlices
EndpointSlices provide a simple way to track network endpoints within a Kubernetes cluster. They offer a more scalable and extensible alternative to Endpoints.

CNI = A specification and a set of libraries that enable plugins to configure network interfaces for containers in Kubernetes.
Correct. The Container Networking Interface (CNI) is a standardized specification that provides a framework for configuring networking in containerized environments, including Kubernetes. It defines how network plugins should configure network interfaces and apply network policies for containers. CNI allows Kubernetes to integrate various networking solutions (such as Calico, Flannel, or Cilium) by providing a consistent interface for setting up pod networking.

A specification and a set of libraries that enable plugins to configure network interfaces for containers in Kubernetes.

The RBAC API declares four kinds of Kubernetes objects: Role, ClusterRole, RoleBinding and ClusterRoleBinding.

When managing the scale of a group of replicas using the HorizontalPodAutoscaler, it is possible that the number of replicas keep fluctuating frequently due to the dynamic nature of the metrics evaluated. This is sometimes referred to as thrashing, or flapping. It's similar to the concept of hysteresis in cybernetics.

What are the six layers of the CNCF landscape?
- App Definition and Development
- Orchestration & Management
- Runtime
- Platform
- Provisioning
- Observability and Analysis

What is a fast serverless framework for Kubernetes with a focus on developer productivity and high performance?
Fission
Serverless Functions as a Service for Kubernetes.

# KCSA

## RessourceQuot vs Limit Quota
RessourceQuota = Limit for namespace
LimitRange = limit for pod ressource

# Kyverno
Kyverno is an admission controller that enable writing and enforcing policies as kubernetes ressource

## securityContext
### Pod level
runAsUser, fsGroup, seLinuxOptions
### Container level
priviledged

## Trivy
Command : trivy image --severity HIGH, CRITICAL myapp:latest


