<h1>Infrastructure Automation</h1>
<h2>Module Overview</h2>

Calling the Cloud API from code is a powerful way to generate infrastructure, but writing code this way has some challenges. One issue us that the maintainability of the infrastructure depends on the quality of the software. Terraform uses a system of highly structured templates and configuration files to document the infrastructure in an easily readable and understandable format. It conceals the actual Cloud API calls so you don't need to write the code and focus on the definition of the infrastructure.

* Terraform
  * Automating the Infrastructure of Networks Using Terraform
* Google Cloud Marketplace

<h2>Terraform</h2>

* Console use for when you are new to using a service or prefer UI
* Cloud Shell best for when you are comfortable using a specific resource and want to quickly create resources using the command line

<h3>Infrastructure as Code (IaC)</h3>

* Infrastructure as Code allows quick provisioning and removing of infrastructures
* Build an infrastructure when needed
* Destroy the infrastructure when not in use
* Create identical infrastructure for dev, test, prod
* Can be part of a CI/CD pipeline
* Templates are the building blocks for disaster recovery procedures
* Manage resource dependencies and complexity
* Google Cloud supports many IaC tools
* Configurations can be modularized with templates which allow the abstraction of resources into reusable components across deployments

<h3>Terraform is an Infrastructure Automation Tool</h3>

* Provision Google Cloud Resources eg Compute Engine, CLoud Firewall Rules, Cloud VPN, Virtual Private Cloud, Cloud Load Balancing, Cloud Router
* Repeatable deployment process
* Declarative language, define what the configuration should be and the system figures out what steps to take
* Focus on the application, specify the resources needed
* Parallel deployment
* Template driven

<h3>Terraform Language</h3>

* Terraform language is the interface to declare resources
* Resources are infrastructure objects
* The configuration file guides teh management of the resource
* A Terraform configuration is a complete document in the Terraform language that tells Terraform how to manage a given collection of infrastructure.
* Configurations can consist of multiple files and directories
* **Blocks** represent objects and can have zer or more labels. 
  ```
  <BLOCK TYPE> "<BLOCK LABEL>" "<BLOCK LABEL>" {
    # Block body
    <IDENTIFIER> = <EXPRESSION> # Argument
  }
  ```
  * **Body** of the block enables you to declare arguments and nested blocks. 
  * **Arguments** are used to assign a value to a name.
  * **Expression** a value that can be assigned to an identifier

Terraform can be used on multiple public and private clouds
* Considered a first class tool in Google Cloud
* Already installed in Cloud Shell

<h3>Terraform Files and Commands</h3>

* **main.tf** to specify the infrastructure we want to create
* **`terraform init`** to initialize the new terraform configuration. Ensure this is run in the same folder as the main.tf file. This command ensures that the Google provider plugin is downloaded and installed in a subdirectory of the current working directory along with other bookkeeping files
* **`terraform plan`** performs a refresh, unless explicitly disabled, then determines what actions are necessary to achieve the desired state specified in the configuration files. A good way to check the execution plan matches your expectations without making the changes just yet
* **`terraform apply`** creates the infrastructure defined in the main.tf file. Once this command is completed you can access teh infrastructure


<h2>Automating the Infrastructure of Networks Using Terraform</h2>
<h3>Intro</h3>

* Create a configuration for an auto mode network
* Create a configuration for a firewall rule
* Create a module for VM instances
* Create and deploy a configuration
* Verify the deployment of a configuration

<h3>Review</h3>

Created a Terraform configuration with a module to automate the deployment of GCP infrastructure. As your configuration changes, Terraform can create incremental execution plans which allocates you to build your overall configuration step by step. The instance module allowed you to reuse the same resource configuration for multiple resources while providing properties as input values

<h2>Google Cloud Marketplace</h2>

* Deploy production grade solutions
* Single bill for Google Cloud and third party services
* If you already have a license for a third party service you might be able to use a bring your own license solution
* Manage solutions using Terraform
* Notifications when a security update is available
* Direct access to partner support

<h2>Demo: Launch Infrastructure Solutions on Google Cloud Marketplace</h2>

Demo of deploying a LAMP stack to a single Compute Engine instance

**LAMP stack** consists of Linux, Apache HTTP server, MySQL and PHP

* Many different providers to choose from
* Options show costs, what it offers
* Deployment Manager to show what has been deployed, change configuration options

<h2>Module Review</h2>

* Automated the deployment of infrastructure using Terraform
* Infrastructure solutions on Cloud Marketplace
* Terraform is beneficial for those who manage several resources and need to deploy, update and destroy them in a repeatable way

