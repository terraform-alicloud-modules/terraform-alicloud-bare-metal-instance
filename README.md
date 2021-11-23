Terraform module for creating Bare Metal instance on Alibaba Cloud.  
terraform-alicloud-bare-metal-instance
-------------

English | [简体中文](https://github.com/terraform-alicloud-modules/terraform-alicloud-ecs-bare-metal-instance/blob/master/README-CN.md)

Terraform module to create Bare Metal instance on Alibaba cloud.

These types of resources are supported:

* [ECS Instance](https://www.terraform.io/docs/providers/alicloud/r/instance.html)

## Usage

There are two types of Bare Metal instance: CPU and GPU. You can create the `cpu` or `gpu` Bare Metal instance by `bare_metal_type`.

```hcl
module "bare_metal_ecs_instance" {
  source = "terraform-alicloud-modules/ecs-bare-metal-instance/alicloud"

  name                        = "TF-bare-metal"
  instance_type_family        = "ecs.ebmgn6v"
  bare_metal_type   = "gpu"
  vswitch_id                  = "vsw-fhuqiexxxxxxxxxxxx"
  security_group_ids          = ["sg-12345678"]
  associate_public_ip_address = true
  internet_max_bandwidth_out  = 10
  instance_charge_type        = "PrePaid"
}
```

## Examples

* [complete](https://github.com/terraform-alicloud-modules/terraform-alicloud-ecs-bare-metal-instance/tree/master/examples/complete)

## Notes
From the version v1.1.0, the module has removed the following `provider` setting:

```hcl
provider "alicloud" {
  profile                 = var.profile != "" ? var.profile : null
  shared_credentials_file = var.shared_credentials_file != "" ? var.shared_credentials_file : null
  region                  = var.region != "" ? var.region : null
  skip_region_validation  = var.skip_region_validation
  configuration_source    = "terraform-alicloud-modules/ecs-bare-metal-instance"
}
```

If you still want to use the `provider` setting to apply this module, you can specify a supported version, like 1.0.0:

```hcl
module "bare_metal_ecs_instance" {
  source               = "terraform-alicloud-modules/ecs-bare-metal-instance/alicloud"
  version              = "1.0.0"
  region               = "cn-beijing"
  profile              = "Your-Profile-Name"
  name                 = "TF-bare-metal"
  instance_type_family = "ecs.ebmgn6v"
  // ...
}
```

If you want to upgrade the module to 1.1.0 or higher in-place, you can define a provider which same region with
previous region:

```hcl
provider "alicloud" {
  region  = "cn-beijing"
  profile = "Your-Profile-Name"
}
module "bare_metal_ecs_instance" {
  source               = "terraform-alicloud-modules/ecs-bare-metal-instance/alicloud"
  name                 = "TF-bare-metal"
  instance_type_family = "ecs.ebmgn6v"
  // ...
}
```
or specify an alias provider with a defined region to the module using `providers`:

```hcl
provider "alicloud" {
  region  = "cn-beijing"
  profile = "Your-Profile-Name"
  alias   = "bj"
}
module "bare_metal_ecs_instance" {
  source               = "terraform-alicloud-modules/ecs-bare-metal-instance/alicloud"
  providers            = {
    alicloud = alicloud.bj
  }
  name                 = "TF-bare-metal"
  instance_type_family = "ecs.ebmgn6v"
  // ...
}
```

and then run `terraform init` and `terraform apply` to make the defined provider effect to the existing module state.

More details see [How to use provider in the module](https://www.terraform.io/docs/language/modules/develop/providers.html#passing-providers-explicitly)

## Terraform versions

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.12.0 |
| <a name="requirement_alicloud"></a> [alicloud](#requirement\_alicloud) | >= 1.56.0 |

Submit Issues
-------------
If you have any problems when using this module, please opening a [provider issue](https://github.com/terraform-providers/terraform-provider-alicloud/issues/new) and let us know.

**Note:** There does not recommend to open an issue on this repo.

Authors
-------
Created and maintained by Alibaba Cloud Terraform Team(terraform@alibabacloud.com)

License
----
Apache 2 Licensed. See LICENSE for full details.

Reference
---------
* [Terraform-Provider-Alicloud Github](https://github.com/terraform-providers/terraform-provider-alicloud)
* [Terraform-Provider-Alicloud Release](https://releases.hashicorp.com/terraform-provider-alicloud/)
* [Terraform-Provider-Alicloud Docs](https://www.terraform.io/docs/providers/alicloud/index.html)
