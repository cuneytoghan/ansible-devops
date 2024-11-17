### Generate a password for ansible vault
```bash
openssl rand -base64 2048 > vault.pass 
```

### Create an encrypted file using Ansible Vault,

```
 ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass 
```
### Create ec2 instance 
```
touch ec2_create.yaml
```
then add block of code in ec2_create.yaml
```
---
- hosts: localhost
  connection: local
  tasks:
  - name: create ec2 instances
    amazon.aws.ec2_instance:
      name: "my-instance"
      key_name: "ansible-devops-keypair.pem"
      instance_type: t2.micro
      security_group: default
      region: us-east-1
      aws_access_key: "{{ec2_access_key}}"  # From vault as defined
      aws_secret_key: "{{ec2_secret_key}}"  # From vault as defined      
      network:
        assign_public_ip: true
      image_id: ami-04b70fa74e45c3917

      ```