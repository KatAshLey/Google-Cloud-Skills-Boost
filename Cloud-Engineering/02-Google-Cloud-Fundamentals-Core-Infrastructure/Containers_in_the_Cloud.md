<h1>Containers in the Cloud</h1>
<h2>Introduction to containers</h2>

**IaaS** Infrastructure as a Service allows you to share resources using VMs by virtualizing the hardware suing virtual machines.

Containers give the independent scalability of workloads in PaaS and an abstraction layer of the OS and hardware in IaaS.
* Is an invisible box around your code and its dependencies
* Has limited access to its own partition of the file system and hardware
* Only require a few system calls to create and starts as quickly as a process
* Only needs an OS kernel that supports containers and a container runtime on each host
* Scales like PaaS, but gives nearly the same flexibility as IaaS

When building applications you can use lots of containers, each performing their own function like microservices. If you build them this way and connect them with network connections, you can make them modular, deploy easily and scale independently across a group of hosts. Hosts can scale up and down and start and stop containers as demand for your app changes or as hosts fail.

<h2>Kubernetes</h2>

Can be boot strapped using Google Kubernetes Engine. Is declarative.

* An open-source platform for managing containerized workloads and services
* Easy to orchestrate any containers on many hosts, scale them as microservices, and deploy rollouts and rollbacks
* A set of APIs to deploy containers on a set of nodes called a cluster
* Divided into a set of primary components that run as the control plane and a set of nodes that run containers
* You can describe a set of applications and how they should interact with each other and Kubernetes figures how to make that happen

**Pod** 
* Is the smallest unit in Kubernetes that you can create or deploy
* Is a running process on your cluster as a component of your application or an entire app
* Generally one container per Pod but  if you have multiple containers with a hard dependency you can package them into a single Pod and share networking and storage resources between them
* Provides a unique network IP and set of ports for your containers and configurable options


**Deployment** represents a group of replicas of the same Pod and keeps your Pods running even when the nodes they run on fail. Can represent a component of an application of even an entire app.


**Service**  is an abstraction which defines a logical set of Pods and a policy by which to access them. Service groups is a set of Pods and provides a stable endpoint(or fixed IP) for them.

Kubernetes commands
* `kubectl` to run a Deployment with a container inside a Pod
* `kubectl get pods` list running Pods in Project
* `kubectl expose deployments nginx --port=80 --type=LoadBalancer`creates Service with fixed IP for Pods and external Load Balancer with public IP
* `kubectl get service` lists all services in Project
* `kubectl scale` to scale deployment
* `kubectl get deployments` lists all deployments
* `kubectl describe deployments` describes deployments
* `kubectl apply -f nginx-deployment.yaml` creates a yaml for nginx deployment
* `kubectl rollout` deploys a new updated container can also change config file then `kubectl apply`
* `gcloud container clusters create k1` startup Kubernetes on a cluster in GKE

<h2>Google Kubernetes Engine</h2>

Google hosted managed Kubernetes services. The environment consists of multiple machines (Compute Engine instances) grouped together to form a cluster. Provisions and manages all the control plane infrastructure.

**Autopilot Mode** manages underlying infrastructure including node configuration, autoscaling, auto upgrades, baseline security configurations and baseline networking configurations. (Recommended) 

* Optimized for production
* Strong security posture
* Promotes operational efficiency

**Standard Mode** you manage the underlying infrastructure, including configuring all the individual nodes.

Kubernetes commands and resources are used for 
* Deploy and manage applications
* Perform administration tasks
* Set policies
* Monitor workload health

Advanced cluster management features
* Google CLoud's load balancing for Compute Engine instances
* Node pools to designate subsets of nodes within a cluster
* Automatic scaling of your cluster's node instance count
* Automatic upgrades for our cluster's node software
* Node auto-repair to maintain node health and availability
* Logging and monitoring with Google CLoud Observability