EC2 Provision
========

Provions one ec2 instance and adds it to your cache so that the rest of your playbook can call it with app_name_server_env.  This role is 1 of 3 parts.  Although, the roles can be used individually they were developed to use together for the most effective ec2 provisioning.

######This ec2 role was broken off of the ansible example and tailored for organizational purposes.

```
- name: make one instance
  local_action:
    module: ec2
    image: "{{ image }}"
    instance_type: "{{ instance_type }}"
    aws_access_key: "{{ ec2_access_key }}"
    aws_secret_key: "{{ ec2_secret_key }}"
    keypair: "{{ keypair }}"
    instance_tags: "{{ instance_tag }}"
    region: "{{ region }}"
    group: "{{ group }}"
    wait: true
  register: ec2_info

- debug: var=ec2_info
- debug: var=item
  with_items: ec2_info.instance_ids

- add_host: hostname={{ item.public_ip }} groupname={{ app_name }}_{{ server_env }}
  with_items: ec2_info.instances

- name: wait for instances to listen on port:22
  wait_for:
    state: started
    host: "{{ item.public_dns_name }}"
    port: 22
  with_items: ec2_info.instances
```

Requirements
-----------
boto

Role Variables
-----------
image
instance_type
ec2_access_key
ec2_secret_key
keypair
instance_tag
region
group
app_name
server_env

Dependencies
-----------
Note: Not dependencies but developed together.
ec2_group
ec2_ami

License
-----------
MIT