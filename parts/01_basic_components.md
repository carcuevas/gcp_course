# Google Compute Engine (GCE)

* This service is not by default activated in a new project one can activate it in console or with `gcloud services enable compute.googleapis.com` or in the APIS section of the console

Google Compute engine is passing many things via MEtadata, this metadata we can check with `curl -H "Metadata-Flavor: Google" metadata.google.internal/computeMetadata/v1/` in among the information is passing ssh key and so.

* Once we create a VM, we cannot change its name, nor the *Zone*
* We can add *additional disks* but it is better not to use with autoscalling since it's not behaving very well
* We can select even to run a container inside the machine directly.
* When we connect to a created VM using the SSH from the Web Console, it will create some temporary SSH keys which will expired after a few minutes so we can connect to the created VM.

## VM types

When selecting VM types, we have to take into consideration that the *High memory* machines have the maximum amount of memory available for a giving number of CPU Cores, and the *High Cpu* type would be the opposite, so the maximum amount of Cores for a giving amount of Memory.


We can customize as we want the amount CPU and Memory we want (of course inside the limits of the machine types), we can select the type of CPU even to add a GPU and so... 



## Settings 

We can select a *default region* and *default zone* 

## Metadata

Here we can for example configure the *SSH Keys* which will be used for a *Project*

## Identity and API access

We can allow from the VM if we want to have access to some or all  of the `Cloud APIs` in the Project directly from a new VM, so from the server we can access those services we want to.

## VM Options

### Disks
* We can select here if we want to delete the boot disk when the instance is deleted
* **Encryption**: It normally better to let Google Manage the encryption keys, also we can use specific *Customer-managed key* which is inside the Cloud Key Management Service, or even to use a *Customer-supplied key* outside of Google, latest one is not recommended though

### Management

#### Automation

* **Startup scripts**: This will run, when starting the machine for first time **and** on a **reboot**
* **Metadata**: We can set variables, basically if in a *Startup script* we have written `variable1` and we set the value in *Metadata* `variable1` to `test1` it will substitue in the script `variable1` to `test1` before executing it. Inside a script we can substitute it like this:

```
#!/bin/bash
# variable1 will be substituted by test1
VARIABLE=$(curl http://metadata.google.internal/computeMetadata/v1/instance/attributes/variable1 -H "Metadata-Flavor: Google")
```



#### Availability Policy

* **Preemptibility**: if selected as *ON* Google just assures that it will run for a maximum of a 24h (or even before in case something happens), but after that it's something happens with the Rack, server or something this machine will be stopped and not migrated; that it is why it's cheaper.

* **Automatic Restart**: When Preemptibility is *OFF* Google will try to have the machine running, so if there is some problem with the Server/Rack Google will automatically restart the instance in another Server/Rack so the machine will be active.

* **On host maintenance**: When Preemptibility is *OFF* and Google needs to do some maintenance in the infrastructure where the VM is, it will automatically migrate the machine to other infrastructure **without downtime** 


### Security

Here we can override the project common settings for SSH Keys, we can block them and use a custom ones for some instance. We can use this when we do not want to allow to specific people on a project to have access to a certain machine for example.






# Google Cloud Storage

## Buckets
* Name should be unique across the Cloud Storage
* Object versioning control cannot be modified from the Console, but just with the command *gsutil*

* We need to take into consideration that to list the buckets inside of a project (Called *Class A Operations*) it's charged by 10.000 operations, if for example we want to list the object of a bucket (called *Class B Operations*) it is also charged by 10.000 operations and depending of the Storage Class 

### Storage Location for Buckets
We can have:
* **Multi-regional**: High availability - 99.95% of Availability SLA 
* **Dual-Region**: (Low latency but with High availability in 2 regions, more expensive one - 99.95%  of Availability SLA 
* **Regional**: Lowest latency but just in one region 99.90% of Availability SLA 


### Storage Class for Buckets
* **Standard**: The most expensive, but for frequently used data
* **Nearline**: For backups, when retrieving data once a month, cheaper. So the minimum time of archiving without paying penalty is 30 days.
* **Coldline**: Best for disaster recovery, or for retrieving data once a trimester. A bit cheaper than Nearline by GB stored. But the minimum time of archiving without paying penalty is 90 days.
* **Archive**: Long time digital preservation, accessed less than once a year. The cheapest one by GB, but take care with the *Class A* and *Class B* operations are quite expensive. The minimum time of archiving without paying penalty is 365 days

### Access control to bucket objects
* **Fine-grained**: One can specify what ACL to apply to the objects inside the Bucket, this was the one before... 
* **Uniform**: uniform access to all objects in the bucket by using only bucket-level permissions, so we cannot make one object private for example if we want the rest of object public...

When upload files, by default are PRIVATE, if we want to get a public object called *object1* in the bucket *test_bucket* we could retrieve it by going to:

**https://storage.googleapis.com/test_bucket/object1**
