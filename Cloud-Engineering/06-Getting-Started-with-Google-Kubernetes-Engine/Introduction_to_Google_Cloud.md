<h1>Introduction to Google Cloud</h1>
<h2>Introduction</h2>

* The definition of cloud computing
*The service Google Cloud offers architects and developers to build solutions
* How Google's powerful global network can power Google Cloud services
* How Google Cloud resources are structured and managed
* Tools to ensure that your organization doesn't accidentally face a big Google Cloud bill
* Four ways to interact with Google Cloud to commence work
* Hands-on practice accessing the Cloud console and Cloud Shell

<h2>Cloud Computing and Google Cloud</h2>

Cloud computing is a way of using information technology that has the 5 following traits
* Customers get computing resources that are on demand and self service through a web interface
* Customers get access to those resources over the internet, from anywhere
* The provider of those resources allocates them to users out of that pool, allowing providers to buy in bulk adn pass savings on to customers
* Resources are elastic - which means they're flexible, so customers can be
* Customers pay only for what they use, or reserve as they go

<h2>Google Cloud Compute Offerings</h2>

<h3>Compute Engine</h3>

* IaaS offering, similar to physical data centers
  * Compute
  * Storage
  * Network
* Predefined and customized VMs
* Persistent disks ( network storage, scale up to 257TB, can disk snapshots for backup and mobility) and local SSDs (high input/output operations per second), uses block storage
* Managed instance groups, global load balancers supporting autoscaling
* Per second billing, preemptible VMs
* Provides complete control over infrastructure since operating systems can be customized and it can run applications that rely on a mix of operating systems
* On premises workloads can easily be lifted and shifted to Google Cloud without needing to rewrite
* Its the best option when other computing options don't support your application or requirements

<h3>Google Kubernetes Engine</h3>

* Runs containerized applications
* Code packaged with all its dependencies

<h3>App Engine</h3>

* Fully managed PaaS offering
* Bind code to libraries
* Focused on application logic
* Deploys required infrastructure
* Supports popular languages like Java, Node.js, Python, PHP, C#, .NET, Ruby and Go
* Integrated with Cloud tools - CLoud Monitoring, Cloud Logging, Cloud Profiler and Error Reporting
* Version control and traffic splitting
* Want to focus on writing code
* Want to focus on building applications instead of deploying and managing the environment
* Don't need to build a highly reliable and scalable infrastructure

Common uses
* Websites
* Mobile App
* Gaming backends
* a method to present a RESTful API

<h3>Cloud Run</h3>

* A managed compute platform
* Runs stateless containers through web requests or Pub/Sub events
* Serverless
* Built on Knative an open API and runtime environment built on Kubernetes
* It's fast, automatically scale up and down
* Charges only for the resources used

<h3>Cloud Run Functions</h3>

* Event based asynchronous compute solution
* Executes code in response to events
* Functions as a service offering
* Serverless, uses Node.js, Python, Go, Java, .NET core, Ruby, PHP
* Deploys the computing capacity to run code
* Functions can be used to construct application workflows from individual business logic tasks, 
* Can connect and extend cloud services
* Bills to the nearest 100 milliseconds, only while your code is running. Provides a perpetual free tier so many Cloud Run Functions can be free of charge

Common uses
* It can be part of a microservices application architecture
* It can be used to build simple, serverless mobile or IoT backends or integrate with third party services and APIs
* It can be part of intelligent application such as virtual assistance, video or image analysis and sentiment analysis

<h2>The Google Network</h2>

* Google network carries as much as 40% of the worlds internet traffic every day
* Highest possible throughput
* Lowest possible latency
* 100+ content caching nodes worldwide
* High demand content is cached for quicker access
* 7 geographical locations
 * North America
 * South America
 * Europe
 * Africa
 * Middle East
 * Asia
 * Australia
* App location affects qualities like availability, durability and latency
* Each location is divided into several regions and zones. **Regions** (41) are independent geographical areas, composed of zones. **Zones** (124) is an area where Google Cloud resources are deployed

<h2>Resource Management</h2>

* Resource hierarchy directly related to how policies are managed and applied on Google Cloud

<h3>Resources</h3> 

Are services in Google Cloud, organized by project. Eg containers, virtual machines, tables in BigQuery. Every resource belongs to a project

