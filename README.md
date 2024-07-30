# Deploy ExpressJS Application with Ansible

This Ansible playbook automates the deployment of an ExpressJS application, including the setup of PostgreSQL, Redis, Nginx, and necessary system configurations. It is designed to be run on a host group `hng`.

## Overview

This playbook performs the following tasks:
- Installs and configures necessary software packages.
- Sets up PostgreSQL and Redis services.
- Clones the application repository.
- Configures environment variables for the application.
- Installs application dependencies.
- Configures Nginx as a reverse proxy.
- Creates a systemd service to handle logging.

## Prerequisites

Before running this playbook, ensure that you have:
- Ansible installed on your local machine.
- Access to the target servers with the necessary privileges.
- Python 3 installed on the target servers.
- A valid SSH key configured for the target servers.
- The `hng` host group defined in your Ansible inventory file.

## Configuration

### Variables

You can configure the following variables in the playbook:

- `ansible_python_interpreter`: Path to the Python 3 interpreter.
- `pg_admin_user`: PostgreSQL superuser username.
- `pg_admin_password`: PostgreSQL superuser password (auto-generated from a file).
- `pg_database`: Name of the PostgreSQL database to create.
- `app_port`: Port on which the ExpressJS application will listen.
- `db_host`: Hostname or IP address of the PostgreSQL server.
- `db_port`: Port number for the PostgreSQL server.
- `redis_host`: Hostname or IP address of the Redis server.
- `redis_port`: Port number for the Redis server.

### Environment Variables

The `.env` file for the ExpressJS application is updated with the following environment variables:
- `PORT`
- `DB_USER`
- `DB_HOST`
- `DB_PASSWORD`
- `DB_PORT`
- `DB_NAME`
- `REDIS_HOST`
- `REDIS_PORT`

## Usage

1. **Clone the Playbook Repository**

   ```bash
   git clone https://github.com/luqmanAA/ansible-playbook.git
   cd ansible-playbook
    ```

2. **Run the Playbook**

    Execute the playbook using the ansible-playbook command:

   ```bash
   ansible-playbook main.yml -b -i inventory.cfg
    ```


## Playbook Details

**Software Installation**

The playbook installs the following software packages:

- git
- postgresql
- python3-pip
- curl
- gnupg
- nodejs
- nginx
- python3-psycopg2
- redis-server
- yarn


**PostgreSQL Configuration**
- Creates a PostgreSQL database and a superuser.
- Stores the PostgreSQL admin credentials in /var/secrets/pg_pw.txt.


**Application Setup**
- Clones the application repository from GitHub.
- Copies and updates the .env file with database and Redis credentials.
- Installs application dependencies using npm.


**Nginx Configuration**
- Configures Nginx to reverse proxy requests to the ExpressJS application.
- Restarts Nginx to apply the new configuration.


**Systemd Service**
- Creates and enables a systemd service for the ExpressJS application.
- Ensures the service starts on boot and restarts automatically if it fails.


**Troubleshooting**
- Nginx Configuration Issues: Check the Nginx configuration using nginx -t.
- Application Logs: Review logs at /var/log/stage_5b/out.log and /var/log/stage_5b/error.log.
- Systemd Service: Use systemctl status stage_5b to check the status of the application service.