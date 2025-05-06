
# KCSA

## The control plane

### kube-apiserver
The kube-apiserver acts as the front end of the control plane

Kubernetes does not have an object specifically for limiting concurrent API server requests. Instead, this is typically controlled through API server configuration flags.

![Admission-controll-phases](admission-controller-phases.png "Admission-controll-phases")

### audit logging
To enable audit logging in Kubernetes, you must create an audit policy file, specify this file using the '--audit-policy-file' flag in the API server configuration, and define the log path using '--audit-log-path'. These steps ensure that audit logs are properly configured and stored.
- Create an audit policy file
- Add '--audit-policy-file' flag to API server
- Specify '--audit-log-path' in the API server configuration

## Kubelet

## debug-level
Set the verbosity level to 4 by adding '--v=4' to the kubelet startup arguments

## Kubectl

### Command
Check the version of the Kubernetes API server
```bash
kubectl version
```

Get all pod
```sh
kubectl get pods -A # --all-namespaces
```

Delete all pod in namespace 'test'
```sh
kubectl delete pods --all -n test
```

Update the container image
```sh
kubectl set image CONTAINER_NAME_1=CONTAINER_IMAGE_1
```

detailed information including its configuration and status
```sh
kubectl describe RESSOURCE
```

Retrieve a list of all contexts in your kubeconfig file
```bash
kubectl config get-contexts
```

Label a node
```bash
kubectl label nodes NODE_NAME env=production
```

Share the PID namespace in docker
```sh
docker run --pid=container:container1
```

## Kube ressources

## AppArmor
container.apparmor.security.beta.kubernetes.io/<nom-du-container>: 'localhost/<nom-du-profil>'

### NetworkPolicies
```yaml
---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-all-ingress
spec:
  podSelector: {}
  ingress:
  - {}
  policyTypes:
  - Ingress

```
#### Allow all selector
An empty podSelector {} matches all pods in the namespace, while omitting the field would make the policy ineffective.


## Pod Security Standards

Use a Pod Security Admission to enforce non-root user requirements

## Deployment

### RessourceQuot vs Limit Quota
RessourceQuota = Limit for namespace
LimitRange = limit for pod ressource

### securityContext

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo-4
spec:
  securityContext:
    runAsUser: 1000
    privileged: false
  containers:
  - name: sec-ctx-4
    image: gcr.io/google-samples/hello-app:2.0
    securityContext:
      runAsNonRoot: true
      allowPrivilegeEscalation: false
      capabilities:
        add: ["NET_ADMIN", "SYS_TIME"]
```
``runAsNonRoot: true``

### Pod level

runAsUser, fsGroup, seLinuxOptions

### Container level

priviledged

### Linux capabilities
capabilities.add

## Tools
### Trivy
Command : trivy image --severity HIGH, CRITICAL myapp:latest

### Kyverno
Kyverno is an admission controller that enable writing and enforcing policies as kubernetes ressource

## Linux Commands
lists all installed packages
```bash
apt list --installed
```

## Compliance and Security Frameworks

### Microsoft Security Development Lifecycle (SDL) 
The Microsoft Security Development Lifecycle (SDL) is a comprehensive framework that integrates security at every phase of software development, including explicit phases for requirements definition, threat modeling, mitigation strategies, and validation

### NIST Cybersecurity Framework
Q: Which compliance framework is primarily recognized for emphasizing continuous policy review and network traffic monitoring to enhance security in cloud environments?

A: The NIST Cybersecurity Framework is widely adopted for managing cybersecurity risks and emphasizes continuous monitoring, including ongoing policy review and network traffic analysis, to effectively manage and mitigate risks in cloud and other environments. SOC 1 Type II focuses on financial controls, ISO/IEC 27017 provides guidelines for cloud security controls but does not emphasize continuous monitoring to the same extent, FedRAMP is a U.S. government program for cloud security authorization, and COBIT is a governance framework for IT management rather than specific continuous monitoring practices.

### Data Flow Diagram (DFD) approach
Q: Which methodology involves visualizing application components and interactions to identify potential security threats?

A: The Data Flow Diagram (DFD) approach is a visual representation technique used to map out data paths and interactions within systems, facilitating the identification and mitigation of security threats.