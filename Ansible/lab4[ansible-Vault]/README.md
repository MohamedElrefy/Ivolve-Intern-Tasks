# Lab 4: Securing Sensitive Data with Ansible Vault

This lab demonstrates how to automate database setup using Ansible while keeping sensitive information secure with Ansible Vault.

## Prerequisites

- Ansible installed on control node

- Access to managed node(s)

## Objectives

- Install MySQL on the managed node

- Create a database iVolve

- Create a user with full privileges on the iVolve database

- Encrypt sensitive data (e.g., database password) using Ansible Vault

- Validate the database setup

## Steps
### 1. Create an Ansible Vault File

Create a vault file to store sensitive data such as the MySQL user password:
```bash
ansible-vault create vault.yml
```

Inside vault.yml, add:

db_user: ivolve_user
db_password: MySecurePassword


You can edit the vault later with:
```bash
ansible-vault edit vault.yml
```
### 2. Write the Playbook

### 3. Run the Playbook

Execute the playbook using vault password:
```bash
ansible-playbook -i inventory.ini mysql.yml --vault-password-file vault.yml
```
### 4. Verification

Check if MySQL is installed and running on the managed node.

Connect to MySQL using the created user:
```bash
mysql -u ivolve_user -p -e "SHOW DATABASES;"
```
