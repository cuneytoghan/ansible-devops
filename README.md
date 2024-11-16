# Ansible-devops
This repo is about configuring ansible for DevOps.

### Install Role Dependencies
mkdir roles && ansible-galaxy install -r required_roles.yaml -p roles/

### a. Setup Python venv

```bash
cd ansible-devops; \
python3 -m venv venv; \
source venv/bin/activate; \
pip install -r requirements.txt
```
### then to exit 
```
deactivate
```
