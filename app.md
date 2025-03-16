# CMS Cloud Manager: App documentation

The CMS Cloud Manager app lets you create projects, choose options, and thanks to the connection to providers' APIs, obtain the YAML file to run with the CLI tool, or run it directly.

## Docker install

Run the frontend

```bash
docker build -t cms-cloud-manager-frontend .
docker run -d -p 80:80 cms-cloud-manager-frontend
```

Run the backend

```bash
docker build -t cms-cloud-manager-backend .
docker run -d -p 5001:5001 cms-cloud-manager-backend
```

## Docker Compose install

```bash
docker-compose up --build -d
```

## Direct install

### Prerequisites

- Git
- NodeJS
- Python

### Install Git

Install Git.

```bash
apt install -y git
git -v
```

### Install NodeJS

Install NodeJS (for example, with Node Version Manager).

```bash
wget -q -O- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash

. ~/.bashrc
nvm --version

nvm install node
node -v
```

### Clone the Repository

Clone the repository using Git:

```bash
cd /path/to/software/
git clone https://github.com/cmscloudmanager/app.git
```

### Configure the Server

To run the server part of the backend we will need `poetry`

```bash
curl -sSL https://install.python-poetry.org | python3 -
export PATH="/root/.local/bin:$PATH"
source ~/.bashrc
poetry install
poetry --version
```

Then we run the server

```bash
cd app/server/
poetry run flask run --port 5001
```

### Configure the Client

```bash
cd app/client
npm install
npm run build
```

### (optional) Using nginx as proxy

If you want, use nginx as proxy so its possible to install a certificate.

```nginx
server {
    listen 80;
    server_name example.com;

    root /var/www/app;
    index index.html;

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
