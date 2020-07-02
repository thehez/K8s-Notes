# Overview

#### This is a quick and dirty list of useful k8s commands to be used during security assessments. The list will be organised and neatened up later!!

## Commands

*kubectl cluster-info* - retrieve cluster information including master node and dns

*kubectl config view* - view brief configuration of cluster

*kubectl get* - retrieve resources, can include - deployments, namespaces, nodes, pods, services etc..  
  *--all-namespaces* - flag to retrieve resources accross all namespaces  
  *-o wide / -o yaml* - flag to get more detailed information  
  *--show-labels* - flag to show labels  
  
*kubectl get endpoints* - get endpoints that are created with services

*kubectl get nodes -w* - watch progress

*kubectl describe* - detailed information on resources (similar to -o wide) - deployments, namespaces, pods, services etc..  

*kubectl api-resources -o wide* - retrieve all resources available to cluster  

*kubectl exec -it -- <pod> <namespace>* - run a command on a pod
  *kubectl exec -it -- <pod> /bin/bash* - open a shell on a pod
  
*kubectl get serviceaccount/SA* - list available service accounts

*kubectl port-forward <pod> 8081:80* - forward port (example forwards 80 to 8081 on a pod)

*kubectl logs <pod>* - get the pods logs

*kubectl drain [node_name] --ignore-daemonsets* - evict pods on a node

*kubectl delete node [node_name]*



