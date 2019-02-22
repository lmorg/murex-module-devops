# Murex module: devops

This _murex_ module provides useful aliases, functions and tooling for DevOps

The following modules are included as part of this package:

## global

This sets global variables which are required for the other modules

## terraform

This provides autocompletion for Hashicorp's Terraform plus a few additional
helper functions for working with Terraform:

### `terraform_get`

This downloads and installs a specific version of Terraform.

Example usage:

    terraform_get 11.0
    
### `terraform_switch`

This switches to a different version of Terraform, providing you've already
downloaded it using the `terraform_get` tool above.

Example useage:

    terraform_switch 11.0
    
You do not require manually running a `terraform_switch` after running
`terraform_get`.
