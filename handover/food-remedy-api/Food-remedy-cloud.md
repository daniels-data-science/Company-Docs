# Food Remedy Cloud Handover

Cloud Resources for Food Remedy API are deployed into a Google Cloud Platform (GCP) project. 

This project is called `sit-23t2-food-remedy-7f9b4c0` with resources primarily running in the `australia-southeast2` region.

## GCP Access

Access to the `sit-23t2-food-remedy-7f9b4c0` GCP project is enabled via a Deakin support request. Reach out to the Gopher Industries company director for help.

## Food Remedy API Cloud Development

We are looking to implement an architecture defined in this document: https://deakin365.sharepoint.com/:w:/s/GopherIndustries2/ERbhoMywyK5Bmuz7lgunM3cBT1vyYciZIuLPgytqd2rcNg?e=lSnwSJ

To build our infrastructure we are using the `Terraform` IAC tool in the `foodrememdy-api` repo: https://github.com/Gopher-Industries/foodremedy-api/tree/48febb6c3bd59d00918193a3c33d06c4eea7dcdd/terraform

Terraform is a declarative configuration language which attempts to deploy the resources defined in the code. Importantly, Terraform must maintain a state file which keeps a record of the resources it is managing in GCP. This means that Terraform deployments are idempotent and repeatable. 

For example, you define a storage bucket in code and use Terraform to deploy it. You might think that if you run the deployment a second time, you will end up with 2 storage buckets. However, Terraform will see that it has already deployed that storage bucket and will not make any changes. If the bucket configuration has changed manually and it's state is not in sync with the Terraform state, Terraform will restore the storage bucket's configuration so it matches what is definide in code. Furthermore, if you delete the storage bucket configuration from your code and run a new Terraform deployment, that bucket will also be removed from GCP. 


