<h1>Introduction to Containers and Kubernetes</h1>
<h2>Introduction</h2>

Containerization helps development teams move fast, deploy software efficiently and operate at an unprecedented scale.
* Containers
* Container images
* Kubernetes
* Google Kubernetes Engine
* Lab with Cloud Build

<h2>Containers</h2>

<h3>History of Deploying an Application</h3>
<h4>Local Computers</h4>

Previously deploying an application required physical space, power, cooling, network connectivity, operating system, software dependencies, the application. When you needed more processing power, redundancy, security or scalability, you would add more computers. It was common for computers to have a single purpose. This process wasted resources and took a long time to deploy, maintain and scale.

<h4>Virtualization</h4>

The process of creating a virtual version of a physical resource such as a server, storage device or network. This made it possible to run multiple virtual servers and operating systems on one local computer. Virtualization takes less time to deploy new solutions, fewer resources are wasted and portability is improved as VMs can be imaged and easily moved.

However an application and all its dependencies and operating system are still bundled. Not easy to move VM from one hypervisor product to another, takes time for operating systems to boot up, applications that share dependencies are not isolated from each other. Can be solved through
* Software engineering policies
  * Need to be updated occasionally
* Integration tests
  * Can cause novel failure modes that are hard to troubleshoot
  * Slows down development
* Run a dedicated VM for each application
* Implement abstraction at the level of the application and its dependencies

**Hypervisor** the software layer that breaks the dependencies of an operating system on the underlying hardware and allows several virtual machines to share that hardware. Eg Kernel based Virtual Machine KVM. 

<h4>Containers</h4>

* Isolated user spaces for running application code
* Lightweight because they don't carry a full operating system
* Can be scheduled or integrated tightly with the underlying system
* Can be created and shut down quickly
* Do not boot an entire VM of initialize an operating system for each application
* Application is packaged with all the dependencies it needs adn the engine that executes the container is responsible for making them available at runtime

Why containers are appealing to developers?
* They're a code-centric way to deliver high performing, scalable applications
* They provide access to reliable underlying hardware and software
* Code will run successfully regardless if its on a local machine or in production as its a Linux kernel base
* Incremental changes can be made to a container based on a production image, it can be deployed quickly with a single file copy, speeding up development
* They make it easier to build up applications that use the microservice design pattern. Loosely coupled, fine grained components allowing the operating system to scale and upgrade components of an application without affecting the application as a whole

<h2>Container Images</h2>

* **Image** an application and its dependencies. A container simply runs an instance of an image

<h3>Docker</h3>

* Open source technology
* Can be used to create and run applications in containers
* No way to orchestrate applications at scale

<h3>Isolate Workloads with Containers</h3>

**Linux process** has its own virtual memory address space, separate from all others and Linux processes can be rapidly created adn destroyed

**Linux namespaces** to control what an application can see, such as process ID numbers, directory trees, IP addresses etc. NOTE not the same as kubernetes namespaces

**Linux cgroups** control what a application can use, such as its maximum consumption of CPU time, memory, I/O bandwidth and other resources

**Union file systems** bundle everything needed into a package. Requires combining applications and their dependencies into a set of clean, minimal layers

<h3>Container Images</h3>

* Structured in layers, the tool used to build the image reads instructions from the container manifest
* Dockerfile instructions specify layers inside the container image. Each layer is read-only but when a container runs from this image, it will also have a writable ephemeral topmost layer

<h4>Dockerfile</h4>

* Contains 4 commands that create a layer
  * `FROM` creates a base layer from a public repository
  * `COPY` adds a new layer, which contains some files copied in from your build tools current directory
  * `RUN` command builds the application by using the make command and puts the result in the third layer
  * `CMD` specifies what command to run within the container
* Layers should start with those least likely to change at the top
* Not a best practice to build your application in the same container where you ship and run it
* Application packaging relies on multi-stage build process. One container builds the final executable image and a separate container receives only what is needed to run the application
* The container runtime adds a new writable layer on top of the underlying layers called **container layer**
* All changes made to the running container are written to this thin writable container layer
* Container images are ephemeral, so multiple containers can share access to the same underlying image while still maintaining their own data state
* When updating a container only the differences need to be copied

<h3>Creating Containers</h3>

* Use publicly available open-source container image as the base for your own images or unmodified use
* Use the Google maintained Artifact Registry at `pkg.dev`, which contains public, open source images. Also provides Google customers a place to store their own container images adn is integrated with IAM
* Use container images available in other public repositories like Docker Hub, Registry and GitLab

<h3>Cloud Build</h3>

* A managed service for building containers
* Integrated with IAM
* Designed to retrieve the source code builds from different code repositories
  * Cloud Source Repositories
  * GitHub
  * Bitbucket
* Configure, build steps to
  * Fetch dependencies
  * Compile source code
  * Run integration test
* Use tools like Docker, Gradle, Maven

<h2>Working with the Cloud Build</h2>
<h3>Intro</h3>

* Use provided code to build a Docker container image and a Dockerfile
* Upload the container to the Google Cloud Artifact Registry

<h2>Kubernetes</h2>

* Open source platform for managing containerized workloads and services
* Makes it easy to orchestrate many containers on many hosts, scale them as microservices, and deploy rollouts and rollbacks
* Is a set of APIs to deploy containers on a set of nodes called a **cluster**
* Divided into a set of primary components that run as the control plane and a set of nodes that run containers. **Nodes** represents a computing instance
* You can describe a set of applications and how they should interact with each other and Kubernetes figures how to make that happen
* Supports declarative configurations
  * Describe the desired state you want to achieve instead of the commands to get there
  * Saves work as the system's desired state is always documented, reducing errors
* Allows imperative configuration
  * Issue commands to change the system's state
  * Experienced users use imperative configuration only for quick temporary fixes and as a tool when building a declarative configuration

<h3>Kubernetes Features</h3>

* Supports stateless apps eg Nginx or Apache web servers
* Supports stateful apps, where user and session data can be stored persistently
* Supports batch jobs and daemon tasks
* Autoscale containerized apps based on resource utilization
* Allows resource request levels and resource limits to improve overall workload performance within a cluster
* Is extensible through an ecosystem of plugins and addons
* Is open source and portable so can be deployed anywhere and move freely without vendor lock in

<h2>Google Kubernetes Engine</h2>

* A managed Kubernetes service hosted on Google's Infrastructure
* Helps deploy, manage and scale Kubernetes environments for containerized applications
* Fully managed so underlying resources do not need to be provisioned and container optimized operating system is used to run workloads
* Operating systems are optimized to scale quickly with minimal resource footprint
* GKE Autopilot manages cluster configuration, designed to manage your cluster configuration like nodes, scaling, security and other preconfigured settings
* Auto upgrade ensures clusters have the latest stable version of Kubernetes
* Auto repair repairs unhealthy nodes **Nodes** the virtual machines that host containers in a GKE cluster. Performs periodic health checks on each node of the cluster and nodes determined to be unhealthy are drained and recreated
* Scales the cluster itself
* Cloud Build integration, uses private container images securely stored in Artifact Registry to automate deployment
* Identity and Access Management integration, helps control access by using accounts and role permissions
* Cloud Observability integration, how an application is performing
* Virtual Private Clouds integration, providing a network infrastructure including load balancers and ingress access for your cluster
* Google Cloud Console provides insights into GKE clusters and their resources, to view, inspect and delete resources in the clusters



