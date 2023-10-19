# kubernetes
Kubernetes AKA K8S

An open-source system (and de-facto standard) for orquestrating container deployments
- Automatic Deployment (Zero Downtime Deployments);
- Scaling & Load Balancing;
- Management (Rollbacks);
---
Kubernetes works with objects:
- Pods;
- Deployments;
- Services;
- Volume;
- ...

Objects can be created in two ways:
1) The Imperative approach
2) The Declarative approach (file.yaml)

## Prerequisites

- Git installed on your system
- DockerHub - Docker Hub is the world's largest library and community for container images
- Docker is a platform designed to help developers build, share, and run container applications.
- Minikube - Minikube is a tool to create a local kubernetes installation.<br>
    Usually for development, official: https://minikube.sigs.k8s.io/docs/start/
- kubectl - The Kubernetes command-line tool


## Setup
- Minikube
  https://minikube.sigs.k8s.io/docs/start/
- kubectl
  https://kubernetes.io/docs/tasks/tools/

## Source code guidelines 
1) Imperative approach :
   - kub-action-01-starting-setup-imperative-approach

2) Declarative approach source code:
    - kub-action-02-declarative-approach-basics
