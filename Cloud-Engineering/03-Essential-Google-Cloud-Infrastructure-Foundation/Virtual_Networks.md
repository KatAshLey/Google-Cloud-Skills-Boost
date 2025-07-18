<h1>Virtual Networks</h1>
<h2>Module Overview</h2>

* Uses a software defined network built on global fiber infrastructure
* Google Cloud consists of Regions around the world along with Points of Presence(POP)
* **Regions** a specific geographical location you can run your resources. Consists of 3 zones (apart from Iowa with 4)

<h2>Virtual Private Cloud</h2>

A comprehensive set of Google managed networking objects, isolated from other VPCs but can interact with others through networking policies.

* Projects - encompass every single network
* Networks
  * Default, auto mode, custom mode
* Subnetworks - allow you to divide or segregate your environment
* Regions and Zones - placement of worldwide data centers providing continuous data protection and high availability
* IP addresses
  * Internal, external, range
* Virtual machines(VMs)
* Routes
* Firewalls rules

<h2>Projects, Networks and Subnetworks</h2>

<h3>Projects</h3>
A key organizer of infrastructure resources in Google Cloud.

* Associates objects and services with billing
* Contains networks(up to 15, additional can be requested) that can be shared/peered

<h3>Network</h3>

* Has no IP address range, a construct of all the individual IP address and services within that network
* Is global and spans all available regions, simultaneously
* Contains subnetworks
* Is available as default, auto, or custom

<h3>VPS Network Types</h3>
<h4>Default</h4>

* Every projects default
* One subnet per region, with non-overlapping CIDR blocks
* Default firewall rules that allow ingress traffic for ICMP, RDP and SSH from anywhere, ingress traffic from within the default network for all protocols and ports

<h4>Auto</h4>

* Default network
* One subnet per region
* Regional IP allocation
* Fixed /20 subnetwork per region
* Expandable up to /16. All of these subnets fit within the 10.182.0.0/9 CIDR block, meaning as new Regions become available, new subnets in those regions are automatically added to auto mode networks using an IP from that block

<h4>Custom</h4>

* No default subnet created
* Full control of IP ranges
* Regional IP allocation
* Expandable to IP ranges you specify
* Can convert to this from Auto but can not go back

Google Cloud now supports IPv6 in a custom VPC network mode, for example you can configure IPv6 addressing on 'dualstack' VM instances running both IPv4 and IPv6

<h3>Networks Isolate Systems</h3>

Resources sitting in the same network can make use of their internal IP address to communicate even if they span different regions. 

Resources that are in the same region but *different* networks must use their external IPs to communicate through Googles Edge Routers. These options have different billing and security ramifications.

<h3>VPC are Global</h3>

A single VPN can securely connect to on premises networks to your Google Cloud network. With VMs in different regions you can leverage Google's private network to communicate between each other and the on-prem network through a VPN gateway, reducing costs and network management complexity.

<h3>Subnetworks Cross Zones</h3>

Subnetworks work on a regional scale which means they can cross zones. The subnet is an IP range and you can use addresses within the range(apart from reserved addresses for broadcasting)

* VMs can be in the same subnet but in different zones
* A single firewall rule can apply to both VMs

<h3>Expanding Subnets Without Recreating Instances</h3>

* Cannot overlap with other subnets in any region
* IP range must be a unique valid CIDR block
* New subnet IP ranges have to fall within valid IP ranges
* Can expand but not shrink
* Auto mode can be expanded from /20 to /16
* Avoid large subnets

<h2>Demo: Expand a Subnet</h2>

Using the network interface settings you can expand the subnets without having to stop resources with downtime.

<h2>IP address</h2>

Each VM can have two IP addresses assigned.

<h3>Internal IP</h3>

Every VM that starts up and any service that depends on VMs gets an internal IP address.

* Allocated from subnet range to VMs by DHCP
* DCH lease is renewed every 24 hours
* VM name and IP is registered with network scoped DNS

<h3>External IP</h3>

Assigned if device or machine is externally facing.

* Assigned form pool (ephemeral) - by default
* Reserved (static) - if you assign a static external IP address and do not assign a resource or forwarding rule, you are charged at a higher rate
* Bring your own IP address (BYOIP) - must be bigger than /24
* VM doesn't know external IP; it is mapped to the internal IP

<h2>Demo: Internal and external IP</h2>

Instances do not need to have an external IP address. 

VM Instances can take 90 second to shut down

<h2>Mapping IP addresses</h2>

* External IPs are unknown to the OS of the VM. It is mapped to the VMs internal address transparently by VPC

<h3>DNS Resolution for Internal Addresses</h3>

Two types of internal DNS **Zonal** (recommended for higher reliability) and **Global**.

Each instance has a hostname that can be resolved to an internal IP.

* Hostname is the same as the instance name
* Fully Qualified Domain Name is [hostname].[zone].c.[project-id].internal

Name resolution is handled by internal DNS resolver

* Provided as part of Compute Engine
* Configured for use on instance via DHCP
* Provides answer for internal and external addresses

<h3>DNS Resolution for External Addresses</h3>

Instances with external IP can allow connections from hosts outside of the project

* Users connect directly using external IP addresses
* Admins can also publish public DNS records pointing to the instance., Public DNS records are not published automatically.

DNS records for external addresses can be published using existing DNS servers (outside of Google Cloud)

DNS zones can be hosted using Cloud DNS

<h3>Cloud DNS</h3>

* Google's DNS service. Is a scalable, reliable and managed authoritative Domain name System running on the same infrastructure as Google
* Translate domain names into IP addresses
* Low latency, using Googles ANycast name servers
* High availability (100% uptime SLA)
* Create and update millions of DNS records without managing your own servers and software
* UI, command line, API

