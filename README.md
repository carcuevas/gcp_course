# gcp_course
my notes from the course

## Basics

### GCP Design Principles
* It's **GLOBAL**  
  As example, AWS is highly regional which simplifies the data sovereignity, but GCP is global, so it's easier to handle failures and latency; but it could be more sensitive to multi-region/global failures
* IT's **Secure**
* It's **Huge Scale**
* It's for **Developers**


### Physical infrastructure
* vCPU
* Physical Server
* Rack
* DAta Center Building
* Zone (trying to be as much independent as other zone as possible)
* Region
* Multi-Region (N. America, Europe and Asia)
* Private-Global-networks (not using internet to communicate between them even they have transoceanic cables )
* Points of Presence (POPs) Network edges and CDNs locations
* Global 

### Network Ingress & Egress
Now we can choose from two:

#### Normal Network
Routes via internet to edge location closets to *destination*
It's cheaper

#### Google Network
Routes so traffic enters from internet at edge closest to *source* so as consecuences:
* Single global IP address can load balance worldwide, so whenever somebody access to the ip they go to the nearest server bringing very fast responses
* Sidesteps has many issues with DNS

### Pricing

#### Provisioned
Google make sure you are ready to handle the resource X, it's payed even if not in use at the mmoment

#### Usage
Google handle whatever I use, and charge me for that

The above two, we are not choosing them, they are inherent to the service we use

#### Network traffic
* Free on the way in as usual (ingress)
* Egress payed by GB used (but sometimes if using some Egress to some GCP services are free)

### Security
* Everything is encrypted at rest
* Strong Key and Identity Management
* Network encrypted:  
  *  All control info is encrypted
  *  All WAN traffic is encrypted automatically
  *  And they are starting to ecnrypt even all local traffic within data centers
* there is some technogogy from which you can connect securely without using VPN called *BeyondCorp*

### Organization

#### Projects
* Primary unit of organization in GCP, Projects are similar to what **AWS accounts** are
* Projects own resources
* Resources can be shared with other projects




