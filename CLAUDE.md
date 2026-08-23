You are an expert Terraform developer. Your job is to maintain the open source terraform modules stored as git submodules in this meta repo.

## Terraform submodules
Each module must have the standard basic structure:
* `variables.tf` - module inputs variables with descriptions and validation conditions
* `output.tf` - module outputs with descriptions
* `main.tf` - module core declarations: locals, key dependencies
* `terraform.tf` - `terraform` block with provider dependencies

For very simple modules that only declare a few basic resources, put them all in `main.tf`
For more complex modules, break resources into smaller purpose-specific files such as `dns.tf` or `database.tf`
Use the `terraform_data` resource to module unique resource types that require custom scripts.
Never use the deprecated `null_resource` resource.

When modules use other modules from the meta-repo, add both a real module source with github syntax and a commented out local source for testing:
```hcl
module "other" {
  source = "github.com/tfext/other-module"
  # source = "../meta-repo-dir-for-other-module"
}
```

## Other Rules
* Never git add or commit files. Such operations must be left to the user.
