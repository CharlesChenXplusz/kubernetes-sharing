# Kubernetes

## What is kuberntes
Kubernetes is an open-source system for automating deployment, scaling, and management of containerized applications.

## Kubernetes Architecture

### Master
Kubernetes cluster consists of at least one master and multiple compute nodes. The master is responsible for exposing the application program interface (API), scheduling the deployments and managing  the overall cluster. Each node runs a container runtime, such as Docker or rkt, along with an agent that communicates with the master. 

### Node
A node is a worker machine in Kubernetes, previously known as a minion. A node may be a VM or physical machine, depending on the cluster. Each node has the services necessary to run pods and is managed by the master components. The services on a node include Docker, kubelet and kube-proxy. See The Kubernetes Node section in the architecture design doc for more details.


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

####  Required Fields
In the .yaml file for the Kubernetes object you want to create, you’ll need to set values for the following fields:
* apiVersion - Which version of the Kubernetes API you’re using to create this object
* kind - What kind of object you want to create
* metadata - Data that helps uniquely identify the object, including a name string, UID, and optional namespace

You’ll also need to provide the object spec field. The precise format of the object spec is different for every Kubernetes object, and contains nested fields specific to that object. The Kubernetes API reference can help you find the spec format for all of the objects you can create using Kubernetes

### Pods
#### What is a Pod?
Pods are the smallest deployable units of computing that can be created and managed in Kubernetes.

A pod (as in a pod of whales or pea pod) is a group of one or more containers (such as Docker containers), the shared storage for those containers, and options about how to run the containers.

#### Working with Pods
You’ll rarely create individual Pods directly in Kubernetes–even singleton Pods. This is because Pods are designed as relatively ephemeral, disposable entities.

##### Pods and Controllers
A Controller can create and manage multiple Pods for you, handling replication and rollout and providing self-healing capabilities at cluster scope. For example, if a Node fails, the Controller might automatically replace the Pod by scheduling an identical replacement on a different Node.

Some examples of Controllers that contain one or more pods include:
* Deployment
* StatefulSet
* DaemonSet

### Deployments
#### What is a Deployment?
A Deployment provides declarative updates for Pods and ReplicaSets (the next-generation ReplicationController). You only need to describe the desired state in a Deployment object, and the Deployment controller will change the actual state to the desired state at a controlled rate for you.

#### Creating a Deployment
Here is an example Deployment. It creates 3 nginx Pods.

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
Run the example by downloading the example file and then running this command
```shell
kubectl create -f docs/user-guide/nginx-deployment.yaml --record
```

Run the command bellow to show deployments:
```shell
kubectl get deployment
```

### Services
#### What is a Services?
A Kubernetes Service is an abstraction which defines a logical set of Pods and a policy by which to access them - sometimes called a micro-service. The set of Pods targeted by a Service is (usually) determined by a Label Selector (see below for why you might want a Service without a selector).

#### Defining a service
```yaml
kind: Service
apiVersion: v1
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
```

### Ingress
#### What is Ingress?
An API object that manages external access to the services in a cluster, typically HTTP.

Note:
Before you start using the Ingress resource, there are a few things you should understand. The Ingress is a beta resource, not available in any Kubernetes release prior to 1.1. You need an Ingress controller to satisfy an Ingress, simply creating the resource will have no effect.

#### Define a ingress
```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: test
  annotations:
    ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: foo.bar.com
    http:
      paths:
      - path: /foo
        backend:
          serviceName: s1
          servicePort: 80
      - path: /bar
        backend:
          serviceName: s2
          servicePort: 80
```