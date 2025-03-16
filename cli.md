# CMS Cloud Manager: CLI documentation

The CLI enables the execution of a specialized YAML file to deploy everything needed on the server. Thanks to the APP, creating the YAML is straightforward. 

## Requisites

- Git
- Python

## Install Python

```bash
apt -y install python3 python3-pip python3-venv
```

## Clone the repository

```bash
git clone https://github.com/cmscloudmanager/cli.git
cd cli/
```

## Set the requirements

```bash
python3 -m venv .venv
source ./venv/bin/activate
pip install -r requirements.txt
```

## Run your manifest file

```bash
python3 main.py deploy ~/my_manifest.yml
```
