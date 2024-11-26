# Project Name

## Description
This project automates the deployment of EC2 instances using Ansible playbooks.

## Table of Contents
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [Authentication](#Authentication)
- [Examples](#examples)


## Features
- Automates EC2 instance creation
- Automate stop/start selected ec2 instances
- Installs required software

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/cuneytoghan/ansible-devops.git


## Usage
1. Generate a password for ansible vault
```bash
openssl rand -base64 2048 > vault.pass 
```

2. Create an encrypted file using Ansible Vault, 

```bash
ansible-vault create <path/to/encryptedfile> --vault-password-file vault.pass 
```

3. Create an encrypted file using Ansible Vault, 

```bash
cd projects/project1
ansible-vault edit <path/to/encryptedfile>  --vault-password-file vault.pass 
```

4. Create ec2 instance 
```bash
touch ec2_create.yaml
```
Then add block of code in ec2_create.yaml
```yaml
---
- name: Create ec2 instance
  hosts: localhost
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

## Authentication
1. Setup passwordless authentication:

- This command will copy your laptop/server's public SSH key to the server's ~/.ssh/authorized_keys file.
```bash
ssh-copy-id -f "-o IdentityFile <PATH/TO/PEMFILE>" ubuntu@< SERVER-IP-ADRESS >
```
- To ssh into server with keypair:
```bash
ssh -o ' IdentityFile PATH/TO/KEYPAIR' 'ubuntu@<IP-address>' 
```

## Examples

1. To run playbooks and create/stop/start/terminate ec2 instances: 
```bash
cd projects/project
```
```bash
ansible-playbook  -i inventory.ini  ec2_create.yaml --vault-pass-file vault.pass   
```
```bash
ansible-playbook  -i inventory.ini  ec2_stop.yaml --vault-pass-file vault.pass  
```
```bash
ansible-playbook  -i inventory.ini  ec2_start.yaml --vault-pass-file vault.pass   
```


```bash
ansible-playbook  -i inventory.ini  ec2_terminate.yaml --vault-pass-file vault.pass   
```



![Build Status](https://img.shields.io/badge/build-passing-brightgreen)

