

## gcloud

It's a command line tool to interact with GCP, in general is more powerful than the console, but less that the Rest API




Also it's very simple to use new functionalities versions (still not well tested ) in the gcloud just with this:

```
gcloud alpha
```
and

```
gcloud beta
```



### Syntax
The syntax is like: `gcloud <global flags> <service/product> <group/area> <command> <flags> <parameters>` 

* check this: https://cloud.google.com/sdk/gcloud/reference/  

#### Global Flags

* *--help, -h* : Display detailed help.
* *--project PROJECT_ID*: select some project
* *--account ACCOUNT*: user account to use for invocation. 
* *--filter*: Sometimes it's not available but when it is, we can cut the information shown (sometimes better than `grep`)
* *--format*: Oput format: *json*, *text*, *csv*, *yaml* and more
* *--quiet, -q*: **Dangerous** With this it wont ask for confirmation in destructive actions, will be using default values


#### Config properties
This values are entered just once and then are used by any command that needs them. They are used very often for the *account*, *project*, *region* and *zone* so to configure this it can be used:

```
gcloud config set <CONFIG_PROPERTY> <VALUE>
```

or to check the value of a property we can do it with:

```
gcloud config get-value <CONFIG_PROPERTY>
```
to unset a property 

```
gcloud config unset <CONFIG_PROPERTY>
```
If we want to configure the common properties in interactive mode just we need to run:

```
gcloud init
```

* If we want to list all the configurations:


```
gcloud config configurations list
```

* Check this https://cloud.google.com/sdk/docs/properties


* Also we can create and switch between configurations if we want .....  For create a new configuration we do:

```
gcloud config configurations create ITS_NAME
```
and to switch to that configuration 

```
gcloud config configurations activate ITS_NAME
```

### Basic stuff

#### Project based operations
##### Show in which project id we are:

```
gcloud config get-value project
```

or also in 
```
gcloud config list
```

### Services stuff

#### List services

* list all services **FOR THE SPECIFIC PROJECT** 
```
gcloud services list --available
```

* list all enabled services **FOR THE SPECIFIC PROJECT** 
```
gcloud services list --enabled
```

#### Enable services

* For example compute service

```
gcloud services enable compute.googleapis.com
```


### Computing Stuff 

#### Listing Compute instances we have in the current project

```
 gcloud compute instances list

```
#### Show different options for machines:

* Show different type of machines of the type f1 and in us-east1

```
gcloud compute machine-types list --filter="NAME:f1 AND ZONE~us-east1"
```


#### Create a VM

```
gcloud compute instances create myvm_name
```

* We can speficy more options so we are not taking by default many options

```
## First we set zone and region
gcloud config set compute/region us-east1
gcloud config set compute/zone us-east1-b
# We create the machine and specify the type
gcloud compute instances create --machine-type=f1-micro myhappyvm

```

#### Remove a VM

```
gcloud compute instances delete myvm_name
```

#### Connect to a VM via SSH
* we won't need our keys in the server

```
gcloud compute ssh VM_NAME
```

### IAM stuff

#### Manage Policy Bindings

* One could add or revoke a binding in a policy using:

``` 
gcloud [GROUP] get-iam-policy
```
get the policy in YAML/JSOIN edit it and then execute 


``` 
gcloud [GROUP] set-iam-policy
```
but this is not that good, and we can use something different which is giving less work and it's less error-prone. **Better to use**:

* For adding a new Binding
```
gcloud [GROUP] add-iam-policy-binding [RESOURCE-NAME] --role [ROLE_TO_GRANT] --member user:[USER-EMAIL]
```

* For removing a Binding
```
gcloud [GROUP] remove-iam-policy-binding [RESOURCE-NAME] --role [ROLE_TO_REVOKE] --member user:[USER-EMAIL]
```




## gsutil

It is used to connect to google cloud storage, it would be like to use `gcloud storage` (which does not exist anymore if ever :D)

### show buckets in the project we are

```
gsutil ls
```
We get something like this:

```
cloudadm1002@cloudshell:~ (data-mind-306710)$ gsutil ls
gs://carlinhos_bucket/
```

### show objects in a bucket

```
cloudadm1002@cloudshell:~ (data-mind-306710)$ gsutil ls gs://carlinhos_bucket/
gs://carlinhos_bucket/image (1).png
gs://carlinhos_bucket/image (2).png
gs://carlinhos_bucket/test_folder/
```

* if we want to show also the *folders* recusirve

```
cloudadm1002@cloudshell:~ (data-mind-306710)$ gsutil ls gs://carlinhos_bucket/**
gs://carlinhos_bucket/image (1).png
gs://carlinhos_bucket/image (2).png
gs://carlinhos_bucket/test_folder/
gs://carlinhos_bucket/test_folder/Admin.png

```
### Playing with labels from/in a bucket

The labels are in JSON format, for example we can get the labels from a bucket with:

```
gsutil label get gs://carlinhos_bucket > /tmp/labels.json
```

* And we can set the labels of a bucket with:

```
gsutil label set /tmp/labels.json gs://carlinhos_bucket2
```
* And we can add for example one more label in a bucket like:

```
gsutil label ch -l "owner:carlinhos" gs://carlinhos_bucket2

```


### Create a bucket

so for specifying all the options we can check the help

```
gsutil mb --help
```

for example we can create one like this:

```
gsutil mb -l us-east1 gs://carlinhos_bucket2
Creating gs://carlinhos_bucket2/...
```


### Playing with versioning in a bucket

* To show the versioning of a bucket

```
gsutil versioning get gs://carlinhos_bucket2

```

* To enable versioning of a bucket:

```
gsutil versioning set on gs://carlinhos_bucket2

```

* To show a file with the versioning data

```
gsutil ls -a gs://carlinhos_bucket2

```



### Operations with files and object bucket

* Copy a file to a bucket
```
gsutil cp file gs://carlinhos_bucket2
```

* Copy all the objects from a bucket to another bucket **NOT CREATING FOLDERS IN DESTINATION!!**

```
gsutil cp file gs://carlinhos_bucket/** gs://carlinhos_bucket2/
```


* Remove a file in a bucket

```
gsutil rm gs://carlinhos_bucket2/file
```

* Remove a file in a bucket

```
gsutil rm gs://carlinhos_bucket2/file
```


## bq

It's command line for BigQuery, like writting `gcloud bigquery`

