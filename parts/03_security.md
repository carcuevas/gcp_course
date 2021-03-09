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

