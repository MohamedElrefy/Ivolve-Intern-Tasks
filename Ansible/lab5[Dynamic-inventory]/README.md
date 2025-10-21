# 🧩 Lab 5: Automated Host Discovery with Ansible Dynamic Inventory
# 📘 Overview

This lab demonstrates how to configure Ansible Dynamic Inventory to automatically discover and manage AWS EC2 instances using AWS tags.
You will create an EC2 instance with a specific tag, configure AWS credentials, set up a dynamic inventory plugin, and verify host discovery by running ad-hoc commands or a simple playbook.

# 🎯 Objectives

By the end of this lab, you will be able to:

Create and tag an EC2 instance in AWS.

Configure AWS credentials for Ansible.

Set up a dynamic inventory file using the AWS EC2 plugin.

Automatically discover EC2 instances and manage them through Ansible.

Verify connectivity using Ansible commands or playbooks.

# ☁️ Step 1: Create AWS User & Access key for ansible 
create user and then Under security credentials add access key and download it
Choose access key use case  --> Application running outside AWS
then on your VM 
![alt text](<Untitled.jpeg>)
enter you access key and secret access key
# ☁️ Step 2: Create AWS EC2 Instance with Tag
## 🪄 Commands:
 Create a new EC2 instance (example using AWS CLI)
```bash 
aws ec2 run-instances \
  --image-id ami-xxxxxx \
  --count 1 \
  --instance-type t2.micro \
  --key-name my-key \
  --security-group-ids sg-xxxxxx \
  --subnet-id subnet-xxxxxx \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=ivolve}]'
```
 and create another ec2 with different tag to filter with tags in the inventory "verification"

 or using the aws console  make sure security group enable SSH


✅ Ensure your instance has the tag Name=ivolve.
You can verify with:
```bash
aws ec2 describe-instances --filters "Name=tag:Name,Values=ivolve" --query "Reservations[].Instances[].InstanceId"
```

# 🧾 Step 3: Create the Dynamic Inventory File
🪄 File: inventory.aws_ec2.yaml

⚠️ Make sure you have the boto3 and botocore Python libraries installed:
```bash
pip install boto3 botocore
```
at the end I provided a solution to specific error about these two libraries

Also ensure the amazon.aws collection is installed:
```bash
ansible-galaxy collection install amazon.aws
```
# 🔍 Step 4: List Discovered Hosts
🪄 Commands:
```bash
ansible-inventory -i dynamic_inventory.yml --graph
```

✅ This command will show all EC2 instances tagged with Name=ivolve grouped dynamically.

To view detailed host information:
```bash
ansible-inventory -i dynamic_inventory.yml --list
```
# 🧠 Step 5: RUN Playbook
Run the playbook:
```bash
ansible-playbook -i dynamic_inventory.yml test.yml
```
![alt text](<Screenshot from 2025-10-18 18-02-34.png>)

as we see the playbook apllied only on the machine with Tag ivolve
# 🧩 Issue: AWS Dynamic Inventory Plugin Failed to Load

## Error message:

Failed to import the required Python library (botocore and boto3)


## Cause:
Ansible was unable to load the amazon.aws.aws_ec2 dynamic inventory plugin because the required Python libraries boto3 and botocore were not installed in the same environment where Ansible is running.
This usually happens when Ansible is installed using pipx and the AWS SDK libraries are installed in a different Python environment.

## 🛠️ Solution

Identify which Python interpreter Ansible is using:
```bash
ansible --version
```

Example output:

python version = /home/mohamed/.local/share/pipx/venvs/ansible/bin/python


Install the missing AWS libraries in that exact environment:
```bash
/home/mohamed/.local/share/pipx/venvs/ansible/bin/python -m pip install boto3 botocore
```

Verify the installation:
```bash
/home/mohamed/.local/share/pipx/venvs/ansible/bin/python -m pip show boto3 botocore
```

Test the AWS dynamic inventory:
```bash
ansible-inventory -i inventory.aws_ec2.yaml --list
```

If the inventory is listed successfully, run your playbook:
```bash
ansible-playbook -i inventory.aws_ec2.yaml nginx.yml
```