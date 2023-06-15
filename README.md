# weatherapp

## Preparation steps
- Get [OpenWeatherMap API key](https://openweathermap.org/)
- [Install docker](https://docs.docker.com/engine/install/) and [docker-compose](https://docs.docker.com/compose/install/) on your local machine
- [Install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) on your local machine
- Clone this repository to your local machine

## Setup development environment
- Place OpenWeatherMap API key in `.env` file in the root of the project

There are several ways to setup containerised development environment:

### Build containers with docker-compose
- Run `docker-compose up` in the root of the project
- Open `http://localhost:8000` in your browser to display frontend
- Weather data is available at `http://localhost:9000/api/weather`

Building containers via docker-compose is the easiest way to setup development environment. It also enables hot reloading for both frontend and backend.

**OR** 

### Build frontend and backend containers separately
- Move to `backend` directory
- Run `docker build -t weatherapp_backend --build-arg APPID=""<API_KEY>" . && docker run --rm -i -p 9000:9000 --name weatherapp_backend -t weatherapp_backend`, where <API_KEY> is your OpenWeatherMap API key

- Move to `frontend` directory
- Run `docker build -t weatherapp_frontend . && docker run --rm -i -p 8000:8000 --name weatherapp_frontend -t weatherapp_frontend`
