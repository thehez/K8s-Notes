# Kubernetes Authentication Adminission and Admission control Process

Kube API Server
* Authentication - Verify the user or service is valid in the cluster. Verified using password, token or certificate to prove the enitity
* Authorisation - Evaluate the request and permissions to validate if the authenticated request is allowed
* Admission - Use the security context and admission controller options to process the request on behalf of the entity against the resources requested

ETCD - persist the reques

## Authentication
*identity* - Kubernetes doesn't have a notion of a human user, assumption is users are managed outside of kubernetes. Typically production environments will use SSO, SAML, LDAP or kerberos for authentication.
 * x509 certificates - client certificates enabled by passing the "--client-ca-file=<somefile>" option to API server
 * token - "--token-auth-file=<somefile>". 
 * password - "--basic-auth-file=<somefile>". (currently only supported for convieniance)
 * service account tokens 

## Authorisation
Kubernetes supports the following modes:
* NodeAuthorisation - special purpose authoriser that grants permissions to kubelets based on the pods they are scheduled to run on 
* Attribute based access control (ABAC) - authoriser grants permissions based on attributes
* webhook - uses HTTP callbacks for integration with kubernetes external authorisers
* Role based access control (RBAC) - the defacto standard for auth. 

## RBAC 
**concepts**
* entity - a group, user, or service account
* resource - a pod, secret or service an entity may try to access
* role - used to define rules for actions on resources
* role binding - attaches a role to an entity, thus determaining a set of actions for specified resources

**Actions** - actions an entity may take are defined in the role, they are based on CRUD verbs (create, read, update, delete) 
**types of roles**
* cluster-wide - cluster roles and bindings accross the entire cluster
* Namespace-wide - roles and bindings within the context of a namespaces (segragation)

**RBAC Tooling**
* audit2rbac - automatically determaine what permissions are necessary for applications and can generate RBAC role bindings as required.
* rbac-manager - a kubernetes operator that simplifies the management of role bindings and service accounts 

## Admission controllers
Admission controllers are the final step before kubernetes persists a change in etcd. Kubernetes supports over 30 admission controllers but some relevant ones are listed below

* AlwaysPullImages - good for image hygiene, pulling fresh images ensures that any vulnerability patches applied upstream will be present in the image
* DenyEscalatingExec - ensures exec and attach commands are blocked from sensitive containers
* PodSecurityPolicy - pod admission based on security context and available policies
* LimitRange & Resource Quota - used to prevent DoS and spawning unauthorised processes
* NodeRestriction - limits the permissions of each kubelet to only modify pods that are bound to it and its own node object

**Enabling admission controllers**
the kubernetes API server flag *--enable-admission-plugins=<admissioncontroller> takes a comma delimited list of admission control plugins to invoke.
 


