# TLS
TLS certificates should be implemented throughout the cluster. Production environments with exposed endpoints should carry out regular certificate rotation. Certificate expiration can be implemented but isn't always recommended at cluster level. A certificate policy in security context for pods and ReplicaSets is extremely important. https://kubernetes.io/docs/tasks/tls/

# Firewall & VPN
Firewalls should be used at all ingress/egress points of a cluster. Restrict access for LoadBalancer service using spec.LoadBalancerSourceRanges - this field takes a list of IP CIDR ranges to configure firewall exceptions and is supported on the main cloud service providers.

# Kubelet security
