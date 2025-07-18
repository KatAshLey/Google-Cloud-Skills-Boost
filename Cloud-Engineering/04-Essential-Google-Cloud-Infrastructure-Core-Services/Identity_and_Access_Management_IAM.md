<h1>Identity and Access Management (IAM)</h1>

<h2>Module Overview</h2>

IAM is a sophisticated system built on top of email-like address names, job type roles and granular permissions. 

Modules:

* Identity and Access Management(IAM)
* Organization
* Roles
* Members
* Service Accounts
* Organization Restrictions
* IAM Best Practices

<h2>Identity and Access Management</h2>

Who can do what on what resource. *Who* can be a person, group or application. *What* refers to specific privileges or actions. *Resource* is any Google Cloud service.

<h3>IAM Objects and Hierarchy</h3>

* Organization - root node
* Folders - children of Organizations, represent department
* Projects - children of Folders
* Resources - children of Projects
* Roles
* Members

<h2>Organization</h2>

* An Organization node is tha root node for Google Cloud resources
* Organization Roles:
  * Organization Admin: Control over all Cloud resources, useful for auditing
  * Project Creator: Controls Project creation, control over who can create projects

<h3>Creating an Organization</h3>

* Created when a Google Workspace or Cloud Identity account creates a Google Cloud Project
* Super Administrator
  * Assign the Organization Admin role to some users
  * Point of contact for recovery issues
  * Control the lifecycle of the account and organization resource
* Organization Admin
  * Define IAM policies
  * Determine the structure fo the resource hierarchy
  * Delegate responsibility over critical components such as networking, billing and resource hierarchy through IAM roles 

<h3>Folder</h3>

Folders provide additional grouping mechanism and isolation boundaries between projects for 

* Different legal entities
* Departments
* Teams

Folders allow delegation of administration rights and also restrict access to resources.

<h3>Resource Manager Roles</h3>

* Organization
  * Admin: Full control over all resources
  * Viewer: View access to all resources
* Folder
  * Admin: Full control over folders
  * Creator: Browse hierarchy and create folders
  * Viewer: View folders and projects below a resource
* Project
  * Creator: Create new projects (automatic owner) and migrate new projects into organization
  * Delete: Delete projects


<h2>Roles</h2>

<h3>Basic Roles</h3>
The original, broad roles available on the Google Cloud Console. Applied to a Project and affect all resources in that project. Fixed, coarse grained levels of access.

* Owner
  * Full administrator access
  * Add, remove members
  * Delete projects
* Editor
  * Modify and delete access
  * Deploy applications amd modify/configure resources
* Viewer
  * Read only
* Billing Administrator
  * Manage billing
  * Add, remove administrators

<h3>Predefined IAM Roles</h3>
Provides members with granular access to specific resources.

<h3>Compute Engine IAM Roles</h3>

* Compute Admin: Full control of all Compute Engine resources
* Network Admin: Permissions to create, modify, delete resources, except firewall rules and SSL certificates
* Storage Admin: Permissions to create, modify and delete disks, images and snapshots

<h3>Custom IAM Roles</h3>

Define a precise set of permissions using the least privilege model

<h2>Demo: Custom Roles</h2>

Create a custom Instance Operator Role that allows some users to start and stop Compute Engine virtual machines but not reconfigure them.

<h2>Members</h2>

Types of members:
* Google Accounts - represents a person who interacts with Google Cloud. Any email address that is associated with a Google Account can be an identity
* Service Accounts - belongs to your application, used to represent the different logical components
* Google Groups - a names collection of Google Accounts and service accounts. Each group has a unique email address that is associated with the group. A convenient way to apply an access policy to a collection of users
* Google Workspace - a virtual group of all the Google Accounts that have been created in an organizations Google Workspace account. Represents your organizations Internet domain name
* Cloud Identity Domains - manage users and groups using the Google Admin console but do not pay for or receive Google Workspace collaboration products

**Note**: you cannot use IAM to create or manage users or groups. Use Cloud Identity or Google Workspace.

<h3>IAM Policies</h3>

* Policy consists of a list of bindings
* Binding binds a list of members to a role
* A collection of access statements attached to a resource
* Contains a set of roles and role members with resources inheriting policies from their parents
* Use a role recommender to identify and remove excess permissions, improving resource security configurations

<h3>IAM Allow Policies</h3>

* Grant access to resources
* Controls access to the resources itself as well as any descendants of that resource
* Associates, binds, to one or more principals with a single IAM role

<h3>IAM Deny Policies</h3>
Deny rules prevent certain principals from using certain permissions, regardless of the roles they are granted. Deny rules specify

