# terraform-aws-credential
Terraform module which creates a random password or ssh key and create a keypair (SSH key only) + parameter store for that credential.

## Usage
```hcl
module "bastion_ssh_key" {
  source = "./modules/terraform-aws-credential"

  type           = "ssh"
  parameter_name = "bastion-ssh-private-key"
  key_name       = "bastion-ssh"
  tags           = var.tags
}

module "bastion" {
  source   = "terraform-aws-modules/ec2-instance/aws"
  version  = "4.0.0"
  ...
  key_name = "bastion-ssh"

################################

module "mysql_password" {
  source = "./modules/terraform-aws-credential"

  type           = "password"
  length         = 10
  parameter_name = "mysql-password"
  tags           = var.tags
}

module "mysql" {
  source   = "terraform-aws-modules/rds/aws"
  version  = "4.3.0"
  ...
  password = module.mysql_password.value
}
```

## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.13.1 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | >= 3.63 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | >= 3.63 |
