# Ansible role: AWS VPC VGW

This role is able to create any number of Virtual Gateways, each attached to a VPC in AWS.

[![Build Status](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-vgw.svg?branch=master)](https://travis-ci.org/Flaconi/ansible-role-aws-vpc-vgw)
[![Version](https://img.shields.io/github/tag/Flaconi/ansible-role-aws-vpc-vgw.svg)](https://github.com/Flaconi/ansible-role-aws-vpc-vgw/tags)
[![Ansible Galaxy](https://img.shields.io/ansible/role/d/25925.svg)](https://galaxy.ansible.com/Flaconi/aws-vpc-vgw/)

## Requirements

* Ansible 2.5


## Additional variables

Additional variables that can be used (either as `host_vars`/`group_vars` or via command line args):

| Variable                            | Description                  |
|-------------------------------------|------------------------------|
| `aws_vpc_vgw_profile`               | Boto profile name to be used |
| `aws_vpc_vgw_default_region`        | Default region to use        |
| `aws_vpc_vgw_vpc_filter_additional` | Additional `key` `val` filter to add to `vpc_filter` and `vpc_name` by default. |

## Example definition

VGW's can be created per VPC either by supplying a VPC `name` or a VPC `filter`.

#### Required parameter only

```yml
aws_vpc_vgws:
  # Create VGW for a VPC by VPC name
  - name: vgw-test-1
    vpc_name: devops-test-vpc-1
  # Create VGW for a VPC by VPC filter
  - name: vgw-test-2
    vpc_filter:
      - key: "tag:Name"
        val: "devops-test-vpc-2"
      - key: "tag:env"
        val: playground
      - key: "tag:department"
        val: devops
```

#### All available parameter
```yml
aws_vpc_vgws:
  # Create VGW for a VPC by VPC name
  - name: vgw-test-1
    vpc_name: devops-test-vpc-1
    region: eu-central-1
    tags:
      - key: env
        val: playground
      - key: department
        val: devops
  # Create VGW for a VPC by VPC filter
  - name: vgw-test-2
    vpc_filter:
      - key: "tag:Name"
        val: "devops-test-vpc-2"
      - key: "tag:env"
        val: playground
      - key: "tag:department"
        val: devops
    region: eu-central-1
    tags:
      - key: env
        val: playground
      - key: department
        val: devops
```


## Testing

#### Requirements

* Docker
* [yamllint](https://github.com/adrienverge/yamllint)

#### Run tests

```bash
# Lint the source files
make lint

# Run integration tests with default Ansible version
make test

# Run integration tests with custom Ansible version
make test ANSIBLE_VERSION=2.4
```
