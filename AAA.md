# Kubernetes Authentication Adminission and Admission control Process

Kube API Server
* Authentication - Verify the user or service is valid in the cluster. Verified using password, token or certificate to prove the enitity
* Authorisation - Evaluate the request and permissions to validate if the authenticated request is allowed
* Admission - Use the security context and admission controller options to process the request on behalf of the entity against the resources requested

ETCD - persist the reques

## Authentication
*identity* 
