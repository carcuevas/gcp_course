

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

#### Global Flags

* *--help, -h* : Display detailed help.
* *--project PROJECT_ID*: select some project
* *--account ACCOUNT*: user account to use for invocation. 
* *--filter*: Sometimes it's not available but when it is, we can cut the information shown (sometimes better than `grep`)
* *--format*: Oput format: *json*, *text*, *csv*, *yaml* and more
* *--quiet, -q*: **Dangerous** With this it wont ask for confirmation in destructive actions, will be using default values


#### Config properties
This values are entered just once and then are used by any command that needs them.

* check this: https://cloud.google.com/sdk/gcloud/reference/  

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

#### Create a VM

```
gcloud compute instances create myvm_name
```

#### Remove a VM

```
gcloud compute instances delete myvm_name
```






## gsutil

It is used to connect to google cloud storage, it's like to use `gcloud storage`

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

