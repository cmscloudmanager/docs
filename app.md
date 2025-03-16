# CMS Cloud Manager: App documentation

The CMS Cloud Manager app lets you create projects, choose options, and thanks to the connection to providers' APIs, obtain the YAML file to run with the CLI tool, or run it directly.

## Docker Compose

### Prerequisites

- Git
- Docker Compose

### Install Git

Install Git.

```bash
apt install -y git
git -v
```

### Install Docker

```bash
mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
apt update
apt -y install docker-ce docker-ce-cli containerd.io docker-compose
```

### Build the Docker

```bash
cd /path/to/project/app
docker-compose up --build -d
```

### Open the URL

```
http://127.0.0.1:5001/
```

### (optional) Using nginx as proxy

If you want, use nginx as proxy so its possible to install a certificate.

```nginx
server {
    listen 80;
    server_name example.com;
    location / {
        proxy_pass http://127.0.0.1:5001/;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```
