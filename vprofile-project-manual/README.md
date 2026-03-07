# VProfile Project — Manual Provisioning

## Overview
A multi-tier web application stack manually provisioned 
on local VMs using Vagrant and VirtualBox.

## Architecture
User Browser → Nginx (web01) → Tomcat (app01) → MySQL (db01)
                                              → Memcache (mc01)
                                              → RabbitMQ (rmq01)

## Tech Stack
| Service     | Technology        | Role                  |
|-------------|-------------------|-----------------------|
| Web Server  | Nginx             | Reverse Proxy         |
| App Server  | Tomcat 10         | Java Application      |
| Database    | MariaDB/MySQL     | SQL Storage           |
| Cache       | Memcache          | DB Query Caching      |
| Queue       | RabbitMQ          | Message Broker        |
| Build Tool  | Maven             | Code Build & Deploy   |
| IaC         | Vagrant           | VM Provisioning       |

## VMs Provisioned
- web01 — Ubuntu (Nginx)
- app01 — CentOS (Tomcat + Maven)
- db01  — CentOS (MariaDB)
- mc01  — CentOS (Memcache)
- rmq01 — CentOS (RabbitMQ)

## Prerequisites
- VirtualBox
- Vagrant
- vagrant-hostmanager plugin

## Setup Instructions
```bash
# Install hostmanager plugin
vagrant plugin install vagrant-hostmanager

# Clone this repo
git clone https://github.com/YOURUSERNAME/vprofile-project-manual.git
cd vprofile-project-manual/vagrant

# Bring up all VMs
vagrant up
```

## What I Learned
- Manual provisioning of a multi-tier application stack
- Linux service configuration (systemctl, firewalld)
- How Nginx reverse proxy connects to a backend Tomcat server
- MariaDB setup, user creation and database initialisation
- RabbitMQ user configuration and permissions
- Memcache configuration for database caching
- Building and deploying a Java WAR file with Maven
- Troubleshooting inter-service connectivity between VMs

## Challenges & Solutions
- **RabbitMQ not starting** — rabbitmq.config loopback_users 
  was missing, recreated the config file and restarted service
- **Hosts file entries** — vagrant-hostmanager plugin 
  automatically managed /etc/hosts across all VMs

