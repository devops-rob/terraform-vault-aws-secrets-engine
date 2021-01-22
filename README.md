# Terraform Module: AWS Secrets Engine

A Terraform module to enable and configure the AWS secrets engine in HashiCorp Vault.

## AWS requirements
Vault will require an aws account is required with programmatic access. This account should have the ability to create, list, delete AWS accounts. For this example, Vault will also require an IAM group to place provisioned accounts.  The permissions assigned to this group will depend on what actions the provisioned accounts need to perform.

For more information about AWS Groups and permissions, refer to the following resources:

- [AWS Groups best practices](https://aws.amazon.com/iam/features/manage-users/)
- [AWS Permissions best practices](https://aws.amazon.com/iam/features/manage-permissions/)

## Usage example

```hcl
provider "vault" {
  address = "http://localhost:8200"
  token   = var.vault_token
}

variable "vault_token" {}
variable "aws_access_key" {}
variable "aws_secret_key" {}

module "aws_defaults" {
  source = "devops-rob/aws-secrets-engine/vault"
  
  aws_backend_role_name = "test"
  aws_iam_groups        = [
    "test1",
    "test2"
  ]

  aws_access_key = var.aws_access_key
  aws_secret_key = var.aws_secret_key
}

```

## License

Licensed under the Apache License, Version 2.0 (the "License").

You may obtain a copy of the License at [apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0).

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an _"AS IS"_ basis, without WARRANTIES or conditions of any kind, either express or implied.

See the License for the specific language governing permissions and limitations under the License.