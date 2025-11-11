# Flask Application Deployment with Ansible

This project automates the deployment of a Flask web application (from GitHub) onto an Ubuntu server using Ansible, Gunicorn, and systemd.

It was built as part of my DevOps learning path and demonstrates full automation — from provisioning dependencies to running a persistent Flask service.

---

## Project Structure
ansible/
├── inventory # List of servers and SSH connection details
├── ansible.cfg # Ansible configuration (defaults and preferences)
├── site.yml # Main playbook that performs the deployment
└── templates/
└── flaskapp.service.j2 # systemd service template for running Flask via Gunicorn

---

## What the Playbook Does
1. Installs system dependencies (`git`, `python3`, `python3-venv`, `pip`)
2. Clones the Flask app from GitHub:  
   https://github.com/raz-sarusi/flaskproject.git
3. Creates a Python virtual environment  
4. Installs Flask, Gunicorn, and Requests inside the venv  
5. Generates a systemd service to run Gunicorn automatically  
6. Starts the Flask app on port 8000

---

## How to Use

### 1: Update the inventory file

[web]
server1 ansible_host=<YOUR_SERVER_PUBLIC_IP> ansible_user=ubuntu ansible_ssh_private_key_file=~/ansible.pem


### Step 2: Run the Playbook

Run the following commands from the control node (your local machine or the Ansible server):

cd ansible

ansible-playbook site.yml -i inventory


### Step 3: Access Your Application

Once the playbook finishes successfully, open your browser and visit:

http://<YOUR_SERVER_PUBLIC_IP>:8000/


You should see your Flask application running.


What I Learned
---
-Automating server configuration and deployments with Ansible

-Running Flask apps in production using Gunicorn and systemd

-Debugging permission, path, and database (SQLite) issues on Linux

-Structuring reusable playbooks for consistent DevOps automation
