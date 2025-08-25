
# KCSA

## The control plane
 - "Node Controller",
 - "Endpoint Controller",
 - "Ingress Controller",
 - "Deployment Controller",
 - "Service Account Controller"

### kube-apiserver
The kube-apiserver acts as the front end of the control plane

Kubernetes does not have an object specifically for limiting concurrent API server requests. Instead, this is typically controlled through API server configuration flags.

![Admission-controll-phases](admission-controller-phases.png "Admission-controll-phases")

### audit logging
To enable audit logging in Kubernetes, you must create an audit policy file, specify this file using the '--audit-policy-file' flag in the API server configuration, and define the log path using '--audit-log-path'. These steps ensure that audit logs are properly configured and stored.
- Create an audit policy file
- Add '--audit-policy-file' flag to API server
- Specify '--audit-log-path' in the API server configuration

### ImagePolicyWebhook 
```yaml
--enable-admission-plugins=ImagePolicyWebhook
```
--admission-control => **Deprecated**

## Kubelet

## debug-level
Set the verbosity level to 4 by adding '--v=4' to the kubelet startup arguments

## Kubectl

### Command
#### Easy
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

#### No Easy
Retrieve a list of all contexts in your kubeconfig file
```bash
kubectl config get-contexts
```

Label a node
```bash
kubectl label nodes NODE_NAME env=production
```

Port-Forward
```bash
kubectl port-forward <pod-name> <local-port>:<pod-port>
```

Share the PID namespace in docker
```sh
docker run --pid=container:container1
```

## Kube ressources

### Service Account
Prevents automatic mounting of the default ServiceAccount token
```yaml
automountServiceAccountToken: false
```

### CNI 
CNI who support Network Policies:
- Calico
- Weave Net
- AWS VPC CNI
- Cilium

### Service
  Service type:
  - ClusterIP
  - NodePort
  - LoadBalancer
  - ExternalName

### AppArmor
Two methode:
1. **Annotations**: Anotate all the container : container.apparmor.security.beta.kubernetes.io/<nom-du-container>: 'localhost/<nom-du-profil>'
2. **securityContext**: User the `appArmorProfile` field

### Ingress
HTTP/HTTPS routing rules and integrate with Ingress controllers to expose services.

### Audit policy rule
```yaml
  # Log the request body of configmap changes in kube-system.
  - level: Request
    resources:
    - group: "" # core API group
      resources: ["configmaps"]
    # This rule only applies to resources in the "kube-system" namespace.
    # The empty string "" can be used to select non-namespaced resources.
    namespaces: ["kube-system"]
```

### NetworkPolicies
Macth all pod : 
  Use empty ``podSelector: {}``

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

### Pod Security Standards

Use a Pod Security Admission to enforce non-root user requirements
#### Pod Security Admission Controller
Pod Security Admission Controller is responsible for enforcing Pod Security Standards in Kubernetes

### RessourceQuot vs Limit Quota
RessourceQuota = Limit for namespace
LimitRange = limit for pod ressource

### Deployment

#### securityContext

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

#### Pod level

runAsUser, fsGroup, seLinuxOptions

#### Container level

priviledged

#### Linux capabilities
capabilities.add

## Tools

### Docker
verify the integrity and authenticity of a container image
A digital signature, public key, and verification tool

### Trivy
Command : trivy image --severity HIGH, CRITICAL myapp:latest

### Kyverno
Kyverno is an admission controller that enable writing and enforcing policies as kubernetes ressource

### Botkube
Slack-based alerts for compliance and security events

## Linux Commands
lists all installed packages
```bash
apt list --installed
```

Lists all processes currently listening on TCP and UDP ports
```bash
sudo netstat -tulpn
```

## Compliance and Security Frameworks

### Supply chain risk
NSA/CISA Kubernetes Hardening Guidance

### Pod Security Admission (PSA) 
Three levels:
| Level      | Description |
| ---------- | ----------- |
| Privileged | Allows the most permissions |
| Baseline   | Moderate security posture suitable for most applications |
| Restricted | Strictest security controls |

** How to try it **
Attempt to create a pod that violates the PSA policy and observe the outcome

### STRIDE
**S**poofing
**T**ampering                Malicious alterations
**R**epudiation              Denial of an action or event
**I**nformation Disclosure
**D**enial of Service
**E**levation of Privileges

### Microsoft Security Development Lifecycle (SDL) 
The Microsoft Security Development Lifecycle (SDL) is a comprehensive framework that integrates security at every phase of software development, including explicit phases for requirements definition, threat modeling, mitigation strategies, and validation

### Sysdig Secure
Q: Which tool is commonly used for real-time compliance monitoring and alerting in Kubernetes environments?

A:Sysdig Secure is a tool designed for real-time compliance monitoring, anomaly detection, and security enforcement in Kubernetes environments. It helps ensure that clusters adhere to security standards and best practices.

### NIST Cybersecurity Framework
NIST SP 800-53 Rev. 5 ecurity and privacy controls specifically for federal information systems
NIST SP 800-190 focuses on cloud computing
NIST SP 800-63 deals with digital identity guidelines
NIST SP 800-171 provides guidelines for protecting controlled unclassified information in nonfederal systems
NIST SP 800-30 is about risk management

Q: Which compliance framework is primarily recognized for emphasizing continuous policy review and network traffic monitoring to enhance security in cloud environments?

A: The NIST Cybersecurity Framework is widely adopted for managing cybersecurity risks and emphasizes continuous monitoring, including ongoing policy review and network traffic analysis, to effectively manage and mitigate risks in cloud and other environments. SOC 1 Type II focuses on financial controls, ISO/IEC 27017 provides guidelines for cloud security controls but does not emphasize continuous monitoring to the same extent, FedRAMP is a U.S. government program for cloud security authorization, and COBIT is a governance framework for IT management rather than specific continuous monitoring practices.

### Data Flow Diagram (DFD) approach
Q: Which methodology involves visualizing application components and interactions to identify potential security threats?

A: The Data Flow Diagram (DFD) approach is a visual representation technique used to map out data paths and interactions within systems, facilitating the identification and mitigation of security threats.
