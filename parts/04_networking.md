## Routing

* This is useful :D https://www.webopedia.com/reference/osi-layers/

* It's not about any particular routing scheme nor setting the stage for routing tables / routes
* We are calling it Routing because this is about Networking in general it is about the **Data Flow** perspective, it is how each peace of data is going from place to place.
* So routing in the sense: *Where data should go next?*


### Routing to Google's Network (Premium Routing Tier)

* Google claims, that the routing of data is done mostly in Google's network that's why they have control and it is faster.
* Total exposure of the data in internet is much smaller
* In the *Standard Routing* they suppose to know where the data have to go before going inside the Google network.  So if we have a web in California, the user has to route the data all the way to California where then get to the webserver. But when using *Premium Routing* when the request goes to the Google Point of Presence, they can decide what location is best to send it, or even if another place may be better. One can have different copies in different places.


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


 









