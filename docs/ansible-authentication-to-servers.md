
### SSH Key Setup for Remote Access
Recommanded!
This command copies a public SSH key to a remote server, enabling passwordless login:

```
ssh-copy-id -f "-o IdentityFile ~/path/to/key.pem" user@server_ip
```
- -f: Force overwrite if key exists.
- -o IdentityFile: Specifies the private key file.
Replace user@server_ip with your remote server’s username and IP.
Ensure your private key permissions are restricted (chmod 400 key.pem) to avoid errors.


### Enabling SSH Password Authentication
To enable password-based SSH access and set up passwordless login using ssh-copy-id, follow these steps:

1. Enable Password Authentication
Open the SSH configuration file:
```
sudo vim /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
```
Set PasswordAuthentication to yes:
```
PasswordAuthentication yes
```
Save and exit the file, then restart the SSH service to apply changes:
```
sudo systemctl restart ssh
```
2. Set the Password for the User
Set a password for the user (e.g., ubuntu):
sudo passwd ubuntu
Follow the prompts to set a secure password.
3. Copy SSH Key to Server
Use the ssh-copy-id command to copy your SSH key to the server for passwordless authentication:
```
ssh-copy-id ubuntu@<server-ip>
```
Replace <server-ip> with your server's IP address. After this step, you can SSH into the server without needing a password.