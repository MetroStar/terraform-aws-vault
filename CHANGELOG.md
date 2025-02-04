## terraform-aws-vault Change Log

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/) and this project adheres to [Semantic Versioning](http://semver.org/).

### 0.0.10

**Commit Delta**: [Change from 0.0.9 release](https://github.com/MetroStar/terraform-aws-vault/compare/0.0.9...0.0.10)

**Released**: 2020.02.26

**Summary**:

* Rework means of creating the pillar directory due to https://github.com/gruntwork-io/terragrunt/issues/829

### 0.0.9

**Commit Delta**: [Change from 0.0.8 release](https://github.com/MetroStar/terraform-aws-vault/compare/0.0.8...0.0.9)

**Released**: 2020.02.24

**Summary**:

* Allow any auth/secrets engine to be enabled but still limit configuration to engines implemented

### 0.0.8

**Commit Delta**: [Change from 0.0.7 release](https://github.com/MetroStar/terraform-aws-vault/compare/0.0.7...0.0.8)

**Released**: 2020.01.03

**Summary**:

* Updated to use `terraform-aws-tardigrade-acm` module for handling certificate validation.

### 0.0.7

**Commit Delta**: [Change from 0.0.6 release](https://github.com/MetroStar/terraform-aws-vault/compare/0.0.6...0.0.7)

**Released**: 2020.01.03

**Summary**:

* Changed `template_vars` to simplifies the inputs.
* Added `extra_config` provisioner for AWS Auth method.
* Added `override_json` variable to allow policy override for certain use cases.

### 0.0.6

**Commit Delta**: [Change from 0.0.5 release](https://github.com/MetroStar/terraform-aws-vault/compare/0.0.5...0.0.6)

**Released**: 2019.11.14

**Summary**:

* Fixed bug [#10](https://github.com/MetroStar/terraform-aws-vault/issues/10) addressing forward slashes are being removed from `path`.
* Changed `changes` output for the the `synced` salt state modules.

### 0.0.5

**Commit Delta**: [Change from 0.0.4 release](https://github.com/MetroStar/terraform-aws-vault/compare/0.0.4...0.0.5)

**Released**: 2019.11.04

**Summary**:

* Added input vars `scale_up_schedule` and `scale_down_schedule` to control AutoScaling Group Scheduled Action option.

### 0.0.4

**Commit Delta**: [Change from 0.0.3 release](https://github.com/MetroStar/terraform-aws-vault/compare/0.0.3...0.0.4)

**Released**: 2019.11.04

**Summary**:

* Fixed unsupported argument error on Dynamnodb resource. `point-in-time-recovery` needs to be defined as a block type.
* Added more instructions to `README.md` on how to use the module and how to compose configs for the pillar.

### 0.0.3

**Commit Delta**: [Change from 0.0.2 release](https://github.com/MetroStar/terraform-aws-vault/compare/0.0.2...0.0.3)

**Released**: 2019.11.01

**Summary**:

* Added `vault_pillar_extra_config` input var. Allowing users to add sensitive information to the pillar by `auto.tfvars`
* Added sample configs for `auth_ldap` and `secret_ad` to the test cases

### 0.0.2

**Commit Delta**: [Change from 0.0.1 release](https://github.com/MetroStar/terraform-aws-vault/compare/0.0.1...0.0.2)

**Released**: 2019.10.31

**Summary**:

* Added `yaml` filter to vault.sync salt state
* Changed sample policies in the `pillar` for the test cases
* Added pillar to the local dev Vagrant setup

### 0.0.1

**Commit Delta**: [Change from 0.0.0 release](https://github.com/MetroStar/terraform-aws-vault/compare/0.0.0...0.0.1)

**Released**: 2019.10.31

**Summary**:

*   Add `point-in-time-recovery` option to dynamodb resource

### 0.0.0

**Commit Delta**: N/A

**Released**: 2019.07.08

**Summary**:

*   Initial release!
