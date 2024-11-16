# Using Ansible Vault to Secure Sensitive Data
Ansible Vault allows you to keep sensitive data such as passwords or keys encrypted within your Ansible projects. This guide provides step-by-step instructions on how to create an encrypted vault file and use it in your Ansible playbooks.

- Prerequisites:

Ansible Installed: Ensure you have Ansible installed on your system.
Basic Knowledge of Ansible: Familiarity with Ansible playbooks and inventory files.
Steps
1. Generate a Vault Password File
First, create a secure password file that Ansible Vault will use to encrypt and decrypt your sensitive data.
```
openssl rand -base64 2048 > vault.pass
```
- Security Note: Keep the vault.pass file secure. Do not commit it to version control systems like Git.

2. Create an Encrypted Vault File
```
ansible-vault create group_vars/all/pass.yml --vault-password-file vault.pass
```

ansible-vault create: Command to create a new encrypted file.
group_vars/all/pass.yml: The path where the encrypted file will be stored.

`Note:`Placing the file in group_vars/all/ makes the variables available to all hosts and groups.

--vault-password-file vault.pass: Specifies the password file to use for encryption.
Instructions:

After running the command, Ansible will open your default editor for you to input your sensitive data.

Example Content for pass.yml:
```
aws_access_key_id: YOUR_ACCESS_KEY_ID
aws_secret_access_key: YOUR_SECRET_ACCESS_KEY
```


3. Run Ansible Playbook with the Vault Password File
Execute your Ansible playbook while providing the vault password file to decrypt sensitive variables at runtime.
```
ansible-playbook -i inventory.ini compute/ec2-provision.yaml --vault-password-file vault.pass
```
`Security Considerations`

Protect the Vault Password File: The vault.pass file contains the key to your encrypted data. Ensure it is securely stored and not accessible to unauthorized users.

Do Not Commit: Add vault.pass to your .gitignore file to prevent it from being committed to version control.

Summary
By following these steps, you can securely manage sensitive data in your Ansible projects using Ansible Vault. Encrypting variables ensures that sensitive information is not exposed in your code repositories or logs, enhancing the security of your automation workflows.