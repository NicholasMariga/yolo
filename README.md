
YOLO App Deployment with Vagrant and Ansible

Project Overview

This project demonstrates the automated provisioning and configuration of a 3-tier containerized web application called YOLO App, consisting of:

- app-client (React frontend)
- app-backend (Node.js backend)
- app-ip-mongo (MongoDB)

We use:
- Vagrant for VM provisioning (VirtualBox),
- Ansible for configuration management (roles, tasks),
- Docker and Docker Compose to containerize and deploy the application.

Tech Stack

| Layer         | Technology          |
|---------------|---------------------|
| Provisioning  | Vagrant (VirtualBox)|
| OS            | Ubuntu 20.04        |
| Configuration | Ansible             |
| Runtime       | Docker              |
| Backend       | Node.js             |
| Frontend      | React               |
| Database      | MongoDB             |

Directory Structure

├── Vagrantfile
├── ansible.cfg
├── inventory.yml
├── hosts
├── playbook.yaml
├── backend
├── client
├── images
├── roles/
│   ├── app-mongodb/
│   │   └── tasks/main.yml
│   ├── app-backend/
│   │   └── tasks/main.yml
│   ├── app-client/
│   │   └── tasks/main.yml

VM Provisioning

We use Vagrant to provision a VirtualBox VM with bridged networking:

Vagrantfile (Summary)

Vagrant.configure("2") do |config|
  config.vm.box = "geerlingguy/ubuntu2004"
  config.vm.network "public_network" # Bridged
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yaml"
  end
end

Configuration Management with Ansible

Ansible is structured using roles, with each major app component having its own role.

Main Playbook: deploy.yml

---
- name: Deploy YOLO App Stack
  hosts: all
  become: true

  roles:
    - app-mongodb
    - app-backend
    - app-client

Role Breakdown

1. app-mongodb
- Creates Docker volume (app-mongo-data)
- Creates Docker network (app-net)
- Starts MongoDB container

2. app-backend
- Builds image from backend/Dockerfile
- Starts container and connects to MongoDB

3. app-client
- Builds React frontend image
- Starts container and connects to backend

Container Networking

All services run in the Docker network app-net, ensuring containers can discover and communicate internally.

networks:
  - name: app-net

Deployment Steps

1. Clone the repo
2. Run:

vagrant up 
vagrant up --provision

This will:
- Provision the VM using VirtualBox
- Trigger Ansible to install Docker, set up roles, and run containers

Verification

Once setup is complete:
- Visit http://<VM_IP>:3000 to access the YOLO App frontend
- API runs on port 5000
- MongoDB accessible on port 27017

Use docker ps inside the VM to confirm containers are running.

