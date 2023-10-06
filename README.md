# weatherapp

The description of the task behind this application can be found [here](https://github.com/eficode/weatherapp)
## Prerequisites
- Get [OpenWeatherMap API key](https://openweathermap.org/)
- Clone this repository to your local machine

## Setup development environment
- [Install docker](https://docs.docker.com/engine/install/) and [docker-compose](https://docs.docker.com/compose/install/) on your local machine
- Place OpenWeatherMap API key in `.env` file in the root of the project

There are several ways to setup containerised development environment:

### Build containers with docker-compose
- Run `docker-compose up` in the root of the project
- Open `http://localhost:8000` in your browser to display frontend
- Weather data is available at `http://localhost:9000/api/weather`

Building containers via docker-compose is the easiest way to set up a development environment. It also enables hot reloading for both frontend and backend.

**OR** 

### Build frontend and backend containers separately
- Move to `backend` directory
- Run `docker build -t weatherapp_backend --build-arg APPID=""<API_KEY>" . && docker run --rm -i -p 9000:9000 --name weatherapp_backend -t weatherapp_backend`, where <API_KEY> is your OpenWeatherMap API key

- Move to `frontend` directory
- Run `docker build -t weatherapp_frontend . && docker run --rm -i -p 8000:8000 --name weatherapp_frontend -t weatherapp_frontend`

## Deploy application to the cloud with Ansible

- [Install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) on your local machine
- Launch a virtual machine (VM) in the cloud (e.g. [AWS EC2 instance](https://aws.amazon.com/ec2/)). Choose Ubuntu Server 22.04 LTS as an operating system or similar.
- Place VM's SSH access key to `ansible/ec2-key.pem` file
- Place OpenWeatherMap API key in `.env` file in the root of the project (if not done yet)
- Insert VM's public IP address to `docker-compose-prod.yaml` file at `ENDPOINT` environment variable, inside the route to the APi
- Insert VM's public IP address to `ansible/hosts.yaml` file at `ansible_host` 
- Move to `ansible` directory and run `ansible-playbook deploy_app.yaml`
- Open your VM's public IP address in your browser to display frontend (use http, not https)

## Reflection
This task was a great learning experience of how to automate deployment of a full stack application to the cloud using Ansible. While Docker had been a well-known technology for me, Ansible was something completely new. Using roles and playbooks to automate deployment of the application was a great way to learn Ansible. 

Tasks:
- [x] Write Dockerfiles for frontend and backend
- [x] Write docker-compose file to run frontend and backend containers
- [x] Write Ansible playbooks to install docker and docker-compose on a VM
- [x] Write Ansible playbook to run application on a VM

*Tasks on testing and NodeJS/React haven't been started*

Things to improve:
- [ ] Create VM in the cloud with Terraform
- [ ] Run VMs behind a load balancer, attach a domain name
- [ ] Use Ansible Vault to encrypt sensitive data
- [ ] Deploy build package of frontend, instead of development version (I ran into issue with webpack built and didn't have enough time to fix it)
