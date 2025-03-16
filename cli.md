# CMS Cloud Manager: CLI documentation

The CLI enables the execution of a specialized YAML file to deploy everything needed on the server. Thanks to the APP, creating the YAML is straightforward. In fact, you can even run the CLI directly from the panel without needing to do anything else.

## Prepare Your Ubuntu Server

Log into your Ubuntu server via SSH:

```bash
ssh your_user@your_server_ip
```

Update the server packages:

```bash
sudo apt update && sudo apt -y upgrade
```

Install essential dependencies:

```bash
sudo apt -y install software-properties-common curl python3-pip python3-venv git
```

## Install Docker and Docker Compose

Docker will allow you to run CMS applications as containers.

Install Docker:

```bash
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo usermod -aG docker $USER
newgrp docker
```

Check Docker is working:

```bash
docker --version
```

Install Docker Compose:

```bash
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

Check Docker Compose:

```bash
docker-compose --version
```

## Install Ansible

Ansible automates the server provisioning and CMS deployment:

```bash
sudo apt-add-repository --yes --update ppa:ansible/ansible
sudo apt install -y ansible
```

Verify Ansible installation:

```bash
ansible --version
```

## Prepare Your Project Structure

Create a new directory for the deployment:

```bash
mkdir ~/cms-deployment
cd ~/cms-deployment
```

Place your automatically generated YAML file (`config.yml`) into this directory.

The structure should look like this:

```
cms-deployment/
├── config.yml
└── playbook.yml  (we'll create this in the next step)
```

## Create an Ansible Playbook

Now, create a basic Ansible playbook called `playbook.yml`. (In practice, your team will likely provide this file.)

Here’s a minimal example of what `playbook.yml` might look like, referencing your `config.yml`:

```yaml
- hosts: localhost
  connection: local
  vars_files:
    - config.yml

  tasks:
    - name: Provision server with Hetzner Cloud
      hetzner.hcloud.hcloud_server:
        api_token: "{{ apiKey }}"
        name: "{{ server_name }}"
        server_type: "{{ instance }}"
        image: ubuntu-22.04
        location: nbg1
        state: present
      register: hcloud_server

    - name: Display server IP
      debug:
        msg: "Server IP: {{ hcloud_server.hcloud_server.ipv4_address }}"

    # Example: Deploy Docker Compose remotely via SSH
    # Additional roles/tasks would be necessary to fully automate this step
```

*(Note: The exact content of `playbook.yml` may vary depending on your automation requirements.)*

## Install Ansible Collections and Dependencies

You’ll need the Hetzner collection if using Hetzner (adapt if another cloud provider is chosen):

```bash
ansible-galaxy collection install hetzner.hcloud
```

Install required Python dependencies:

```bash
pip install hcloud
```

## Execute the Ansible Playbook

Run your Ansible playbook using the provided command (substitute your actual email for Let’s Encrypt):

```bash
ansible-playbook --connection=local --inventory 127.0.0.1, playbook.yml -e letsencrypt_email=something@example.com
```

This command will provision a server based on your YAML configuration (`config.yml`).

## Deploying the CMS Containers (Docker)

After provisioning the server, you'll SSH into your newly created instance:

```bash
ssh root@your_newly_created_server_ip
```

Inside this server, use Docker Compose to deploy your CMS.  
Create a simple `docker-compose.yml` file as follows (adjust according to your components):

```yaml
version: '3.8'

services:
  wordpress-1:
    image: wordpress:latest
    container_name: wordpress-1
    restart: unless-stopped
    ports:
      - 80:80
    environment:
      WORDPRESS_DB_HOST: mariadb-1
      WORDPRESS_DB_USER: wp_user
      WORDPRESS_DB_PASSWORD: yourpassword
      WORDPRESS_DB_NAME: wp_database
    volumes:
      - wordpress_data:/var/www/html

  mariadb-1:
    image: mariadb:latest
    container_name: mariadb-1
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: wp_database
      MYSQL_USER: wp_user
      MYSQL_PASSWORD: yourpassword
    volumes:
      - db_data:/var/lib/mysql

volumes:
  wordpress_data:
  db_data:
```

Launch containers:

```bash
docker-compose up -d
```

Verify your CMS is running by accessing the server IP via your web browser.

## Secure Your CMS (Optional: Let’s Encrypt)

You can use tools like `traefik` or `certbot` for SSL/TLS certificates. For example, to quickly set up HTTPS with Certbot:

Install certbot:

```bash
sudo apt install certbot python3-certbot-nginx -y
```

Obtain SSL Certificate (assuming you’ve already pointed a domain to your server):

```bash
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com --email something@example.com --agree-tos --redirect
```

## Backups and Scalability

- Configure regular backups using cloud storage providers (AWS S3, Hetzner Storage Box).
- Adjust resources and scale containers easily via Docker Compose configuration.

🎉 **Done!**

You’ve successfully deployed your CMS server using YAML configuration, Ansible, Docker, and your selected cloud provider.

This setup offers flexibility, scalability, and security, making it ideal for your CMS deployments.
