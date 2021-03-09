# Security Products in GCP

## Authentication Products

### For identity

#### For humans
*G Suite* or *Cloud Identity*

#### For application and sevices
*Service Accounts*

### For identity hierachy
*Google groups*

### Managing Identities
*Google Cloud Directory Sync* (GCDS) to pull data from LDAP (not push)

## Authorization Products

### For identity hierachy
*Google groups*

### For Resource hierarchy
*Organization*, *Folder* and *Projects*

### For Identity and Access Management
*IAM* so we can manage Perminssions, Roles and Bindings

### Others
*Google Cloud Storage* has some **ACLs**
*Billing Management*


## Accounting Products (accountability)
*Google Cloud Logging* to audit and to store Activity Logs

*Billing Export* to go to *BigQuery* or to file in GCS

*GCS Object Lifecycle Management* so we can get rid of sensitive data which is not needed anymore for example

# IAM

## Breakdown of IAM
* Authorization of GCP

## Resources Hierarchy

### Resource
* It is just something you create it in GCP

### Project
* Container we use for a set of some related resources
* Also it define a trust boundary, by default we can access resources within one *Project* but we cannot access to resources in other *Projects*
* Different projects of course can different resources

### Folder
* Contains any number of *Projects* and/or *Folders* itself

### Organization
* Top level Hierarchy
* Tied to *G Suite* or *Cloud Identity Domain*


## Permissions and Roles

### Permission
* Allows to perform a certain action
* The permissions always follows the pattern `Service.Resource.Verb` as for example `pubsub.topics.publics`
* Usually each of the permissions corrresponds to REST API methods

### Role
* It is a collection of permissions to use or manage GCP resources

#### Primitive Roles
* These are *Project* level and often too broad:
  * **Viewer**: Just read-only, cannot change anything
  * **Editor**: it can view and change things but cannot change  *Access* to *Billing*
  * **Owner**: It is like editor but also controls *Access* and *Billing*

#### Predefined Roles
* Gives granular access to specific GCP resources
* A list here: https://cloud.google.com/iam/docs/understanding-roles#predefined_roles

#### Custom Roles
* It can be *Project* or *Organization* level collection we define of granular permissions
  
## Members and Groups

### Members

* It is some Google-known identity
* Each member is identified by an unique email address

#### Types of members: 

* **User**:
  * It's an specific Google account like *G Suite*, *Cloud Identity*, *Gmail* or some validated email
  * It's for people 

* **Service Account**:
  * It's used for Applications and Services

* **Group**:
  * It's a collection of *Users* and/or *Service Accounts*
  * Managed by *Google Group* 
  * It should be the default for us to be used

* **Domain**:
  * Actually it's the whole domain
  * Managed by *G Suite* or *Google Identity* 
 
* **allAuthenticatedUsers**:
  * When using any Google account or Service account
  * Basically it is saying that the resource is **PUBLIC** every body can open a Google account so **Be careful!!** 
  * Since it's inside Google we can tie actions back to the user

* **allUsers**:  
  * Anyone on the internet 
  * The resource is **PUBLIC** so **Be careful!!** 
  

### Groups

* It is a named collections of Google Accounts and *Service Accounts*
* Every group has an unique email addresss associated with the group
* So membership in a *Group* can grants capabilities to Users and *Service Accounts*
* **It is recommende to use them for everything**
* Can be used for owner when within an *Organization*
* Can nest *Groups* in an *Organization*

## Policies

### Breakdown of Policies

* A *Policy* binds *Members* to *Roles* for some scope of *Resources*
* Basically, it answers *Who can do what to which thing?*
* This is attached to some level in the Resource Hierarchy: *Organization*, *Folder*, *Project* or even a *Resource* inside a *Project*
* There are always *additive* mneaning only using  **ALLOW** it cannot be substractive (it is not possible to use a deny)
  * **Child Policies cannot restrict access granted at a higher level** That's why always good to use *Folders*.
* Only **Only *Policy* per *Resource** it's allowed
