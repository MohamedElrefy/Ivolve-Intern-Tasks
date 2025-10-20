# Lab 3: Structured Configuration Management with Ansible Roles
## Create Inventory File
## Configure Docker&kubectl&jenkins Role
```bash
vim roles/docker/tasks/main.yml
vim roles/kubectl/tasks/main.yml
vim roles/jenkins/tasks/main.yml
```
## Create Main Playbook to Run All Roles

## Run the Playbook
```bash
ansible-playbook -i inventory.ini docker_jenkins_kubectl.yml
```
## Verify Installation on Managed Node
```bash 
ansible -i inventory all -m command -a "docker --version"
ansible -i inventory all -m command -a "kubectl version --client"
ansible -i inventory all -m command -a "systemctl status jenkins"
```