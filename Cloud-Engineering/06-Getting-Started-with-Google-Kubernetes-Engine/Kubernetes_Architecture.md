<h1>Kubernetes Architecture</h1>
<h2>Introduction</h2>

* Kubernetes concepts
* Kubernetes components
* Google Kubernetes Engine concepts
* Kubernetes object management
* Lab practicing deploying a sample Pod in GKE

<h2>Kubernetes Concepts</h2>

<h3>Kubernetes Object Model</h3>

Each item Kubernetes manages is represented by an object, you can view and change the objects attributes and state. Kubernetes workloads are spread evenly across available nodes by default.

**Kubernetes object** is defined as a persistent entity that represents the state of something running in a cluster, its desired state and its current state. various kinds of objects represent containerized applications, the resources available to them and the policies that affect their behavior.
* **Object spec** desired state described by you
* **Object status** current state described by Kubernetes
* **Kubernetes control pane** various system processes that collaborate to make a cluster work

**Principle of Declarative Management** Kubernetes needs to be told how objects should be managed then it will work to achieve and maintain that desired state through a **watch loop**

<h4>Pod</h4>

* Foundational building block of the standard Kubernetes model, smallest deployable Kubernetes object
* Pods create the environment where containers live, if there is multiple containers they are tightly coupled and share resources (networking, storage)
* Kubernetes assigns each Pod a unique IP address and every container within a Pod shares the network namespace, including IP and network ports. Containers in the same Pod can communicate through local host 127.0.0.1
* Pods can specify a set of storage volumes that can be shared among its containers

<h2>Kubernetes Components</h2>

<h3>Cluster</h3>

* Needs computers, usually VMs
* One is the control plane and others are nodes. Nodes run Pods, Control Plane coordinates the entire cluster.

<h3>Control Plane</h3>

*  `kube-APIserver` 
  * Accepts commands that view or change the state of the cluster
  * Launches Pods
* `kubectl` 
  * Connects to the kube-APIserver
  * Communicates with it using Kubernetes API
  * Authenticates incoming requests, determines if they are authorized and valid
  * Manage admission control
* `etcd` the clusters database
  * Reliably stores the state of the cluster
    * All the cluster configuration data
    * What nodes are part of the cluster
    * What Pods should be running
    * Where they should be running
  * You never directly interact with etcd
* `kube-scheduler`
  * Schedule Pods into the nodes
  * Evaluates the requirements of each individual Pod and selects which node is most suitable
  * Doesn't actually launch pods on nodes, Chooses a node and writes the name of that node into the Pod object
  * Knows the state of all the node
  * Obeys constraints you define
  * Can define affinity and anti-affinity parameters, which specify which groups do or do not run on the same node
* `kube-controller-manager` Continuously monitors the state of a cluster through the kube-APIserver
  * If the desired state does not match the current state, it will attempt to make changes to achieve the desired state
  * Many Kubernetes objects are maintained by loops of code called **controllers**
  * Use certain controllers to manage workloads
  * Other types of controllers have system level responsibilities
* `kube-cloud-manager`
  * Manages controllers that interact with underlying cloud providers

<h3>Node</h3>

* `Kublet` a small family of control plane components, Kubernetes agent on each node. Kublet uses the container runtime to start the Pod and monitors its lifecycle, readiness, liveness probes and reports back to the kube-APIserver
* **Container runtime** software used to launch a container from a container image. GKE uses containerd from Docker
* `kube-proxy` maintains network connectivity among Pods in a cluster

<h3>GKE Modes</h3>

GKE differs from Kubernetes as its responsible for provisioning and managing all the control plane infrastructure behind it. It also eliminates the need for a separate control plane.
* Autopilot mode - recommended, GKE manages the underlying infrastructure such as node configuration, autoscaling, auto-upgrades, baseline security configurations and baseline networking configuration
* Standard mode - user managed infrastructure including configuring individual nodes

<h2>GKE Autopilot and GKE Standard</h2>

<h3>Autopilot</h3>

* Optimizes the management of Kubernetes with a hands off experience
* Less management overhead
* Less configuration options
* Only pay for what you use
* All Pods in GKe Autopilot are scheduled with a Guaranteed class Quality of Service through a minor configuration change
* Optimized for production
  * Create clusters according to best practice
  * Defines machine type based on workloads, optimizing usage and cost and adapts for changing workloads
  * Deploy production-ready GKE clusters faster
* Strong security cluster
  * Secures cluster nodes and infrastructure
  * Eliminates infrastructure security tasks
  * Reduces the clusters attack surface, by locking down nodes
  * Reduces ongoing configuration mistakes
* Promotes operational efficiency
  * Monitors the entire Autopilot cluster
  * Ensures Pods are always scheduled
  * Keeps clusters up to date
  * Configures update windows for clusters
  * User only pays for Pods, not nodes

Autopilot restrictions
* Configuration options are more restrictive
* Autopilot clusters have restrictions on access to node objects
* No SSH
* No privilege escalation
* Limitations on node affinity and host access

<h3>Standard</h3>

* Kubernetes management infrastructure to be configured in many different ways
* More management overhead
* Fine grained control
* Pay for all the provisioned infrastructure, regardless of how much gets used
* Same functionality as Autopilot but you are responsible for the configuration, management adn optimization of the cluster

<h2>Object Management</h2>

* All Kubernetes objects are identified by a unique name and unique identifier
* Define objects that Kubernetes creates and maintains with **manifest files** written with YAML or JSON

<h3>Manifest Files</h3>

* `apiVersion` the Kubernetes API version used to create the object
* `kind` states the object you want
* `metadata` identifies the object name, unique ID and optional namespace
* Best practice: if several objects are related, define them all in the same YAML file, making it easier to manage
* Best practice: Use Cloud Source Repositories to save YAML files in version control repositories so it's easier to track and manage changes and undo the changes when necessary. Helpful when recreating or restoring a cluster

<h3>Details of an Object</h3>

* **Name** all objects are identified by a name. The name must consist of a unique string under 253 characters using numbers, letters, hyphens and periods and not be the same as another object
* **UID** unique identifier generated by Kubernetes
* **Labels** key value pairs to tag objects to help identify and organize objects. Resources can be selected by label through the kubectl command

**Object controller** manages the state of the Pods. As Pods are designed to be ephemeral and disposable, they don't heal or repair themselves and are not meant to run forever. Controllers create a child object **ReplicaSet controller** to launch Pods. ReplicaSet controller recognizes the difference between current states and desired states.
Example controllers
* Deployments - ideal for web servers, long lived software components
* Statefulsets
* DaemonSets
* Jobs

<h2>Deploying GKE Autopilot Clusters</h2>
<h3>Intro</h3>

* Use the Google Cloud console to build GKE clusters
* Deploy a Pod
* Examine the cluster and Pods
