<h1>Resource Management</h1>
<h2>Module Overview</h2>

Resources in Google Cloud are billable so managing them means controlling costs. Quotas that limit consumption, can be raised on request, but having them in place provides a checkpoint of a chance to make sure that this is really a resource you intend to consume in greater quantity.

<h2>Resource Manager</h2>

Resource Management allows you to hierarchically manage resources by project, folder and organization.

**Policies** contain a set of roles and members that is set on resources. These resources inherit policies from their parent, therefore resource policies are a union of parent and resource if an IAM all policy is associated. However if an IAM deny policy is associated with a resource then the policy can prevent certain principals from using certain permissions, regardless of the roles they are granted.

Billing is accumulated from bottom up, as resource consumption is measured in quantities like rate of time, number of items or feature use.

* A resource belongs to one and only one project
* Project is associated with one bulling account
* Organization contains all billing accounts

<h3>Organizations</h3>

Organization node is the root node for Google Cloud resources

<h3>Projects</h3>

Project accumulates the consumption of all its resources
* Track resource and quota usage
  * Enable billing
  * Manage permissions and credentials
  * Enable services and APIs
* Projects use three identifying attributes
  * Project Name
  * Project Number
  * Project ID, also known as the Application ID

<h3>Resource hierarchy</h3>

Resources are categorized as the following but are still organized into projects for billing and reporting
* Global - images, snapshots, networks
* Regional - external IP addresses
* Zonal - instances and disks

<h2>Quotas</h2>

All resources are subject to project quotas or limits. These can be increased on the quotas pages in the console ot a support ticket
* How many resources you can create per project
  * 15 VPC networks/project
* How quickly you can make API requests in a project: rate limits
  * 5 admin actions/second (Spanner)
* How many resources you can create per region
  * 24 CPUs region/project

<h3>Why use Quotas?</h3>

* Prevent runaway consumption in case of an error or malicious attack
* Prevent billing spikes or surprises
* Forces sizing consideration and periodic review

<h2>Labels</h2>

Labels are a utility for organizing Google Cloud resources. They are key value pairs that you can attach to your resources (maximum of 64 labels per resource)
* Attached to resources: VM disk, snapshot, image using the console or API
* Examples of use
  * Inventory
  * Filter resources
  * In scripts to help analyze costs, run bulk operations

<h3>Label Uses</h3>

* Team or Cost Center
* Components
* Environment or stage
* Owner or contact: or primary contact for a resource
* State

<h3>Compare to Network Tags</h3>

* Labels are a way to organize resources across Google Cloud
  * Disks, image, snapshots etc
  * User defined strings in key-value format
  * Propagated through billing

* Network tags are applied to instances only
  * User defined strings
  * Tags are primarily used for networking (applied firewall rules)

<h2>Billing</h2>

<h3>Budgets and Email Alerts</h3>

To help with project planning and controlling costs, you can set a budget to track your spending.

**Scope** the budget name, which project it applies to

**Amount** the budget amount of set to previous months spend

**Actions** emails sent to Billing Admins after spending exceeds a percentage of the budget or a specified amount or forecasted to exceed the percentage of the budget amount by the end of the month. Can additionally use pub/sub notifications as part of automating cost management

**Labels** can help optimize Google Cloud spending. Recommended to label all your resources and export your billing data to BigQuery to analyze your spending. **BigQuery** is scalable, fully managed enterprise data warehouse with SQL and fast response times.

<h3>Looker Studio</h3>

Looker Studio turns your data into informative dashboards and reports that are easy to read, share and fully customizable.

<h2>Demo: Billing Administration</h2>

Exporting billing data and common activities that a Billing Administrator performs
* Billing credits
* Multiple billing accounts
* Budgets and alerts - actual or forecasted
* Transactions
* Billing export
* Payment information

<h2>Examining Billing Data with BigQuery</h2>
<h3>Intro</h3>

* Sign in to BigQuery from the Cloud console
* Create a dataset
* Create a table
* Import data from a billing file stored in a bucket
* Run complex queries on a larger dataset

<h3>Review</h3>

* Monitor changes in resource consumption over time. Inputs into capacity planning and help determine how to scale up your application to meet growth or scale down your application for efficiency.

<h2>Module Review</h2>

* Cloud Resource Manager
  * Quotas
  * Labels
  * Billing
* BigQuery analyzing billing data