<h3>Alias IP Ranges</h3>
Assign a range of internal IP addresses as an alias to a VMs network interface. Useful for multiple servers on a VM and want to assign different IP address to each service.

<h2>IP Addresses for Default Domains</h2>

File in folder

<h2>Routes and Firewall Rules</h2>

<h3>Cloud Routes</h3>
A route is a mapping of an IP range to a destination. Every route has:

* Routes that let instances in a network send traffic directly to each other
* A default route that directs packets to destinations that are outside the network.

**Firewall rules must also allow the packet**

* Apply to traffic egressing to a VM
* Forward traffic to most specific route
* Are created when a subnet is created
* Enable VMs on the same network to communicate
* Destination is in CIDR notation
* Traffic is delivered only if it matches a firewall rule

<h3>Instance Routing Tables</h3>

* Routes may apply to one or more instances
* A route applies to an instance id the network and instance tags match
* If the network matches and there are no instance tags specified, the route applies to all instances in that network
* Compute Engine then uses the Routes collection to create individual read-only routing tables for each instance

<h3>Firewall Rules</h3>
Firewall rules protect your VM instances from unapproved connections

* VPC network functions as a distributed firewall
* Firewall rules are applied to the network as a whole
* Connections are allowed or denied at the instance level
* Firewall rules are stateless, meaning they allow bidirectional communication once a session is established
* Implied deny all ingress (inbound) and allow all egress (outbound)

Rules comprise of:

`direction` Inbound connections are matched against ingress rules only. Outbound connections are matched against egress rules only

`source` For the ingress direction, can be specified as part of the rule with IP addresses, source tags or a source service account

`destination` For the egress direction, can be specified as part of the rule with one or more ranges of IP address

`protocol` or `port` Any rule can be restricted to apply specific protocols oly or specific combinations of protocols and ports only

`action` To allow or deny packets that match the direction, protocol, port, and source/destination of the rule

`priority` Governs the order in which rules are evaluated, the first matching rule is applied

`Rule assignment` All rules are assigned to all instances, but you can assign certain rules to certain instances only

<h2>Pricing</h2>

<h3>Network Pricing</h3>

* No charge for:
  * Ingress
  * Egress same zone (internal IP address)
  * Egress to Google products
  * Egress to to different Google Cloud service within same region

* Charges:
  * $0.01 (per GB)
    * Egress between zones in the same region
    * Egress to the same zone (external IP address)
    * Egress between regions within the US and Canada
  * Varies by region
    * Egress between regions, not including traffic between US regions

<h3>External IP Pricing</h3>

* Static IP address (assigned but unused) - High $ eg 0.010
* Static and ephemeral IP addresses in use on standard VM instance - Small $ eg $0.005
* Static and ephemeral IP addresses in use on preemptible and Spot VM instances - Very small $ eg 0.0025
* Static and ephemeral IP addresses used by Cloud NAT - Small $ eg $0.005
* Static and ephemeral IP addresses attached to forwarding rules or used as a public IP for a Cloud VPN tunnel - Free

<h3>Google Cloud Pricing Calculator</h3>
Estimate costs of resources by using the Google Cloud Pricing Calculator. A web based tool, that you specify the expected consumption of certain services and resources and it provides an estimated cost, adjust the currency and time frame to meet your needs before it is saved or emailed to you.

<h2>VPC Networking</h2>
<h3>Intro</h3>

Create an auto mode VPC network with firewall rules and two VM instances. Convert auto mode network to custom mode and create custom mode networks to a diagram. Explore connectivity across networks.

<h3>Review</h3>

* Explored a default network, cannot create VM instances without a VPC network
* Created auto mode VPC with subnets, routes, firewall rules, two VM instances and tested connectivity.
* Auto mode networks are not recommended for production, so converted it to custom
* Created 2 more custom mode VPC networks with firewall rules, VM instances using Console and command line
* Tested connectivity with pings which worked with external IP but not internal. As VPC networks are be default, isolated private networking domains, therefore no internal IP communication is allowed unless you set up peering or VPN connection.

<h2>Common network designs</h2>

<h3>Availability</h3>
Increase availability by placing 2 virtual machines into multiple zones (within the same region) but within the same subnetwork. Using a single subnetwork allows you to create a firewall rule against the subnetwork without additional security complexity. Provides isolation for infrastructure, hardware and software failures.

<h3>Globalization</h3>
Using multiple regions provides a higher degrees of failure independence, creating robust systems, lower latency and lower traffic costs. Use a external Application Load Balancer.

<h3>Cloud NAT</h3>
Google's managed network address translation service that lets you provision your application instances without public IP address (best practice), while also allowing them to access the internet for updates, patching, configuration management, etc. Outbound NAT only.

<h3>Private Google Access</h3>
Private Google Access should be applied to allow VM instances that only have internal IPs to reach external IPs of Google APIs and services. Enabled subnet by subnet.

<h2>Implement Private Google Access and Cloud NAT</h2>
<h3>Intro</h3>

Implement Private Google Access and Cloud NAT for a VM instance that doesn't have an external IP address. Verify the access to public IP address of Google APIs adn services and other connections to the INternet.

<h3>Review</h3>

* Created an instance with no external IP address, accessed it using Cloud IAP
* Enable Private Google Access, configured a NAT gateway, verified vm-internal can access Google APIs and public IPs.
* VM instances without external IPs are isolated from external networks. Using Cloud NAT, these instances can access the internet for upgrades and patches. Cloud NAT provides high availability without user management and intervention.

<h2>Module Review</h2>

* Overview of Google's Virtual Private Cloud
* Objects within VPCs: Projects, networks, IP addresses, routes, firewall rules
* Overview of how network design choices can affect billing
* Common network designs
