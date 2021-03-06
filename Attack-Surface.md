# Attack Surface 

## Access to Node/VM

Nodes are bare-metal machines or VMs and are a viable point of entry for attackers. Server hardening should be carried out to ensure no uneccesary open ports etc. 
An attacker able to gain access to a node (especially with privs) will more than likely be able to compromise the entire cluster.

## Access to ETCD API

The key value datastore for the entire cluster - Even read only access to the ETCD datastore can provide an attacker with information on how to compromise the entire cluster.
In most cases ETCD is run on a private network/VPC however TLS certificates are essential to ensure only authorised agents can communicate with the datastore.

## Kube API server

The API server should be the only k8s component accessible from outside the cluster. TLS certificates should be implemented to protect the API.

## Control plane traffic

Control planes will be on private networks/VPC but should still use TLS certificates for security. Attackers that gain access to a master node (control plane) can replace 
k8s modules with modules containing malware. Server hardening and rotating credentials/certificates should be carried out regularly.

## Kubelet

The module that communicates with the k8s API server and container runtime. TLS certificates should be used, ensure secrets aren't baked in.

## Application traffic

It is necessary to ensure that applications are isolated within containers. Applications should not run with root privilege and should prevent privilege escalation by 
application components. Application open ports should be limited, and volumes mapped from the host should be limited.

## Container runtime

Containers require their own level of security. Images should be scanned for vulnerabilities before being stored in a secure repository. Images should always be pulled
from a secure repository. Running the latest images is recommended and kubernetes should be configured to always pull images from the repository on each execution.

### Container breakout

factors that can lead to breakout include:
* kernel vulns - containers share the same kernel
* bad configurations - ensure pods/containers don't run as privileged
* mounted filesystems - mounting host filesystems enable attackers to modify the filesystem and escalate host privs
* mounted network sockets - mounting the runtime daemon socket inside a container - allows trivial breakout

# Security boundaries

### Cluster
Consideration should be given to allocate clusters to specific domains such as test, dev, staging, prod etc for various levels of required hardening at each stage and reduce risk accross domains.

### Node
Nodes may serve one or more control plane, worker node etcd... Sensitive workloads should be seperated by assigning pods to specific nodes by using *nodeSelector, node or pod affinity* The *nodeAuthorizer* is key to limiting the blast radius of a compromised pod or node.

### Namespaces
RBAC will implement Namespaces as the basic unit of authorisation. Admission control is applied at the namespace level and prevents depletion of resources (stealing data) as well as preventing DoS style attacks.

### Pod 
All containers in a pod are guarenteed to only run on the node hosting the pod. This architecture helps with the scope of security context and policies. Network policies at the pod level should be used to further enhance isolation of workloads.

### Container
Containers are essentially a combination of cgroups, namespaces, and copy-on-write filesystems. Pod restraints on container runtimes may provide added isolation and security, but, sandboxing and runtime protection is needed to further protect systems.
