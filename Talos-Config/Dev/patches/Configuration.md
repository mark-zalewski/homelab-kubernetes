# Kubernetes Development Cluster Config

**Goal is for production to match initially**

## Nodes
- 1 Control Node
- 1 Workder Node

## Networking
- Celium with Kube-proxy
Goal is for Celium to handle all pod routing and kube-proxy to handle service routing.  More in line with Kubernetes default and easier to setup.  

## Storage
- Longhorn will be setup to handle shared storage for all nodes.

Going forward all new workloads will be created, setup, tested and validated in the development cluster.  Once everything checks out it will then be promoted to the production cluster.  The goal is to make sure production remains as unimpacted as possible as learning new technologies and setting up new services and applications.  