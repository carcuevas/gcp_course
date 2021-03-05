## gsutil

It is used to connect to google cloud storage

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

And we can set the labels of a bucket with:

```
gsutil label set /tmp/labels.json gs://carlinhos_bucket2
```


* as a response we get in JSON with the list of labels


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



## gcloud

### Basic stuff

#### Project based operations
##### Show in which project id we are:

```
gcloud config list
```

