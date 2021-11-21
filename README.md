# Docker-Compose-2021
Docker Compose NGNIX+PROMETHEUS+ALERTMANAGER

Overview
This project was designed to create containers using docker-compose. It will have Nginx container which will be monitored by Prometheus and incase Nginx instance go down Prometheus will send the alert to AlertManager.

Installation
Before we begin make sure you have docker installed in your machine. I'm using mac so installed it via following commands:

brew install docker docker-compose docker-machine xhyve docker-machine-driver-xhyve
Since docker-machine-driver-xhyve has to run as root fire following commands too:

sudo chown root:wheel $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve 
sudo chmod u+s $(brew --prefix)/opt/docker-machine-driver-xhyve/bin/docker-machine-driver-xhyve
Now you have docker installed and you are ready to start creating containers.

Lets Begin ...
Clone repo to your machine:

git clone <Repo Link>
cd <Repo>
This Repo contains docker-compose.yaml file which has the details of 3 services (Nginx, Prometheus & AlertManager) which we will be creating. All of the above services will have their own frontends available to interact with using following links:

Nginx UI
Prometheus UI
AlertManager UI
You will find the Service Specific folders which contains the configs needed to spin up these services.

1. Nginx
It has 2 files: index.html: To serve the index page / home page of Nginx UI

healthcheck.html: To serve the metrics path which will be monitored by Prometheus

2. Prometheus
It has 2 files:

alert.rules: This contains the group of rules which can be setup for monitoring. For eg: In this project we are monitoring Down Instances.

prometheus.yml: This contains the configuration for setting up Prometheus. It has sections like scrape_interval which helps to define how frequently it has to monitor, rule_files defines all the rules we have set for triggering Alerts, alerting sections helps to integrate AletManager with Prometheus and finally we provide the targets that needs to be monitored under scrape_configs.

2. alertmanager
It has 1 file:

alertmanager.yml: This file can be use to send the notifications of the Alerts triggered to Mail / slack etc.

Commands
To start all the containers, use following command:

docker-compose up -d
You will see output as:

$ docker-compose up -d
Starting nginx        ... done
Starting prometheus   ... done
Starting alertmanager ... done
You can verify all the process using:

docker ps
To Stop them:

$ docker-compose stop
Output:

$ docker-compose stop
Stopping prometheus   ... done
Stopping nginx        ... done
Stopping alertmanager ... done
