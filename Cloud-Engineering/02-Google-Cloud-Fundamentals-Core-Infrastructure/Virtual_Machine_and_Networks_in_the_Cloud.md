<h1>Virtual Machines and Networks in the Cloud</h1>

<h2>Virtual Private Cloud networking</h2>

VPC is a secure, individual private cloud computing model hosted within a public cloud. 
* VPC networks connect Google Cloud resources to each other and to the internet, segmenting networks, using firewall rules to restrict access to instances, creating static routes to forward traffic to specific destinations
* Google VPC networks are global and can have subnets in any Google Cloud region worldwide.
* Subnets can span the zones in a region, resources can be in different zones on the same subnet

<h2>Compute Engine</h2>

* Create and run virtual machines on Google infrastructure
* No upfront investments
* Thousands of virtual CPUs can run on a system that's designed to be fast and offer consistent performance
* Each VM has the power and functionality as a full fledged operating system
* Can be configured much like a physical server

VMs

* Created with Google Cloud console, Google Cloud CLI or Compute Engine API
* Can run Linux or Windows server images provide by Google or run images of other operating systems and flexibly reconfigure VMs
* Can choose the machine properties of instances
* Are billed per second with a one minute minimum. 
* **Sustained use discounts** apply automatically to VMs the longer they run(25% per month)
* **Committed use discounts** are for stable predictable workloads, VMs can be purchased for up to 57% discount with usage terms of 1 or 3 years
* **Preemptible and Spot VMs** up to 90% discount. When using these ensue that you job can be stopped and restarted. *Spot VMs* have more features, no maximum runtime. *Preemptible VMs* Less features, runtime up to 24 hrs

**Cloud Marketplace** offers solutions from Google and third party vendors. Solutions provide settings so you don't have to manually configure software, virtual machine instances, storage or network settings but can be modified if required. Some solutions require usage fees.

<h2>Scaling virtual machines</h2>

* Choose machine properties by set predefined machine types or creating your own custom machine types
* Large virtual machines available for CPU intensive analytics etc

**Autoscaling** VMs are added or subtracted based on load metrics.
**Maximum number of CPUs per VM** are tied to machine family and constrained by user quota which is zone dependent.

<h2>Important VPC compatibilities</h2>

**Routing Tables**
* Built in
* No router provisioning or managing
* Forward traffic fom one instance to another
* No external IP address required

**Firewalls**
* No router provisioning or managing
* Restrict access to instances
* Rules can be defined through network tags

**VPC Peering** A relationship between two VPCs can be established.

**Share VPC** Alternative to VPC peering using IAM to control and configure.

<h2>Cloud Load Balancing</h2>

**Cloud Load Balancing** distributes user traffic across multiple instances of an application to reduce the risk that applications experience performance issues.

* Fully distributed, software defined managed service
* Can be put in front of all traffic: HTTP(S), TCP, SSL, UDP
* Cross- region load balancing, including automatic multi-region failover
* No "pre-warming" required for anticipated traffic

**Application Load Balancers** at the application layer handling HTTP and HTTPS traffic (level 7). 
* Operate as reverse proxies, distributing incoming traffic across multiple backend instances based on rules you define. 
* Highly flexible, configure for both external an internal 
* Ideal for web applications an services that require advance features like content-based routing andd SSL/TLS termination

**Network Load Balancers** at the transport layer handling TCP, UDP and IP protocols (layer 4).
* **Proxy Network Load Balancers** function as reverse proxies, terminating client connections and establishing new ones to backend services. Traffic management capabilities and support backend
* **Passthrough Network Load Balancers** directly forward traffic to backend while preserving the original source IP address. Ideal for direct server return or need to handle a wide range of IP protocols

<h2>Cloud DNS and Cloud CDN</h2>

*Note:* 8.8.8.8 free Google service providing a public domain name service

**Cloud DNS**
* Manage DNS service that runs on the same infrastructure as Google
* Low latency, high availability, cost effective
* DNS information you publish is served from redundant locations around the world
* Is programmable with console, CLI, or API. Publish and manage millions of DNS zones and records

**Edge Caches** the use of caching servers to store content closer to end users.

**Cloud CDN**(Content Delivery Network)
* Lowers network latency
* Origins of content will experience reduced load
* Save money
* Enabled with a single checkbox(after Application Load Balancer)

<h2>Connecting networks to Google VPC</h2>

**Cloud VPN**
* Cloud Router to make connection dynamic
* Border Gateway Protocol used to exchange information between other networks and Google VPC over VPN
* Not always the best option due to security concern of bandwidth limitations

**Direct Peering**
* A router in the same public datacenter as a Google point of presence (PoP)
* Use a router to exchange traffic between networks
* More than 100 PoPs worldwide

**Carrier Peering**
* Direct access from an on premises network through a service provider's network
* Not covered by a Google Service Level Agreement

**Dedicated Interconnect**
* One or more direct, private connections to Google
* Can be covered by up to a 99.99% SLA
* Connections backed up by a VPN

**Partner Interconnect**
* Connectivity between on premises network and a VPC network though a supported service provider
* Useful if the physical location can't reach a Dedicated Interconnect colocation facility
* Useful if the data needs don't warrant 10 GB per second connection
* Can be configured to support mission critical services or applications that can tolerate some downtime
* Can be covered by up to a 99.99% SLA

**Cross-Cloud Interconnect**
* High bandwidth dedicated connectivity between Google CLou and another cloud service provider
* Supports the adoption of an integrated multi cloud strategy, reduced complexity, site to ite data transfer an encryption
* Connection sizes: 10 Gbps or 100 Gbps