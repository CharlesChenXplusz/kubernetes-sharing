#Kubernetes
##What is kuberntes
Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications.

##Kubernetes Architecture
###Master
Kubernetes cluster consists of at least one master and multiple compute nodes. The master is responsible for exposing the application program interface (API), scheduling the deployments and managing  the overall cluster. Each node runs a container runtime, such as Docker or rkt, along with an agent that communicates with the master. 
###Node
Each node runs a container runtime, such as Docker or rkt, along with an agent that communicates with the master. The node also runs additional components for logging, monitoring, service discovery and optional add-ons. Nodes are the workhorses of a Kubernetes cluster. They expose compute, networking and storage resources to applications. Nodes can be virtual machines (VMs) running in a cloud or bare metal servers running within the data center.
![Kubernetes Architecture](images/0.png)
