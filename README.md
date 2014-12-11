# Ansible Role For EC2 Provisioning

Provions ec2 instances. This role provisions instances inside of a EC2 VPC it has not been tested to provision instances inside of an EC2 classic network.

## Installation

``` bash
$ ansible-galaxy install crushlovely.ec2_provision
```

## Variables

You will want to fill all these in before running the role.

``` yaml
ec2_access_key: ""
ec2_secret_key: ""
keypair: ""
image: ""
acct_vpc_id:
region: ""
group:
instance_type:
quantity: 1
vpc_subnet:
app_name:
server_env:
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
    - { role: crushlovely.ec2_provision, zone: "", vpc_subnet: }
```

## Dependencies

Although, this role is not dependant on ec2_group it is highly recommended that the ec2_group role is also added to your playbook to ensure ec2 tags match. Boto is required to use this role.

## License

MIT