# terraform-aws-vpc

## Table of Content

- [Prerequisites](#Prerequisites)
- [Quick Start](#Quick-Start)
- [Dependencies](#Dependencies)
- [License](#License)

## Prerequisites

- [Terraform](https://releases.hashicorp.com/terraform/). This module currently tested on `4.2.0`

## Quick Start

This module multi-tier (public-app-data subnets) VPC creation.
This module is tested for 2 AZs with static cidr_subnet 


### Module


<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >=  v1.1.6 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | ~> 4.2.0 |
| <a name="requirement_random"></a> [random](#requirement\_random) | >= 3.1.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | ~> 4.2.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_flowlogs_to_s3_naming"></a> [flowlogs\_to\_s3\_naming](#module\_flowlogs\_to\_s3\_naming) | git@github.com:traveloka/terraform-aws-resource-naming.git | v0.20.0 |


## License

Apache 2 Licensed. See LICENSE for full details.

## Acknowledgement
