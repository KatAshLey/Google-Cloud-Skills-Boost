Google Cloud offerings are broadly compute, storage, big data, machine learning and application services.

<h1>Introducing Google Cloud</h1>
<h2>Cloud Computing Overview</h2>
Cloud computing is a way of using IT with the following traits

1. Computing resources on-demand and self-service
2. Access to the resources online
3. Resources are allocated to users out of a pool
4. Resources are elastic, flexible allocation
5. Only pay for what you use

Historically, the first wave of cloud computing started with colocation. Users were able to financially benefit from renting physical space instead of investing in building data centers. 

The virtualized data centers today, users maintain the infrastructure but it's still a user-controlled and user-configured environment. 

Now we are moving into a container-based architecture. Fully automated, elastic, scalable

<h2>IaaS and PaaS</h2>
<h3>IaaS</h3>
Infrastructure as a Service, include raw compute, storage, network capabilities. 
Pay ahead for resources allocated

<h3>PaaS</h3>
Platform as a Service uses code libraries to provide access to the infrastructure applications need.
Pay for resources actually used

<h3>Serverless</h3>
Allows developers to concentrate on code
No infrastructure management needed
Googles Cloud Run and Cloud un Functions

<h3>SaaS</h3>
Software as a Service, applications are not installed on your computer but run in the cloud. eg Gmail, Docs, Drive


<h2>The Google Cloud Network</h2>

**Locations** 7 major geographical locations: North America, South America, Europe, Africa, Middle East, Asia, Australia. These impact Googles availability, durability and latency(the time packets of information takes to travel fom its source to its destination) 

**Regions** are independent geographical areas and are made up of zones. Use multiple regions to bing information closer to users and defend against region outages such as natural disasters. Some services support placing resources in multi-regions

**Zones** an area whee Google Cloud resources are deployed. Use multiple zones to ensure resource redundancy


<h2>Environmental Impact</h2>

Google data centers were first to obtain ISO14001 certification, environmental performance through improving resource efficiency and reducing waste.

First decade Google became the first major company to be carbon neutral, second decade they were first to achieve 100% renewable energy and by 2030 aim to become carbon free.


<h2>Security</h2>
Google Infrastructure Security
<h3>Hardware Infrastructure</h3>
Hardware design and provenance, custom designed equipment

Secure boot stack, cryptographic signatures

Premises security, physical security

<h3>Service Deployment Layer</h3>
Encryption fo inter-service communication, cryptographic privacy and integrity fo remote procedure call (RPC) data

<h3>User Identity Layer</h3>
User identity, sign in pages and additional information, Universal 2nd factor open standard

<h3>Storage Services Layer</h3>
Encryption at rest

<h3>Internet Communication Layer</h3>
Google Front End (GFE) TLS connections are ended using public-private key pairs and X.509 certificates and best practices

Denial of Service (DoS) protection. Multi-tie, multi-layer

<h3>Operational Security Layer</h3>
Intrusion detection, rules and machine intelligence give operation security teams warnings of possible incidents. Red Team exercises measure and improve effectiveness of detection and response mechanisms

Reducing insider risk, aggressively limits and actively monitors activities of those given administrative access to infrastructure

Employee Universal Second Factor(U2F) security keys

Software Development Practices



<h2>Open Source Ecosystems</h2>
Google publishes key elements of technology using open source licenses to create ecosystems that provide customers with options other than Google


<h2>Pricing and Billing</h2>
Provides pe-second billing for Compute Engine, Kubernetes Engine, Dataproc, App Engine. Can provide discounts for greater use.

**Budgets** can assist with cost limits

**Alerts** are based on metrics you can set, to warn you about costs

**Reports** a visual tool allowing monitoring of expenditure based on projects or service

**Quotas** to prevent over consumption of resources because of errors or malicious attacks
*Rate quota* reset after a specific time, *Allocation quota* govern the number of resources