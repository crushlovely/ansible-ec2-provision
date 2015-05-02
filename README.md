# Ansible Role For EC2 Provisioning

[![Current Version](http://img.shields.io/github/release/crushlovely/ansible-ec2-provision.svg?style=flat)](https://crushlovely/ansible-ec2-provision/releases)

Provions ec2 instances. This role provisions instances inside of a EC2 VPC it has not been tested to provision instances inside of an EC2 classic network.

## Installation

``` bash
$ ansible-galaxy install crushlovely.ec2_provision,v1.0.0
```

## Variables

You will want to fill all these in before running the role.

``` yaml
aws:
  ec2_access_key: "Amazon IAM access key"
  ec2_secret_key: "Aamazon secret key"
  keypair: "Amazon security key pair"
  image: "Image to be provisioned"
  acct_vpc_id: "EC2 vpc id"
  region: "us-east-1"
  group: "{{ app_name }}-{{ server_env }}"
  instance_type: "m3.medium"
  quantity: "1"
  vpc_subnet: "EC2 VPC regional subnet"
app_name: test
server_env: qa
```
You can also add a vars folder to your project folder and have your variables served by adding them to a file and calling it in your playbook.

```yaml
- hosts: localhost
...
  vars_files:
    - vars/default_vars.yml
...
```


## Usage

Once this role is installed on your system, include it in the roles list of your playbook.

``` yaml
- hosts: localhost
  connection: local
  gather_facts: True
  roles:
    - { role: crushlovely.ec2_provision, zone: "", vpc_subnet: "" }
```

## Dependencies

Although, this role is not dependant on ec2_group it is highly recommended that the ec2_group role is also added to your playbook to ensure ec2 tags match. Boto is required to use this role.

## License

MIT