<h3>Project</h3>

A container for all your Google Cloud resources. A way to organize resources, manage billing and control access. Has a unique identifier
* The basis for enabling and using Google Cloud services like managing APIs, enabling billing, adding, removing collaborators and enabling services
* Projects are separate entities under the organization node
* Projects hold resources, each of which belongs to just one project
* Projects can have different owners and users
* Projects are billed and managed separately
* **Project ID**
  * Globally unique
  * Assigned by Google Cloud but mutable during creation
  * Immutable after creation
* **Project name** 
  * Need not be unique
  * Chosen by you
  * Mutable
* **Project number**
  * Globally unique
  * Assigned by Google Cloud
  * Immutable

<h3>Folders</h3>

Groups projects which can be organized by folders or subfolders, on a per department basis

<h3>Organizations</h3>

Encompasses all the projects, folders and resources

<h3>Policies</h3>

Can be defined at teh project, folder and organization levels, some allow policies can be applied to individual resources. They are inherited downwards

<h3>Identity and Access Management (IAM)</h3>

Administrators can apply policies that define who can do what on which resources
* **Who** /principal can be a Google account, Google group, service account, Cloud identity domain. Has its own identifier usually an email
* **can do what** is defined by a role. An IAM role is a collection of permissions

<h3>Security in the Cloud</h3>

Shared responsibility between you and Google. General guideline for shared responsibility is if you configure or store it, you're responsible for securing it.
* Cloud provider responsible for:
  * Hardware
  * Networks
  * Physical security
* Customer responsible for:
  * Configurations
  * Access policies
  * User data

<h2>Billing</h2>

* Billing is established at the project level. When you define a project you link a billing account to it. it is where you configure billing information and payment options
* A billing account can be linked to zero or more projects. If a project is not linked to a billing account it can only use free services
* Billing accounts are charged automatically and invoiced every month, or at every threshold limit
* Billing subaccounts can be used to separate billing by project
* **Budgets** can be a fixed limit, tied to a metric eg percentage of previous months spend
* **Alerts** be notified when costs approach the budget limit
* **Reports** a visual tool to monitor expenditure based on projects or services
* **Quotas** designed to prevent the over consumption of resources because of an error or malicious attack
  * Rate quota reset after a specific time
  * Allocation quotas govern the number of resources that you can have in your project

<h2>Interacting with Google Cloud</h2>

<h3>Google Cloud Console</h3>

* Deploy, scale, diagnose issues in a simple web based Graphical User Interface (GUI)
* Easily find resources, check their health, have fully management control over them and set budgets
* Provides a search facility to quickly find resources and connect to instances through SSH in the browser
* available at `console.cloud.google.com`

<h3>Google Cloud SDK and Cloud Shell</h3>

**SDK**
* Can download and install the Google Cloud SDK locally to your computer
* Set of tools to manage resources and applications hosted on Google Cloud
  * gcloud tool - provides the main command line interface for products and services
  * gcloud storage - provides access to CLoud storage from the command line
  * bq - a command line tool for BigQuery

**Cloud Shell**
* Provides command line access to cloud resources directly from a browser
* Debian based virtual machine with a persistent 5GB home directory
* Each Cloud Shell VM is ephemeral
* Provides web preview functionality and built in authorization for access to Cloud console projects and resources including GKE resources
* The Google Cloud SDK gcloud command and other utilities are always installed, available, up to date and fully authenticated

<h3>APIs (Application Programming Interfaces)</h3>

* The services that make up Google Cloud offer APIs so that the code you write can control them
* The Google APIs Explorer that shows which APIs are available, and in which versions
* Developers often use APIs to build applications that allocate and manage Google Cloud resources

<h3>Google Cloud App</h3>

* Start, stop and use SSH to connect to Compute Engine instances and see logs form each instance
* Stop and start Cloud SQL instances
* Administer applications deployed on App Engine by viewing errors, rolling back deployments and changing traffic splitting

<h2>Accessing the Cloud Console and Cloud Shell</h2>
<h3>Intro</h2>

* Using Google Cloud console and Cloud shell to create the following
  * Buckets
  * Virtual Machines
  * Service accounts
  * Other commands to become familiar with both
