<h1>Resources and Access in the Cloud</h1>
<h2>Google Cloud resource hierarchy</h2>

<h3>Level 01 - Resources</h3>

Virtual machines, Cloud Storage buckets, tables in Big Query or anything else in Google Cloud. Can only be allocated to one project

<h3>Level 02 - Projects</h3>

* Resources are organized into projects. 
* Projects are the basis for enabling services. 
* Each project is a separate entity under the organization node
* They hold resources which belong to that project
* Have different owners and users
* Are billed and managed separately

Projects have 3 identifying attributes:
* Project ID - Globally unique, assigned by Google Cloud but mutable during creation, immutable after creation
* Project Name - Need not to be unique, chosen by you, mutable
* Project Number - Globally unique, assigned by Google Cloud, immutable

**Resource Manage Tool** for managing projects
* Lists, creates, updates, deletes projects
* Recover previously deleted project
* Access though RCP API and REST API


<h3>Level 03 - Folders</h3>

Projects are organized into folders and sub folders. Folders give you more control over policies and permissions assigned and delegate administrative rights to allow wok to be done independently


<h3>Level 04 - Organization node</h3>

Encompasses all projects, folders and resources. Has special roles associated with this node. eg organization policy administrator and project creator role. How organization nodes are created depends on if you are a Google Workspace customer or use Cloud Identity.


<h3>Policies</h3>

Can be defined at each level, only some services can have individual policies applied to each resource. They are also inherited downward.


<h2>Identity and Access Management(IAM)</h2>

Administrators apply policies that define who can do what and on what resources.
IAM checks relevant deny policies before allow policies, so user could be denied certain permissions regardless of roles granted


**Principal** the who, has an identifier, can be a Google account, a Google group, service account, Cloud identity domain

**Role** a collection of permissions 
* Basic IAM Role - owner, editor, view billing admin
* Predefined IAM Role - Some services offer sets of predefined oles and define where they can be applied
* Custom IAM Role - to define exact permissions. Only at project or organizational level


<h2>Service accounts</h2>

Service accounts allow you to assign specific permissions to a resource so it can interact with other resources without human intervention. 

* They are named with an email address and use cryptographic keys instead of passwords.
* Have to be managed
* Are a resource so can have its own IAM policies attached

<h2>Cloud Identity</h2>

Organizations can define policies and manage their users and group using the Google Admin Console.

* Log in and manage resources with the same credentials used in existing Active Directory or LDAP systems
* Google Admin Console can e used to disable user accounts and remove them from groups when they leave
* Available in fee and premium editions
* Already available to Google Workspace customers in the Google Admin Console

<h2>Interacting with Google Cloud</h2>

<h3>Google Cloud Console</h3>

* Simple web based graphical user interface
* Easily find resources, check their health, have full management control ove them, and set budgets
* Provides a search facility to quickly find resources and connect to instances via SSH in the browser

<h3>Google Cloud SDK and Cloud Shell</h3>

Set of tools to manage resources and applications hosted on Google Cloud. **Google Cloud CLI** provides the main command line interface fo products and services and bq a command line tool fo BigQuery.

* Provides command line access to cloud resources directly from a browser
* Debian based virtual machine with a persistent 5 GB home directory
* Google Cloud SDK gcloud command and other utilities are always installed, available, up to date and fully authenticated

<h3>APIs</h3>

* Offer APIs that allow code to be written to control them
* Google APIs Explorer shows what APIs are available and in what versions
* Provides Cloud Client and Google API Client libraries
* Languages represented: Java, Python, PHP, C#, Go, Node.j, uby and C++

<h3>Google Cloud App</h3>

* Start, top and ue H to connect into Compute Engines instances and see logs
* Stop and start Cloud SQL instances
Administer applications deployed on App Engine
* Up to date billing information for projects and alerts for those going over budget
* Customize graphs showing key metics
* Alerts and incident management