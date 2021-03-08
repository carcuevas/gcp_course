## Instance Templates

* They are *Global* so no need to create them in some location
* Instance Templates are immutable, we do not change them, we create new ones in case it's needed. We can copy them and modify them from the web console.
* We can create a VM from a *Instance Template*, and we can modify a bit the configuration in the template if we want.


### Instance Groups

#### Group types

* **Managed Stateless**:  They will have just identical instances, and this one it is special for stateless services like batch-processing and so; it is possible to have: *auto-scalling*, *auto-healing*, *auto-updating*, *load-balancing* and *multi-zone deployment*.
* **Managed Stateful**:  They will have just identical instances, and this one it is special for stateful services like DB machines where there will be disk and metadata preservation, there will be available:: *auto-scalling*, *updating*, *load-balancing* and *multi-zone deployment*.

* **Unmanaged**: When we want to have not identical instances, and we can add or remove instances arbitrarily managed by ourselves. It cannot be *multi-zone*, but supports *load-balancing*.

#### Autohealing

Allows to recreate VM instances when needed, so we can have some *Health Check* to recreate machines in case it's not 
