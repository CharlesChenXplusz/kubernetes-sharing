# Kubernetes

## What is kuberntes
Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications.

## Kubernetes Architecture

### Master
Kubernetes cluster consists of at least one master and multiple compute nodes. The master is responsible for exposing the application program interface (API), scheduling the deployments and managing  the overall cluster. Each node runs a container runtime, such as Docker or rkt, along with an agent that communicates with the master. 

### Node
Each node runs a container runtime, such as Docker or rkt, along with an agent that communicates with the master. The node also runs additional components for logging, monitoring, service discovery and optional add-ons. Nodes are the workhorses of a Kubernetes cluster. They expose compute, networking and storage resources to applications. Nodes can be virtual machines (VMs) running in a cloud or bare metal servers running within the data center.
![Kubernetes Architecture](images/0.png)

## Kubernetes Objects

### Understanding Kubernetes Objects
Kubernetes Objects are persistent entities in the Kubernetes system. Kubernetes uses these entities to represent the state of your cluster. Specifically, they can describe:
* What containerized applications are running (and on which nodes)
* The resources available to those applications
* The policies around how those applications behave, such as restart policies, upgrades, and fault-tolerance

### Describing a Kubernetes Object
When you create an object in Kubernetes, you must provide the object spec that describes its desired state, as well as some basic information about the object (such as a name). When you use the Kubernetes API to create the object (either directly or via kubectl), that API request must include that information as JSON in the request body. **Most often, you provide the information to kubectl in a .yaml file.** kubectl converts the information to JSON when making the API request.

Here’s an example .yaml file that shows the required fields and object spec for a Kubernetes Deployment:

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

One way to create a Deployment using a .yaml file like the one above is to use the kubectl create command in the kubectl command-line interface, passing the .yaml file as an argument. Here’s an example:

```
$ kubectl create -f docs/user-guide/nginx-deployment.yaml --record
```

### Required Fields
In the .yaml file for the Kubernetes object you want to create, you’ll need to set values for the following fields:
* apiVersion - Which version of the Kubernetes API you’re using to create this object
* kind - What kind of object you want to create
* metadata - Data that helps uniquely identify the object, including a name string, UID, and optional namespace

You’ll also need to provide the object spec field. The precise format of the object spec is different for every Kubernetes object, and contains nested fields specific to that object. The Kubernetes API reference can help you find the spec format for all of the objects you can create using Kubernetes
