# Lab 2: Automated Web Server Configuration Using Ansible Playbooks

## 🎯 Objective
This lab demonstrates how to automate the configuration of a **web server** using **Ansible**.  
By the end of this lab, you will have:
- Installed **Nginx** on a managed node.
- Deployed a **customized web page** automatically.
- Verified that the web server is running successfully.

---

## 🧰 Prerequisites
Before you start, make sure you have:
- **Ansible** installed on your control node.  
  ```bash
  ansible --version
 ```
 At least one managed node (Linux machine) accessible via SSH.

Proper SSH key-based authentication between control and managed nodes.

inventory file configured with the target node’s IP or hostname. 

## Playbook Overview

The playbook (nginx.yml) performs the following tasks:

- Install Nginx on the managed node.

- Deploy a custom index.html file to /usr/share/nginx/html/.

- Ensure Nginx service is running and enabled on boot.

- Verify that the web page is accessible.

## Run the playbook:
```bash
ansible-playbook -i inventory.ini webserver.yml
```
![alt text](<Screenshot from 2025-10-20 19-45-48.png>)
## Verification
Verify the deployment:
Open a browser on the managed node and navigate to:

http://localhost