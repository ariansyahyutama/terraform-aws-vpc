# terraform-aws-vpc

[![Terraform Version](https://img.shields.io/badge/Terraform%20Version->=0.13.0,_<0.14.0-blue.svg)](https://releases.hashicorp.com/terraform/)
[![Release](https://img.shields.io/github/release/traveloka/terraform-aws-vpc.svg)](https://github.com/traveloka/terraform-aws-vpc/releases)
[![Last Commit](https://img.shields.io/github/last-commit/traveloka/terraform-aws-vpc.svg)](https://github.com/traveloka/terraform-aws-vpc/commits/master)
[![Issues](https://img.shields.io/github/issues/traveloka/terraform-aws-vpc.svg)](https://github.com/traveloka/terraform-aws-vpc/issues)
[![Pull Requests](https://img.shields.io/github/issues-pr/traveloka/terraform-aws-vpc.svg)](https://github.com/traveloka/terraform-aws-vpc/pulls)
[![License](https://img.shields.io/github/license/traveloka/terraform-aws-vpc.svg)](https://github.com/traveloka/terraform-aws-vpc/blob/master/LICENSE)
![Open Source Love](https://badges.frapsoft.com/os/v1/open-source.png?v=103)

## Table of Content

- [Prerequisites](#Prerequisites)
- [Quick Start](#Quick-Start)
- [Dependencies](#Dependencies)
- [Contributing](#Contributing)
- [Contributor](#Contributor)
- [License](#License)
- [Acknowledgments](#Acknowledgments)

## Prerequisites

- [Terraform](https://releases.hashicorp.com/terraform/). This module currently tested on `0.13.7`

## Quick Start
Terraform module to create all mandatory VPC components.

This module supports either single-tier (only public subnet) or multi-tier (public-app-data subnets) VPC creation.
This module supports only up to 4 AZs.

### Multi-Tier VPC

```hcl
module "abc_dev" {
  source  = "traveloka/vpc/aws"
  version = "v0.8.0"
  
  product_domain = "abc"
  environment    = "dev"

  vpc_name       = "abc-dev"
  vpc_cidr_block = "172.16.0.0/16"

  flowlogs_s3_logging_bucket_name = "S3-bucket-name"
}
```

We use multi-tier architecture for our VPC design. This design divides the infrastructure into three layers: 
- Public tier: entrypoint for public-facing client. Using public subnet since resources in this tier will be discoverable through Internet. Examples: external load balancer, bastion, etc.
- Application Tier: this is where the business logic services life and communicate each others. This tier using private subnet, hence it's only accessible through private network.
- Database Tier: this is where databases life. Application and databases are seperated to have clear boundaries and secure access through application tier.

Benefits or having multi-tier architecture are:
- Scalable
- Gives us high availability and redundancy
- Fit with microservices architecture
- Clear boundaries between public-facing, business logic, and data storage
- Secure and reduce risk, because by default any services life at private subnet, and database only accessible through the application tier.

### Single-Tier VPC

In some cases, you will need a VPC which has only public subnets.

```hcl
module "abc_dev" {
  source  = "traveloka/vpc/aws"
  version = "v0.8.0"

  # you only need to add this line
  vpc_multi_tier = false 

  # ... omitted
}
```

In some situations (it is not always happening), you will get some errors from Terraform when you set `vpc_multi_tier = false`.
It happens because several resources were not created but stated as the outputs.
Currrently Terraform does not allow `count` inside `output` block, so now it is inevitable.
But don't worry, the errors have nothing to do with the stacks/resources/infrastructures that you created.
Just re-execute `terraform apply` and you will be fine.

### Examples

* [Multi-Tier VPC](https://github.com/traveloka/terraform-aws-vpc/tree/master/examples/multi-tier)

### Module


<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.12.0 |
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.13 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | ~> 3.74 |
| <a name="requirement_random"></a> [random](#requirement\_random) | >= 1.2, < 3.0.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | ~> 3.74 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_flowlogs_to_s3_naming"></a> [flowlogs\_to\_s3\_naming](#module\_flowlogs\_to\_s3\_naming) | git@github.com:traveloka/terraform-aws-resource-naming.git | v0.20.0 |


## License

Apache 2 Licensed. See LICENSE for full details.

## Acknowledgement
