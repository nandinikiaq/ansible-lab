# Ansible Lab for Ubuntu EC2

This repository contains individual Ansible playbooks to install and configure the following on an Ubuntu EC2 instance:

1. Install and configure Ansible Inventory & SSH
2. Install and configure Docker & Docker Compose
3. Install and configure Nginx
4. Install and configure Jenkins
5. Install and configure Harbor Registry
6. Install and configure HashiCorp Vault
7. Install and configure SonarQube
8. Install and configure Prometheus & Grafana

## Prerequisites

- Ubuntu EC2 instance running on AWS
- SSH private key file saved in your Downloads folder
- Ansible installed on your local machine
- Public IP or hostname of your EC2 server

Example on Ubuntu local machine:

```bash
sudo apt update
sudo apt install ansible -y
```

## Update connection details

Before running the playbooks, update these placeholder values:

- In `inventory/hosts.ini`, replace `YOUR_EC2_PUBLIC_IP` with your EC2 public IP
- In `inventory/hosts.ini` and `ansible.cfg`, replace `your-ec2-key.pem` with your actual key file name
- Keep the actual key file in your Downloads folder, for example:

```bash
~/Downloads/your-ec2-key.pem
```

Example:

```ini
[ubuntu]
ec2-server ansible_host=54.12.34.56 ansible_user=ubuntu ansible_ssh_private_key_file=~/Downloads/my-aws-key.pem
```

Then set permissions:

```bash
chmod 400 ~/Downloads/my-aws-key.pem
```

## Run the individual playbooks

### 1) Inventory & SSH

```bash
ansible-playbook -i inventory/hosts.ini playbooks/01-setup-inventory-ssh.yml
```

### 2) Docker & Docker Compose

```bash
ansible-playbook -i inventory/hosts.ini playbooks/02-install-docker.yml
```

### 3) Nginx

```bash
ansible-playbook -i inventory/hosts.ini playbooks/03-install-nginx.yml
```

### 4) Jenkins

The Jenkins package repo requires its GPG key to be installed before `apt` can update successfully. The playbook includes the required signing key and uses the `signed-by` apt repository option to avoid the `NO_PUBKEY` / `Failed to update apt cache` error.

```bash
ansible-playbook -i inventory/hosts.ini playbooks/04-install-jenkins.yml
```

### 5) Harbor Registry

```bash
ansible-playbook -i inventory/hosts.ini playbooks/05-install-harbor.yml
```

### 6) HashiCorp Vault

```bash
ansible-playbook -i inventory/hosts.ini playbooks/06-install-vault.yml
```

### 7) SonarQube

```bash
ansible-playbook -i inventory/hosts.ini playbooks/07-install-sonarqube.yml
```

### 8) Prometheus & Grafana

```bash
ansible-playbook -i inventory/hosts.ini playbooks/08-install-prometheus-grafana.yml
```

## Optional: run all at once

```bash
ansible-playbook -i inventory/hosts.ini playbooks/*.yml
```
