# FCCM-public
FCCM build repository
 OFSAA / IFRS

Weblogic on IFRS Network solution for IFRS Application
=======================================================

This solution provides a Network Architecture deployment to prepare for IFRS application to be deployed.


## Quickstart Deployment

1. Clone this repository to your local host. The `examples` directory contains the Terraform configurations for a sample topology based on the architecture described earlier.

2. Install Terraform. See https://learn.hashicorp.com/terraform/getting-started/install.html.

3. Open `examples/full-deployment/terraform.tfvars` in a plain-text editor, and enter the values of the variables in that file.

4. Set the deployment variables.  The full deployment examples requires variables to be set for the node_pool_ssh_public_key & kube_config_file location. These can be set using environment variables, or added to the `terraform.tfvars` files. e.g.

	```
	$ export TF_VAR_bastion_ssh_public_key_file="~/.ssh/ida_rsa.pub"
	$ export TF_VAR_bastion_ssh_private_key_file="~/.ssh/ida_rsa"
	$ export TF_VAR_remote_ssh_public_key_file="~/.ssh/ida_rsa.pub"
	$ export TF_VAR_remote_ssh_private_key_file="~/.ssh/ida_rsa"
	```

5. Deploy the topology:

-   **Deploy Using Terraform**

	1. Copy the `examples/full-deployment/terraform.tfvars` into each Terraform configuration sub directory.
	2. Go to the `full-deployment/common/compartments` directory.
	3. Run the following commands:
    	```
    	terraform init
    	terraform plan
    	terraform apply
    	```
	4. Repeat runing the `terraform init`, `terraform plan`, and `terraform apply` commands in the following directories, in the given order:
		- `examples/full-deployment/common/compartments`
    	- `examples/full-deployment/common/secrets`
    	- `examples/full-deployment/ifrs_identity/groups`
    	- `examples/full-deployment/ifrs_identity/policies`
    	- `examples/full-deployment/infrastructure/network`
    	- `examples/full-deployment/infrastructure/access`
    	- `examples/full-deployment/ifrs_loadbalancers/private_lbs`
    	- `examples/full-deployment/ifrs_storage/block`
    	- `examples/full-deployment/ifrs_storage/fss`
    	- `examples/full-deployment/ifrs_storage/object`
    	- `examples/full-deployment/ifrs_servers/compute_instances`
    	- `examples/full-deployment/ifrs_database/dbaas` 

-	**Deploy Using Marketplace**
	0. This portion is done manually thru OCI Console Marketplace which has a prebuilt Terraform stack.
	1. Navigate to Marketplace and select the stack of Weblogic Enterprise edition.
	2. Enter all the required values and hit submit button. 
	3. Monitor the output of weblogic stack for successful completion

## Troubleshooting

### Cleaning up after a failed or partial deployment

If this occurs you will need to manually run `terraform destroy` in each terraform configuration directory in the reverse order of the folders listed in the **Deploy Using Terraform** section above.

### End
