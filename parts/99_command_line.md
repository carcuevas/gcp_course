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


## gcloud

### Basic stuff

#### Project based operations
##### Show in which project id we are:

```
gcloud config list
```

