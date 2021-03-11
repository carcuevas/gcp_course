## Setting up Billing in BigQuery

* We should export Billing to *BigQuery* so we can export our daily usage and costs automatically throughtout the day to a BigQuery dataset, and then we can use *BigQuery* to access it. 

One have to go to *Billing* and then to *Billing Export*, then to create a "BigQuery", so the export must be set up per billing account, so for this we can create some kind of `admin-gcp` project in which we can have this managing stuff

* Billing export is not real-time, there will be **hours** of delay (not seconds nor days)


## Setting up a Billing Alert

We can set a budget, so we can try to plan and control cost. One can set a `Budget` either to a billing account or to a project and send alerts if we exceed the set threshold.

To create in the for the whole Billing Account, it is just needed to go to the Budget, and Create budget. We can also use Pub/Sub to send notifications.

## Create user which has the ability of creating Projects and can assign Project to a budget.



Check this for setting up the Admin accounts and so
https://cloud.google.com/resource-manager/docs/organization-setup
https://console.cloud.google.com/getting-started/enterprise?organizationId=646329885933
