🧩 Lab 1: Initial Ansible Configuration and Ad-Hoc Execution

📘 Overview

This lab demonstrates how to set up the Ansible Automation Platform on a control node, configure SSH key-based authentication, create an inventory file, and run ad-hoc commands to verify connectivity and automation functionality.

🎯 Objectives

By the end of this lab, you will be able to:

Install and configure Ansible on a control node.

Generate and use SSH keys for passwordless authentication.

Create an inventory file for managed nodes.

Execute ad-hoc commands to manage remote systems.

⚙️ Step 1: Install and Configure Ansible on Control Node
🪄 Commands:
# Update system packages
sudo apt update -y

# Install Ansible
sudo apt install ansible -y

# Verify Ansible installation
ansible --version

🔑 Step 2: Generate SSH Key on Control Node
🪄 Commands:
# Generate a new SSH key pair
ssh-keygen -t rsa -b 4096 -C "ansible@control-node"

# Verify the key files
ls ~/.ssh/

🔐 Step 3: Transfer the Public Key to Managed Node
🪄 Commands:
# Copy public key to the managed node
ssh-copy-id -f -i ~/.ssh/id_rsa.pub [remote-user]@[remote-ip]

# Test SSH connection
ssh [remote-user]@[remote-ip]


✅ If successful, you should connect without being prompted for a password.

📁 Step 4: Create the Ansible Inventory File
🪄 File: inventory.ini
[webservers]
remote-ip ansible_user=user-name


Replace remote-ip with the IP address of the managed node
Replace user-name with the username used for SSH access

🧠 Step 5: Run Ad-Hoc Command (Check Disk Space)
🪄 Commands:
ansible all -i inventory.ini -m command -a "df -h" --private-key ~/.ssh/id_rsa -K


✅ This command checks the disk space of all managed nodes listed in your inventory.

🧾 Summary

You have successfully:

Installed and configured Ansible.

Set up SSH key-based authentication.

Created an inventory file for managed nodes.

Executed ad-hoc commands for basic system management.