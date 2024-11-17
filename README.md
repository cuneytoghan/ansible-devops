# Ansible-devops

## Description
This project is about configuring ansible for DevOps.

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)
- [Contributing](#contributing)

## Features
- Automates tasks with Ansible
- Installs required software

## Installation
1. Install Role Dependencies
```bash
mkdir roles && ansible-galaxy install -r required_roles.yaml -p roles/
```

## Usage
1. Setup Python venv

```bash
cd ansible-devops; \
python3 -m venv venv; \
source venv/bin/activate; \
pip install -r requirements.txt
```
To exit 
```bash
deactivate
```
