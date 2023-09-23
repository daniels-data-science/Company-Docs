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

### Terraform State

Terraform supports either `local` or `remote` state files. Local state will be saved as a file locally, whereas remote statefiles are automatically stored and updated in a remote file repository. For Food Remedy API, remote state is preferred because:

1. State is autoamtically backed up to the cloud in durable storage.
2. It eliminates the need for the state file to be shared amongst developers (it is bad practice to push the state file to github as it will contain sensitive information).

The catch is that the storage bucket which contains the state file must be manually created and cannot truly be managaed by Terraform (chicken-and-egg problem).

Here is an example configuration to use remote state.

```terraform
backend "gcs" {
    bucket = "foodremedy-api-tfstate"
    prefix = "foodremedy/gcp"
  }
```

Take note of the `prefix` value. This must be unique for any terraform project which is using the `foodremedy-api-tfstate` bucket, otherwise the state file will be overriden. 


### Terraform: `Init`, `Plan` and `apply`

For this you must have Terraform installed for your system. You will also need the `gcloud` CLI installed and authenticated to the Food Remedy API project

To begin working with Terraform for Food Remedy, checkout the `Gopher-Industries/foodremedy-api` github repo. It is recommended to use **Visual Studio Code** with the **Hashicorp Terraform** extension: https://marketplace.visualstudio.com/items?itemName=HashiCorp.terraform

Navigate to `terraform/gcp` via the command line, and run `terraform init`, which will install dependencies for the GCP provider.

If you have made changes to the Terraform configuration, you can run `terraform plan` to see what effect they will have. 

When you are ready for the changes to be deployed to GCP, run `terraform apply`.

Next, navigate to the `terraform/kubernetes` directory and repeat the steps above for running `init`, `plan` and `apply` when there are changes to be made. The configuration in `terraform/gcp` must be deployde first, as the GKE cluster resources must be deployed before the kubernetes configurations can be deployed.

## Work in Progress

- [ ] Setup permissions to run full deployments for Food Remedy API project. Must work with Deakin IT to get this done. Trial and Error process, however the Terraform configuration should give an indication of what permissions are required.
- [ ] Automate Terraform deployments with Github Actions. Start with `terraform validate` and `terraform plan` checks for PR validation. Then, automate `terraform apply` for the `main` branch on merge.
- [ ] Domain name and DNS. We need to register a domain name for the Food Remedy API. This will be used for the frontend and backend. We will also need to setup DNS records for the domain name to point to the frontend and backend services. What name?
- [ ] Automate docker deployments to Google Artifact repos. Backend, database and frontend images should be built and pushed to GCP, to be picekd up and executed by Kubernetes. Three Artifact repos, one for each image.
- [ ] Run `Docker build` for PR validation for backend, frontend and database images.
- [ ] Setup budget alerts for Food Remedy API project. This will prevent us from being charged for resources we don't need.
- [ ] Security: GCP Artifact Repo for Docker - enable image scanning features and find ways to report issues to developers.
- [ ] Security: Execute vulnerability scans and penetration tests on the Food Remedy API.