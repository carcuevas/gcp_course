## Routing

* This is useful :D https://www.webopedia.com/reference/osi-layers/

* It's not about any particular routing scheme nor setting the stage for routing tables / routes
* We are calling it Routing because this is about Networking in general it is about the **Data Flow** perspective, it is how each peace of data is going from place to place.
* So routing in the sense: *Where data should go next?*

### Unicast vs Anycast
These two are routing schemes which brings how data can go from one place to another.
* **Unicast**: says that there is just one unique device in the World that can handle the data, and it should be sent there.
* **Anycast**: says that there are multiple devices that can handle the data, so better to send it to the closest.


### Routing to Google's Network (Premium Routing Tier)

* Google claims, that the routing of data is done mostly in Google's network that's why they have control and it is faster.
* Total exposure of the data in internet is much smaller
* In the *Standard Routing* they suppose to know where the data have to go before going inside the Google network.  So if we have a web in California, the user has to route the data all the way to California where then get to the webserver. But when using *Premium Routing* when the request goes to the Google Point of Presence, they can decide what location is best to send it, or even if another place may be better. One can have different copies in different places.
* Using Global *anycast IP*


### Routing to the right resource (Load Balancing)

This is important because of: 
* Latency reduction (servers physically close to clients)
  * This is something we can get using Premium Tier Routing and *Cross-Region Load Balancing* with *Global Anycast IP*

* Load Balancing
  * Separate from auto-scaling
  * We get this using *Cloud Load Balancer*, having different types *Internal* or *External* and *Layer 4 Load Balancer* or *Layer 7 Load Balancer*

* System design
  *  Different servers may handle differents parts of the systems
  *  Especially when using microservices
  *  We get this using *HTTP(S) Load Balancer* with *URL MAP* so different *Paths* can go to different places. This is the most powerful one.

https://cloud.google.com/load-balancing/docs/load-balancing-overview



## VPC  Routing Among Resources

* The *VPC* itself is Global 
* The *Subnets* on inside the *VPC* are **not** Golbal but Regional, but all of the *Subnets* can reach all others(without VPN)
* *Routes* inside the *VPC* are also Global, and define the next hop for traffic based on destination IP
  *  Routes are global aind apply by Instance-level *Tags* not by *Subnet* (I think this is different from AWS), we can configure the *Tags* in certain *Resouorces*
  *  No route to the internet Gateway means no such data can flow
 * *Firewall* Rules, are also define at *VPC* level so they are Global, and filter data flow that would otherwise route.
   * All *Firewall* Rules are apply Instance-level *Tags* or Service Account 
   * Default *Firewall* Rules block all inboud traffic and allow all the the oubound data. Of course that we can change

### VPC Creation

#### Subnet Creation Mode
* **Automatic**: it will create one subnet in each region, _using always the same CIDRs_
  * If a new Region or Zone is included a new *Subnet* it will be included automatically

* **Custom**: We will need to create our *Subnets* with their CIDRs.

* When creating a new *VPC* if we use **Automatic** `Subnet  Creation Mode` it will create one subnet in each region, _using always the same CIDRs_


 

#### Firewall Rules

* Also we start a new *VPC* with some 4 default  Firewall rules, which we can modify.
  1. *[my-vpc-name]-allow-all-icmp* (so we can allow ping/traceroute and so)
  2. *[my-vpc-name]-allow-internal* (allowing internal traffic to be accepted inside the *VPC*)
  3. *[my-vpc-name]-allow-rdp* (incoming rdp)
  4. *[my-vpc-name]-allow-ssh* (incomming ssh traffic)
* There are also two another rules which we cannot modify, the last two ones:
  1. *[my-vpc-name]-deny-all-ingress*
  2. *[my-vpc-name]-allow-all-egress*








