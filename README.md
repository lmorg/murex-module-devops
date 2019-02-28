# Murex module: devops

This _murex_ module provides useful aliases, functions and tooling for DevOps

The following modules are included as part of this package:

## global

This sets global variables which are required for the other modules

## terraform

This provides autocompletion for Hashicorp's Terraform plus a few additional
helper functions for working with Terraform:

### `terraform-get`

This downloads and installs a specific version of Terraform.

Example usage:

    terraform_get 11.0
    
### `terraform-switch`

This switches to a different version of Terraform, providing you've already
downloaded it using the `terraform_get` tool above.

Example useage:

    terraform_switch 11.0
    
You do not require manually running a `terraform_switch` after running
`terraform_get`.

### `env-tf`

This function creates some useful shortcuts for common actions in Terraform.
The reasoning behind having these functions only enabled via a `env-tf` is so
that you don't override other tools with common terms.

Rather than list each function, I'll just include the source for `env-tf` since
it is just as readable:

    func env-tf {
        # Sets some lazy shortcut functions for working with Terraform

        func init {
            # Remove existing .terraform directory and run `terraform init`
            rm -rf .terraform
            terraform init
        }

        func plan {
            # Runs a .terraform plan. -c / --clean to remove .terraform directory and plan from a clean init
            try {
                args args {
                    "AllowAdditional": false,
                    "Flags": {
                        "--clean": "bool",
                        "-c": "--clean"
                    }
                }

                if { $args[Flags]->[--clean] } then {
                    init
     
                } else {
                    terraform get
                }
            
                terraform plan
            }
        }

        autocomplete set plan { [{
            "Flags": [ "--clean" ]
        }] }

        alias apply=terraform apply
    }