* A set of principals that are denied permissions
* The permission that the principals are denied or unable to use
* Optional: the condition that must be true for the permission to be denied

<h3>IAM Conditions</h3>
Enforce conditional, attribute based access control for resources

* Grant resource access to identities only if  configured conditions are met
* Specified in the role bindings of a resources IAM role

<h3>Organization Policies</h3>

* A configuration of restrictions
* Defined by configuring a constraint with desired restrictions
* Applied to the organization node, folders or projects

<h3>Google Cloud Directory Sync</h3>
Administrators can use to manage resources using the same usernames and passwords they already use from their corporate directory. It synchronizes users and groups from your existing Active Directory with users and groups in the Cloud Identity domain.

<h3>Single Sign-on(SSO)</h3>

Use Cloud Identity to configure SAML SSO. If SAML2 isn't supported , use a third party solution

<h3>Google Cloud Access without Gmail</h3>
You can create a Google account without Gmail, to use Google Cloud with the password but no email

<h2>Service Accounts</h2>

An account that belongs to an application that provides and identity for carrying out service to service interactions in a project without supplying user credentials.

* Programs running within Compute Engine instances can automatically acquire access tokens with credentials
* Tokens are used to access any service API in the project and any other services that granted access to that service account
* Service accounts are convenient when you're not accessing user data
* Are identified by an email address
* Three types of service accounts
  * User created (custom)
  * Built in - Compute Engine and App Engine default service accounts
  * Google APIs service accounts - Runs internal Google processes on your behalf

<h3>Default Compute Engine Service Account</h3>

* Automatically created per project with auto-generated name and email address
* Automatically added as a project Editor
* By default, enabled on all instances created using gcloud or console

<h3>Scope</h3>
Authorization is the process of determining what permissions an authenticated identity has on a set of specified resources. Scopes are used to determine if an authenticated identity is authorized.

* Can be changed after an instance is created
* For user-created service accounts, use IAM roles instead

<h3>Service Account Permissions</h3>

* Default service accounts: basic and predefined roles
* User-created service accounts: predefined roles
* Roles for service accounts can be assigned to groups or users

<h3>Service Account Keys</h3>
<h4>Google Managed Service Accounts</h4>

* All service accounts have Google managed keys
* Google stores both the public and private portion of the key
* Each public key can be used for signing for a maximum of 2 weeks
* Private keys are never directly accessible

<h4>User Managed Service Accounts</h4>

* Google only stores the public portion of a user managed key
* Users are responsible for private key security
* Can create up to 10 user managed service accounts keys per service
* Can be administered via the IAM API, gcloud or console

**Note** Google cannot help if you lose user managed private keys. TO list all keys associated with a service account `gcloud iam service-accounts keys list --iam-account user@email.com`

<h2>Organization Restrictions</h2>

Prevents data exfiltration through phishing or insider attacks. For managed devices in an organization, this feature restricts access only to resources in authorized organizations. Google Cloud administrators and egress proxy administrators collaborate to set up organization restrictions. Can be used to restrict access to employees, read only access or access other vendors.

<h2>IAM Best Practices</h2>

<h3>Leverage and Understand the Resource Hierarchy</h3>

* Use projects to group resources that share the same trust boundary
* Check the policy granted on each resource and make sure you understand the inheritance
* Use principles fo least privilege when granting roles
* Audit policies in Cloud Audit Logs: setiampolicy
* Audit membership of groups used in policies

<h3>Grant Roles to Groups</h3>

* Update group membership instead of changing IAM policies
* Audit membership of groups used in policies
* Control the ownership of the Google group used in IAM policies

<h3>Service Accounts Best Practice</h3>

* Be very careful granting serviceAccountUser role
* When creating a service account, give it a display name that clearly identifies its purpose
* Establish a naming convention for service accounts
* Establish key rotation policies and methods
* Audit with `serviceAccount.keys.list()` method

<h3>Identity Aware Proxy (IAP)</h3>

Enforce access control policies for applications and resources

* Identity based control
* Central authorization layer for applications accessed by HTTPS

IAM policy is applied after authentication.

<h2>Exploring IAM</h2>
<h3>Intro</h3>

Grant and revoke roles to change access. Use IAM to implement control, restrict access to specific features and resources, use Service Account User role.

<h3>Review</h3>



<h2>Module Review</h2>

Identity and Access Management components and best practice. The creation and administration of corporate identities occurs through the Workspace admin or Cloud Identity interface and is commonly handled by a person separate from the Google Cloud administrator.

