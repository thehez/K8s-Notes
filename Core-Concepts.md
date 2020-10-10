# Cluster Architecture

https://kubernetes.io/docs/concepts/overview/components/

## Overview

A Kubernetes cluster consists of a number of machines called nodes.

Master nodes maintain the control plane, while worker nodes are assigned the pods to run the application workloads.

## Control Plane

* API Server - Communications hub for all cluster components by exposing the Kube-apiserver. 
* Scheduler - Assigns applications (pods) to worker nodes. Can auto-detect based on resource requirements, hardware constraints etc..
* Controller manager - Maintains cluster, handles node failures etc
* etcd - Primary data store for the cluster

## Node Components
* Kubelet - Runs and manages the containers held on the node and communicated with the kube-api
* Kube-Proxy - load balances traffic between applications
* Container runtime - program that runs containers - docker, containerd etc..


