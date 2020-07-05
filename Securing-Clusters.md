# TLS
TLS certificates should be implemented throughout the cluster. Production environments with exposed endpoints should carry out regular certificate rotation. Certificate expiration can be implemented but isn't always recommended at cluster level. A certificate policy in security context for pods and ReplicaSets is extremely important. https://kubernetes.io/docs/tasks/tls/

# Firewall & VPN
Firewalls should be used at all ingress/egress points of a cluster. Restrict access for LoadBalancer service using spec.LoadBalancerSourceRanges - this field takes a list of IP CIDR ranges to configure firewall exceptions and is supported on the main cloud service providers.

# Kubelet security
Some typical CIS benchmarks:
* allow-privileged: false (or true with PodSecurityPolicies set)
* anonymous-auth: false
* authorisation-mode: avoid AlwaysAllow (should use RBAC)
* client ca file: set to use valid certs
* --read-only-port: specified in config
* --streaming-connnection-idle-timeout: to avoid DoS attacks
* --protect-kernal-defaults: set to true

**Note some settings are in the kubelet config (etc/kubernetes/kubelet.conf)/(var/lib/kubulet/config.yaml) and some set for the cluster (API server)**

# ETCD
typical CIS benchmarks:
* etcd-certfile and etcd-keyfile: set 
* --enable-admission-plugins: set to a ServiceAccount
* --tls-certfile: set
Most clusters run more than one etcd server for high availability, etcd also should be run on a seperate node from the master/worker nodes.

**Config file can be found /etc/kubernetes/manifests/etcd.yaml
